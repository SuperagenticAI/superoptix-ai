# SuperOptiX Reference Architecture Analysis
## Comprehensive Overview of GEPA, DSPy, and MCP Tool Optimization

---

## Executive Summary

SuperOptiX contains a sophisticated reference architecture supporting:
1. **GEPA** - Graph Enhanced Prompting Algorithm for reflective prompt evolution
2. **DSPy** - Enhanced framework with MCP (Model Context Protocol) integration
3. **MCP Tool Optimization** - Production-grade MCP adapter for optimizing tool descriptions and system prompts

The project integrates GEPA, DSPy, and MCP to create a complete system for optimizing AI agents and their tool usage patterns.

---

## Directory Structure

```
/Users/local/superagentic/SuperOptiX/
├── reference/                          # Reference implementations
│   ├── gepa/                          # GEPA framework (Graph Enhanced Prompting Algorithm)
│   │   ├── src/gepa/
│   │   │   ├── core/                  # Core GEPA engine
│   │   │   │   ├── adapter.py         # GEPAAdapter protocol
│   │   │   │   ├── engine.py          # Optimization engine
│   │   │   │   ├── state.py           # State management
│   │   │   │   └── result.py          # Result tracking
│   │   │   ├── adapters/              # Framework integrations
│   │   │   │   ├── mcp_adapter/       # MCP ADAPTER (NEW - Production Grade)
│   │   │   │   │   ├── mcp_adapter.py            # 628 lines - Main MCP adapter
│   │   │   │   │   ├── mcp_types.py              # Type definitions
│   │   │   │   │   ├── simple_stdio_client.py    # Local MCP client
│   │   │   │   │   ├── sse_client.py             # Remote SSE transport
│   │   │   │   │   ├── streamable_http_client.py # Production HTTP transport
│   │   │   │   │   └── __init__.py
│   │   │   │   ├── dspy_adapter/      # DSPy integration
│   │   │   │   ├── generic_rag_adapter/  # RAG support
│   │   │   │   └── default_adapter/
│   │   │   ├── proposer/              # Instruction proposal strategies
│   │   │   │   ├── base.py
│   │   │   │   ├── merge.py
│   │   │   │   └── reflective_mutation/
│   │   │   ├── strategies/            # Optimization strategies
│   │   │   │   ├── batch_sampler.py
│   │   │   │   ├── candidate_selector.py
│   │   │   │   ├── component_selector.py
│   │   │   │   └── instruction_proposal.py
│   │   │   ├── examples/
│   │   │   │   ├── mcp_tool_optimization/  # MCP EXAMPLES
│   │   │   │   │   ├── README.md           # Complete tutorial
│   │   │   │   │   ├── simple_mcp_server.py # Local MCP server
│   │   │   │   │   ├── local_ollama.py      # Local optimization
│   │   │   │   │   ├── cloud_api.py         # OpenAI-based
│   │   │   │   │   └── remote_server.py     # Remote MCP
│   │   │   │   ├── aime.py
│   │   │   │   └── rag_adapter/
│   │   │   └── logging/
│   │   ├── tests/
│   │   │   └── test_mcp_adapter/
│   │   │       ├── test_mcp_adapter.py
│   │   │       ├── test_mcp_integration.py
│   │   │       └── test_mcp_types.py
│   │   ├── README.md
│   │   ├── pyproject.toml
│   │   └── CONTRIBUTING.md
│   │
│   └── dspy/                          # DSPy reference implementation
│       ├── dspy/
│       │   ├── teleprompt/            # Optimizers
│       │   │   ├── mipro_optimizer_v2.py   # MIPROv2
│       │   │   ├── copro_optimizer.py      # COPRO
│       │   │   ├── simba.py                # SIMBA
│       │   │   ├── bootstrap.py            # Bootstrap
│       │   │   ├── grpo.py                 # GRPO
│       │   │   ├── avatar_optimizer.py     # Avatar
│       │   │   └── utils.py
│       │   ├── utils/
│       │   │   └── mcp.py             # DSPy MCP utilities (47 lines)
│       │   ├── adapters/
│       │   ├── clients/
│       │   ├── evaluate/
│       │   └── signatures/
│       ├── docs/
│       │   └── docs/learn/
│       │       ├── programming/mcp.md # MCP Integration Guide
│       │       └── optimization/
│       └── tests/
│           ├── utils/test_mcp.py
│           └── utils/resources/mcp_server.py
│
└── superoptix/                        # SuperOptiX implementation
    ├── core/
    │   ├── optimizer_factory.py        # 826 lines - Optimizer factory
    │   ├── base_pipeline.py
    │   ├── pipeline_utils.py           # Enhanced with optimizer factory
    │   ├── rag_mixin.py
    │   └── validation.py
    ├── agents/
    │   └── dspy_optimizers/            # Optimizer demonstration agents
    │       ├── gepa_playbook.yaml
    │       ├── gepa_math_agent_playbook.yaml
    │       ├── simba_playbook.yaml
    │       ├── copro_playbook.yaml
    │       ├── miprov2_playbook.yaml
    │       ├── bootstrapfewshot_playbook.yaml
    │       ├── labeledfewshot_playbook.yaml
    │       └── knnfewshot_playbook.yaml
    ├── tools/
    ├── models/
    ├── memory/
    └── observability/
```

