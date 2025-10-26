# SuperOptiX Reference Documentation

This directory contains comprehensive analysis and documentation of the SuperOptiX project's reference implementations for GEPA, DSPy, and MCP tool optimization.

## Documents

### 1. [GEPA_DSPy_MCP_Analysis.md](./GEPA_DSPy_MCP_Analysis.md)
**Comprehensive reference architecture analysis** (20KB)

Complete technical overview including:
- Full directory structure of reference materials
- Detailed component analysis (GEPA, DSPy, MCP)
- Architecture patterns and design
- Integration points and extension strategies
- Implementation status matrix
- What's built vs. what needs building

**Best for**: Understanding the overall architecture and what's available

---

### 2. [MCP_Integration_Summary.md](./MCP_Integration_Summary.md)
**Practical MCP integration guide** (10KB)

Focused guide to MCPAdapter including:
- What the MCPAdapter does
- Complete working example
- Transport options (local, remote)
- Multi-tool support
- Error handling
- Integration roadmap for SuperOptiX
- Quick status matrix

**Best for**: Getting started with MCP tool optimization

---

## Quick Navigation

### I want to...

**Understand the architecture**
→ Read [GEPA_DSPy_MCP_Analysis.md](./GEPA_DSPy_MCP_Analysis.md)

**Integrate MCP into SuperOptiX**
→ Read [MCP_Integration_Summary.md](./MCP_Integration_Summary.md)

**Run an MCP optimization example**
→ See `/reference/gepa/src/gepa/examples/mcp_tool_optimization/`

**Explore the MCPAdapter code**
→ `/reference/gepa/src/gepa/adapters/mcp_adapter/mcp_adapter.py` (628 lines)

**Understand GEPA framework**
→ `/reference/gepa/src/gepa/core/adapter.py` for protocol definition

**See optimizer implementations**
→ `/reference/dspy/dspy/teleprompt/` for 10+ optimizers

**Check SuperOptiX optimizer factory**
→ `/superoptix/core/optimizer_factory.py` (826 lines)

---

## Key Paths

### Reference Implementations
```
/reference/gepa/                                    # GEPA framework
  └─ src/gepa/adapters/mcp_adapter/                # MCPAdapter (628 lines)
     ├─ mcp_adapter.py                             # Main implementation
     ├─ mcp_types.py                               # Type definitions
     ├─ simple_stdio_client.py                      # Local client
     ├─ sse_client.py                               # Remote SSE
     └─ streamable_http_client.py                   # Production HTTP

/reference/gepa/src/gepa/examples/
  └─ mcp_tool_optimization/                        # Examples
     ├─ local_ollama.py                            # Local (free)
     ├─ cloud_api.py                                # OpenAI
     ├─ remote_server.py                            # Remote MCP
     ├─ simple_mcp_server.py                        # Example server
     └─ README.md                                   # Complete guide

/reference/dspy/dspy/
  ├─ teleprompt/                                    # Optimizers
  ├─ utils/mcp.py                                   # MCP utilities
  └─ docs/learn/programming/mcp.md                 # MCP guide
```

### SuperOptiX Implementation
```
/superoptix/core/
  ├─ optimizer_factory.py                          # Optimizer registry
  └─ pipeline_utils.py                             # Pipeline integration

/superoptix/agents/dspy_optimizers/                # Demo playbooks
  ├─ gepa_playbook.yaml
  ├─ simba_playbook.yaml
  ├─ copro_playbook.yaml
  └─ ... (20+ examples)
```

---

## Current Status

| Component | Status | Notes |
|-----------|--------|-------|
| GEPA Core | Complete | Optimization engine ready |
| MCPAdapter | Complete | Full implementation with tests |
| DSPy Integration | Complete | MCP utilities & 10+ optimizers |
| Examples | Complete | Local, cloud, remote working |
| SuperOptiX Integration | **In Progress** | Wrapper needed |

---

## Implementation Checklist

### Phase 1: Reference Understanding ✓
- [x] Analyze GEPA architecture
- [x] Study MCPAdapter implementation
- [x] Review DSPy integration
- [x] Document examples

### Phase 2: SuperOptiX Integration (Next)
- [ ] Create MCPToolOptimizer wrapper class
- [ ] Add MCP playbook schema support
- [ ] Integrate with optimizer_factory
- [ ] Add CLI command `super agent optimize --mcp`

### Phase 3: Enhancement (Future)
- [ ] Caching layer for MCP calls
- [ ] Tool argument optimization
- [ ] Multi-tool routing optimization
- [ ] A/B testing framework

---

## Quick Start

### Run Local MCP Optimization (Free)
```bash
# 1. Install Ollama and required packages
pip install mcp gepa litellm

# 2. Start Ollama (separate terminal)
ollama serve

# 3. Pull models
ollama pull llama:3.2:1b
ollama pull llama:3.1:8b

# 4. Run example
cd /reference/gepa/src/gepa/examples/mcp_tool_optimization
python local_ollama.py
```

### Run Cloud MCP Optimization (OpenAI)
```bash
export OPENAI_API_KEY=your-key-here
python cloud_api.py
```

---

## Questions to Ask

**Q: How do I optimize MCP tools?**
A: Use MCPAdapter with GEPA. See [MCP_Integration_Summary.md](./MCP_Integration_Summary.md)

**Q: What's the difference between GEPA, DSPy, and MCP?**
A: See "Architecture Overview" in [GEPA_DSPy_MCP_Analysis.md](./GEPA_DSPy_MCP_Analysis.md)

**Q: How do I integrate this into SuperOptiX?**
A: Follow "Integration Points" in [GEPA_DSPy_MCP_Analysis.md](./GEPA_DSPy_MCP_Analysis.md)

**Q: Can I optimize multiple tools at once?**
A: Yes! MCPAdapter supports multi-tool optimization. See [MCP_Integration_Summary.md](./MCP_Integration_Summary.md)

**Q: What transports are supported?**
A: Local Stdio, Remote SSE, Remote StreamableHTTP. See [MCP_Integration_Summary.md](./MCP_Integration_Summary.md)

---

## References

**External Documentation**:
- [GEPA GitHub](https://github.com/gepa-ai/gepa)
- [DSPy GitHub](https://github.com/stanfordnlp/dspy)
- [MCP Specification](https://modelcontextprotocol.io/)
- [GEPA Paper](https://arxiv.org/abs/2507.19457)

**Internal Documentation**:
- [CLAUDE.md](../../CLAUDE.md) - Project development guide
- [README.md](../../README.md) - Project overview

---

*Documentation updated: 2025-10-18*
*Working directory: /Users/shashi/superagentic/SuperOptiX*
