# MCP Tool Optimization Integration Summary

## Quick Overview

**Status**: Production-grade MCP adapter exists in `/reference/gepa` - ready for SuperOptiX integration

**Implementation Location**:
```
/Users/local/superagentic/SuperOptiX/reference/gepa/src/gepa/adapters/mcp_adapter/
```

---

## The MCPAdapter Class (628 lines)

### What It Does
Optimizes MCP tool usage by evolving:
- Tool descriptions (how tools are described to the model)
- System prompts (how the model is instructed to use tools)
- Tool usage guidelines

### How It Works
1. **Two-Pass Execution**:
   - Pass 1: Model sees user query, decides which tool to call
   - Pass 2: Model sees tool response, generates final answer
   
2. **Transport Flexibility**:
   - Local Stdio (subprocess, via `StdioServerParameters`)
   - Remote SSE (Server-Sent Events)
   - Remote StreamableHTTP (production-grade)

3. **Optimization Loop**:
   - GEPA engine tests candidates
   - MCPAdapter evaluates on batch
   - Generates feedback from execution traces
   - Proposes improved tool descriptions & prompts

### Supported Optimizations
```python
seed_candidate = {
    "tool_description_read_file": "Original description",
    "tool_description_write_file": "Original description",
    "system_prompt": "You are a helpful assistant with access to tools",
}
```

---

## Complete Integration Example

```python
# 1. Import
from gepa.adapters.mcp_adapter import MCPAdapter
from gepa import optimize
from mcp import StdioServerParameters

# 2. Define metric function
def score_output(item, output):
    # item has: user_query, tool_arguments, reference_answer
    # output has: final_answer, tool_called, selected_tool, tool_response
    if item["reference_answer"] in output["final_answer"]:
        return 1.0
    return 0.0

# 3. Create adapter
adapter = MCPAdapter(
    tool_names=["read_file", "write_file"],
    task_model="gpt-4o-mini",
    metric_fn=score_output,
    server_params=StdioServerParameters(
        command="python",
        args=["mcp_server.py", "/tmp"],
    ),
    enable_two_pass=True,
)

# 4. Define what to optimize
seed_candidate = {
    "tool_description_read_file": "Read the contents of a file from the filesystem.",
    "system_prompt": "You are a helpful assistant with access to tools.",
}

# 5. Create training/validation data
trainset = [
    {
        "user_query": "What is in file.txt?",
        "tool_arguments": {"path": "file.txt"},
        "reference_answer": "file contents",
        "additional_context": {},
    },
    # ... more examples
]

# 6. Run GEPA optimization
result = optimize(
    seed_candidate=seed_candidate,
    trainset=trainset,
    valset=trainset,  # Usually separate
    adapter=adapter,
    task_lm="gpt-4o-mini",
    reflection_lm="gpt-4",
    max_metric_calls=50,
)

print("Optimized tool description:", result.best_candidate["tool_description_read_file"])
print("Optimized system prompt:", result.best_candidate["system_prompt"])
```

---

## Key Files

| File | Size | Purpose |
|------|------|---------|
| `mcp_adapter.py` | 628 lines | Main adapter - evaluation, two-pass workflow, feedback generation |
| `mcp_types.py` | ~60 lines | Type definitions (MCPDataInst, MCPTrajectory, MCPOutput) |
| `simple_stdio_client.py` | ~80 lines | Workaround for MCP SDK stdio bug - local client |
| `sse_client.py` | ~150 lines | Remote SSE transport |
| `streamable_http_client.py` | ~170 lines | Production HTTP transport |

---

## What It Optimizes

### 1. Tool Descriptions
```python
# Original
"Read the contents of a file from the filesystem."

# GEPA can optimize to
"Read and return the complete text contents of a file. Use when the user asks about file contents, configuration settings, or data stored in files. Provide the file path as an argument."
```

### 2. System Prompts
```python
# Original
"You are a helpful assistant with access to tools."

# GEPA can optimize to include:
# - Specific tool guidance
# - When to use/avoid tools
# - Expected output formats
# - Error handling strategies
```

---

## Transport Options

### Local (Stdio) - Perfect for Development
```python
server_params = StdioServerParameters(
    command="python",
    args=["mcp_server.py", "/tmp"],
    env={"PYTHON_PATH": "/path/to/env"},
)

adapter = MCPAdapter(
    tool_names=["read_file"],
    task_model="gpt-4o-mini",
    metric_fn=score_fn,
    server_params=server_params,  # <- Local
)
```

### Remote SSE - Simple Remote
```python
adapter = MCPAdapter(
    tool_names=["search_web"],
    task_model="gpt-4o-mini",
    metric_fn=score_fn,
    remote_url="https://mcp-server.com/sse",  # <- Remote SSE
    remote_transport="sse",
)
```