---

## Key Component Analysis

### 1. GEPA Framework (`/reference/gepa`)

**Purpose**: Graph Enhanced Prompting Algorithm for reflective optimization of text components

**Core Architecture**:
- **GEPAAdapter Protocol** (`core/adapter.py`): Interface for integrating systems with GEPA
  - `evaluate()`: Execute candidate on batch data
  - `make_reflective_dataset()`: Build feedback dataset for reflection
  - `propose_new_texts()`: Optional custom proposal logic

- **Optimization Engine** (`core/engine.py`): Main GEPA optimization loop
  - Supports multiple objective optimization
  - Pareto-front selection
  - Reflective mutation strategies

- **Key Features**:
  - Works with any text component system
  - Supports multiple transport types (local stdio, remote SSE, HTTP)
  - Captures detailed execution trajectories
  - Reflective feedback for continuous improvement

**Available Adapters**:
1. **MCP Adapter** (NEW, Production Grade) - See section 2
2. **DSPy Adapter** - Optimize DSPy module signatures
3. **Generic RAG Adapter** - Optimize RAG pipeline components
4. **Default Adapter** - Single-turn LLM environment
5. **AnyMaths Adapter** - Mathematical problem solving

---

### 2. MCP Adapter Implementation (`/reference/gepa/src/gepa/adapters/mcp_adapter`)

**Status**: Production-grade implementation with comprehensive features

**Files & Sizes**:
```
mcp_adapter.py              628 lines   Main adapter implementation
mcp_types.py               ~60 lines   Type definitions
simple_stdio_client.py      ~80 lines   Local stdio client (workaround for SDK bug)
sse_client.py              ~150 lines   Remote SSE transport
streamable_http_client.py  ~170 lines   Production HTTP transport
__init__.py                ~30 lines   Module exports
```

**Key Features**:

1. **Transport Support**:
   - Local Stdio (subprocess-based, via StdioServerParameters)
   - Remote SSE (Server-Sent Events)
   - Remote StreamableHTTP (production-grade, recommended)

2. **Tool Optimization Capabilities**:
   - Tool descriptions
   - System prompts
   - Tool usage guidelines
   - Multi-tool scenarios (supports multiple tools)

3. **Execution Model**:
   - Two-pass workflow:
     1. **First Pass**: Model receives query, decides to call tool
     2. **Second Pass**: Model receives tool response, generates final answer
   - Optional two-pass execution (configurable)
   - Detailed trajectory capture for reflection

4. **Type Definitions**:
   ```python
   MCPDataInst:     Dataset item (user_query, tool_arguments, reference_answer, context)
   MCPTrajectory:   Execution trace (tool used, args, response, descriptions, scores)
   MCPOutput:       Final output (answer, tool_called, selected_tool, response)
   ```

5. **Core Methods**:
   - `evaluate()`: Run candidate on batch using MCP tool
   - `_first_pass()`: Model calls tool based on query
   - `_second_pass()`: Model generates answer from tool response
   - `_build_system_prompt()`: Creates prompt with tool information
   - `make_reflective_dataset()`: Creates feedback for reflection
   - `_generate_tool_feedback()`: Generates tool-focused feedback
   - `_generate_system_prompt_feedback()`: Generates system prompt feedback

6. **Configuration**:
   ```python
   MCPAdapter(
       tool_names="read_file",                    # Single or list
       task_model="gpt-4o-mini",                  # LiteLLM compatible
       metric_fn=lambda item, output: score,      # Custom scoring
       server_params=StdioServerParameters(...),  # Local config
       remote_url="https://mcp-server.com/sse",   # Remote config
       remote_transport="sse" or "streamable_http",
       base_system_prompt="You are helpful...",
       enable_two_pass=True,
       failure_score=0.0,
   )
   ```

**Complete Example Flow**:
```python
# 1. Setup
adapter = MCPAdapter(
    tool_names=["read_file", "write_file"],
    task_model="gpt-4o-mini",
    metric_fn=custom_metric,
    server_params=StdioServerParameters(
        command="python",
        args=["mcp_server.py", "/tmp"]
    )
)

# 2. Create candidates to optimize
seed_candidate = {
    "tool_description_read_file": "Read file",
    "system_prompt": "You are helpful"
}

# 3. Optimize with GEPA
from gepa import optimize
result = optimize(
    seed_candidate=seed_candidate,
    trainset=train_data,
    valset=val_data,
    task_lm="gpt-4o-mini",
    reflection_lm="gpt-4o",
    adapter=adapter,
    max_metric_calls=100,
)
```

---

### 3. DSPy Integration

**Location**: `/reference/dspy/dspy`

**MCP Support**:
- **File**: `dspy/utils/mcp.py` (47 lines)
- **Utilities**:
  - `convert_mcp_tool()`: Convert MCP tool to DSPy tool
  - `_convert_mcp_tool_result()`: Extract text from MCP responses

- **Documentation**: `docs/docs/learn/programming/mcp.md`
  - HTTP Server (remote) examples
  - Stdio Server (local) examples
  - Tool conversion patterns
  - ReAct agent integration

**Optimizer Ecosystem** (`dspy/teleprompt/`):
```
Available Optimizers:
- GEPA           - Reflective prompt evolution
- SIMBA          - Stochastic introspective batch ascent
- MIPROv2        - Multi-step instruction prompt optimization
- COPRO          - Collaborative prompt optimization
- Bootstrap      - Few-shot bootstrapping
- BetterTogether - Ensemble few-shot
- KNNFewShot     - K-nearest neighbor few-shot
- LabeledFewShot - Traditional few-shot
- Random Search  - Random search over candidates
- Ensemble       - Model ensemble
- GRPO           - Generative reward policy optimization
- Avatar         - Avatar-based optimization
```

**ReAct + MCP Integration**:
```python
# Convert MCP tools to DSPy
dspy_tools = [
    dspy.Tool.from_mcp_tool(session, tool)
    for tool in response.tools
]

# Use with ReAct
react_agent = dspy.ReAct(
    signature=TaskSignature,
    tools=dspy_tools,
    max_iters=5
)
```

---

### 4. SuperOptiX Optimizer Factory (`/superoptix/core/optimizer_factory.py`)

**Status**: 826 lines, production-ready

**Key Components**:
1. **Optimizer Registry**: Maps optimizer names to DSPy classes
2. **Default Parameters**: Sensible defaults for each optimizer
3. **Factory Methods**:
   - `create_optimizer()`: Main factory method
   - `_configure_optimizer()`: Route to specific configuration
   - `_configure_gepa()`: GEPA-specific setup
   - `_configure_simba()`: SIMBA-specific setup
   - etc.

4. **Features**:
   - Supports both string names and alternative names (e.g., "gepa" or "GEPA")
   - Normalizes parameters (removes underscores/hyphens)
   - LM configuration support for GEPA
   - Graceful error handling

5. **Tier-Optimized Optimizer Creation**:
   ```python
   # Automatically selects best optimizer for tier
   optimizer = DSPyOptimizerFactory.create_tier_optimized_optimizer(
       tier="oracles",           # Different tier optimization
       training_data_size=10,
       optimizer_config=None,
   )
   ```