### Remote StreamableHTTP - Production
```python
adapter = MCPAdapter(
    tool_names=["analyze_data"],
    task_model="gpt-4o-mini",
    metric_fn=score_fn,
    remote_url="https://mcp-server.com/mcp",  # <- Remote HTTP
    remote_transport="streamable_http",
    remote_headers={"Authorization": "Bearer TOKEN"},
    remote_timeout=30,
)
```

---

## What Gets Captured

### Trajectories (Execution Traces)
```python
trajectory = {
    "user_query": "What is in config.txt?",
    "tool_names": ["read_file"],
    "selected_tool": "read_file",
    "tool_called": True,
    "tool_arguments": {"path": "config.txt"},
    "tool_response": "# Configuration...",
    "tool_description_used": "Read file...",
    "system_prompt_used": "You are...",
    "model_first_pass_output": '{"action": "call_tool", ...}',
    "model_final_output": "The config contains...",
    "score": 1.0,
}
```

### Available Outputs
```python
output = {
    "final_answer": "The config contains...",
    "tool_called": True,
    "selected_tool": "read_file",
    "tool_response": "# Configuration...",
}
```

---

## Multi-Tool Support

```python
# Optimize multiple tools at once
adapter = MCPAdapter(
    tool_names=["read_file", "write_file", "list_files"],  # Multiple!
    task_model="gpt-4o-mini",
    metric_fn=score_fn,
    server_params=server_params,
)

seed_candidate = {
    "tool_description_read_file": "...",
    "tool_description_write_file": "...",
    "tool_description_list_files": "...",
    "system_prompt": "You have access to file system tools...",
}
```

---

## Error Handling

The adapter handles errors gracefully:

```python
# Execution failures -> failure_score (default 0.0)
# Invalid tool selection -> silently ignored
# Tool response extraction -> handles various formats
# Type mismatches -> logged with context
```

---

## Performance Characteristics

- **Batch Processing**: Async evaluation for efficiency
- **Resource Management**: Proper client cleanup
- **Error Recovery**: Continues on individual item failures
- **Tracing Overhead**: Optional trajectory capture (capture_traces=True/False)

---

## Integration with SuperOptiX (Next Steps)

### What Needs to Happen:
1. Create wrapper class in `superoptix/core/mcp_optimizer.py`
2. Add MCP playbook support to SuperSpec
3. Integrate with optimizer_factory
4. Add CLI command `super agent optimize --mcp`

### Suggested API:
```python
from superoptix.core.mcp_optimizer import MCPToolOptimizer

optimizer = MCPToolOptimizer(
    agent_name="file_assistant",
    tool_names=["read_file", "write_file"],
    optimization_targets=["tool_description", "system_prompt"],
    mcp_config={
        "type": "local",  # or "remote"
        "server": "mcp_server.py",
    }
)

result = optimizer.optimize(
    training_data=trainset,
    metric_fn=score_fn,
    max_iterations=50,
)
```

---

## Examples Ready to Use

| Example | Setup | Cost | Time | Status |
|---------|-------|------|------|--------|
| `local_ollama.py` | Ollama running | Free | 3-10 min | Works great |
| `cloud_api.py` | OpenAI key | $$ | 2-5 min | Fast iteration |
| `remote_server.py` | MCP server URL | Varies | Immediate | Production-ready |

**Location**: `/Users/local/superagentic/SuperOptiX/reference/gepa/src/gepa/examples/mcp_tool_optimization/`

---

## Current Status Matrix

| Component | Status | Location | Notes |
|-----------|--------|----------|-------|
| MCPAdapter | Ready | reference/gepa/adapters | Full implementation, tested |
| GEPA Engine | Ready | reference/gepa/core | Complete optimization |
| DSPy Integration | Ready | reference/dspy | MCP utilities, optimizers |
| Optimizer Factory | Ready | superoptix/core | 10+ optimizers |
| Examples | Ready | reference/gepa/examples | Local, cloud, remote |
| Tests | Ready | reference/gepa/tests | Comprehensive coverage |
| SuperOptiX Wrapper | Not Yet | - | **TODO** |
| Playbook Support | Not Yet | - | **TODO** |
| CLI Integration | Not Yet | - | **TODO** |

---

## Code Quality

- **Line Coverage**: All critical paths tested
- **Type Hints**: Full typing throughout
- **Error Handling**: Comprehensive with logging
- **Documentation**: Docstrings, examples, READMEs
- **Compatibility**: Works with local & remote MCP servers

---

## Next Actions

1. Review `/Users/local/superagentic/SuperOptiX/reference/gepa/src/gepa/adapters/mcp_adapter/mcp_adapter.py`
2. Run example: `python /reference/gepa/src/gepa/examples/mcp_tool_optimization/local_ollama.py`
3. Create SuperOptiX wrapper class
4. Add playbook schema support
5. Implement CLI integration

---

*Summary generated: 2025-10-18*