---

## MCP Tool Optimization Examples

**Location**: `/reference/gepa/src/gepa/examples/mcp_tool_optimization`

### Quick Start Options:

| Example | Models | API Keys | Best For |
|---------|--------|----------|----------|
| **local_ollama.py** | Local Ollama | None | 100% local, free |
| **cloud_api.py** | OpenAI API | Required | Production quality |
| **remote_server.py** | Any | Maybe | Remote MCP tools |

### `local_ollama.py` (100% Local, Recommended)
- Models: llama:3.2:1b (task), llama:3.1:8b (reflection)
- Cost: $0.00
- Runtime: 3-10 minutes
- System: Ollama running locally

### `cloud_api.py` (OpenAI-based)
- Creates test files
- Optimizes `read_file` tool description
- Shows before/after comparison
- Expected improvement documented

### `remote_server.py` (Remote MCP)
- Command-line interface
- SSE or StreamableHTTP transport
- Authentication support
- Public/hosted MCP server support

### `simple_mcp_server.py` (Local MCP Implementation)
- Provides file system tools
- Supports: read_file, write_file, list_files
- Security: Path traversal protection
- Stdio transport

---

## Current Implementation Status

### Fully Implemented & Production Ready:

1. **GEPA Framework Core**
   - Optimization engine
   - Pareto-front selection
   - Reflective mutation
   - Multi-component optimization

2. **MCP Adapter** (New, 2025)
   - Full async support
   - Multiple transport types
   - Tool optimization
   - Trajectory capture
   - Comprehensive testing framework

3. **DSPy Integration**
   - MCP utilities
   - ReAct + MCP support
   - Multiple optimizers
   - Tool conversion

4. **SuperOptiX Optimizer Factory**
   - 10+ optimizers supported
   - Tier-aware selection
   - LM configuration
   - Parameter normalization

### Partially Implemented:

1. **RAG Integration**
   - Generic RAG adapter exists
   - Multiple vector DB support
   - But: Limited optimization examples

2. **Tool Integration**
   - MCP tools supported
   - DSPy tools supported
   - But: Limited domain-specific examples

### Not Yet Implemented:

1. **MCP Tool Optimizer API** (Main Integration Point)
   - Wrapper around MCPAdapter for easy SuperOptiX integration
   - Plugin architecture for custom transport/strategies

2. **SuperOptiX Native MCP Tools**
   - MCP adapter in superoptix/tools/
   - Native integration with tool registry

3. **MCP Playbook Support**
   - SuperSpec playbooks for MCP optimization
   - Tool description templates
   - Optimization strategy YAML configs

4. **Advanced Features**:
   - Tool argument optimization
   - Multi-tool routing optimization
   - Tool error handling strategies
   - Caching/memoization for tool calls
   - A/B testing framework for tools

---

## Architecture Patterns

### 1. Adapter Pattern (GEPA Core)
```
┌─────────────────────┐
│   GEPA Engine       │
│  (optimization)     │
└──────────┬──────────┘
           │
           │ uses
           ▼
┌─────────────────────┐
│   GEPAAdapter       │ (Protocol)
│ - evaluate()        │
│ - make_reflective   │
│ - propose_new()     │
└──────────┬──────────┘
           │
     ┌─────┴─────┬──────────┬───────────┐
     │            │          │           │
     ▼            ▼          ▼           ▼
  MCPAdapter  DSPyAdapter  RAGAdapter  DefaultAdapter
```

### 2. Transport Abstraction (MCP Adapter)
```
┌──────────────────────┐
│   MCPAdapter         │
│  (optimization)      │
└──────────┬───────────┘
           │
      ┌────┴────┬─────────────┐
      │          │             │
      ▼          ▼             ▼
  Stdio       SSE         StreamableHTTP
  (local)    (remote)     (production)
```

### 3. Two-Pass Workflow (MCP Adapter)
```
User Query
    │
    ▼
┌────────────────────────┐
│ First Pass:            │
│ Model decides to call  │
│ tool (JSON output)     │
└────────────┬───────────┘
             │
    ┌────────▼────────┐
    │ Tool Execution  │
    │ via MCP         │
    └────────┬────────┘
             │
    ┌────────▼───────────────────────┐
    │ Second Pass:                    │
    │ Model generates final answer    │
    │ from tool response (if enabled) │
    └────────┬───────────────────────┘
             │
        Final Answer
```

---

## Integration Points & Extension Strategy

### For SuperOptiX Integration:

1. **MCPAdapter → SuperOptiX Wrapper**
   - Create `/superoptix/agents/mcp_optimizer/` with MCPToolOptimizer class
   - Wrap MCPAdapter with SuperOptiX conventions

2. **Playbook Support**
   - Define MCP optimization playbook schema
   - Support in SuperSpec DSL:
     ```yaml
     optimization:
       type: mcp_tool_optimization
       adapter: MCPAdapter
       mcp_config:
         server: local  # or remote
         tools: ["read_file", "write_file"]
         optimization_targets:
           - tool_description
           - system_prompt
     ```

3. **Tool Registry Integration**
   - Register MCP tools in SuperOptiX tool system
   - Support tool optimization in CLI:
     ```bash
     super tool optimize read_file --adapter mcp
     ```

4. **Observable Integration**
   - Use existing tracing infrastructure
   - Surface MCP optimization metrics in dashboard
   - Track tool usage patterns

---

## What's Already Built

### Reference Implementations:
1. MCPAdapter (628 lines) - Full-featured MCP tool optimization
2. GEPA Framework - Complete optimization engine
3. DSPy Integration - MCP utilities and optimizers
4. 20+ DSPy optimizer demo playbooks
5. MCP examples (local, cloud, remote)
6. Complete testing framework

### What Works:
- Local MCP server optimization (Ollama example)
- Cloud API optimization (OpenAI example)
- Remote MCP optimization (SSE, HTTP)
- Multi-tool optimization
- Trajectory capture & reflection
- Custom metric functions
- Batch evaluation

---

## What Needs to Be Built

### Priority 1 (Core Integration):
1. MCPToolOptimizer class in SuperOptiX
2. SuperSpec MCP playbook support
3. Integration with optimizer factory
4. CLI command for MCP tool optimization

### Priority 2 (Enhanced Features):
1. Caching layer for MCP calls
2. Error recovery strategies
3. Tool argument optimization
4. Multi-tool routing optimization

### Priority 3 (Advanced):
1. A/B testing framework
2. Performance profiling
3. Cost optimization
4. Tool versioning

---

## Key Files Reference

**GEPA MCP Adapter**:
- Main: `/Users/local/superagentic/SuperOptiX/reference/gepa/src/gepa/adapters/mcp_adapter/mcp_adapter.py`
- Types: `/Users/local/superagentic/SuperOptiX/reference/gepa/src/gepa/adapters/mcp_adapter/mcp_types.py`
- Transport: SSE, StreamableHTTP clients

**DSPy MCP Utils**:
- Utils: `/Users/local/superagentic/SuperOptiX/reference/dspy/dspy/utils/mcp.py`
- Docs: `/Users/local/superagentic/SuperOptiX/reference/dspy/docs/docs/learn/programming/mcp.md`

**SuperOptiX Optimizer**:
- Factory: `/Users/local/superagentic/SuperOptiX/superoptix/core/optimizer_factory.py`
- Examples: `/Users/local/superagentic/SuperOptiX/superoptix/agents/dspy_optimizers/`

**Examples**:
- MCP: `/Users/local/superagentic/SuperOptiX/reference/gepa/src/gepa/examples/mcp_tool_optimization/`

---

## Recommendations

1. **Start with MCPToolOptimizer wrapper** - Easy integration point
2. **Add MCP playbook support** - Enables YAML-based configuration
3. **Integrate with CLI** - `super agent optimize --mcp` command
4. **Add example agents** - Demonstrate real-world usage
5. **Document integration** - Update CLAUDE.md with MCP examples

---

*Analysis generated: 2025-10-18*
*Working directory: /Users/local/superagentic/SuperOptiX*
