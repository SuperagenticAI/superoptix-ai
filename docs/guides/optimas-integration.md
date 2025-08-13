---
title: Optimas Integration Guide
---

# ⚡ Optimas Integration Guide

SuperOptiX integrates seamlessly with the **Optimas** framework, enabling you to use advanced prompt optimization techniques (OPRO, MIPRO, COPRO) with multiple LLM frameworks including **OpenAI SDK**, **CrewAI**, **AutoGen**, and **DSPy**.

## 🚀 Quick Start

### 1. Install SuperOptiX with Optimas Support

```bash
# Install with Optimas support
pip install "superoptix[optimas]"

# For OpenAI SDK target (recommended - most reliable)
pip install "superoptix[optimas,optimas-openai]"

# For CrewAI target
pip install "superoptix[optimas,optimas-crewai]"

# For AutoGen target  
pip install "superoptix[optimas,optimas-autogen]"

# For DSPy target
pip install "superoptix[optimas,optimas-dspy]"
```

### 2. Install Additional Dependencies

```bash
# Required for DSPy 3.0.0 streaming support
pip install litellm

# For CrewAI (install manually to avoid conflicts)
pip install crewai
pip install json-repair>=0.30.0
```

### 3. Quick Demo

```bash
# Initialize project
super init test_optimas
cd test_optimas

# Pull demo agents
super agent pull optimas_openai      # OpenAI SDK (recommended)
super agent pull optimas_crewai      # CrewAI
super agent pull optimas_autogen     # AutoGen
super agent pull optimas_dspy        # DSPy

# Test compilation
super agent compile optimas_openai --target optimas-openai
super agent compile optimas_crewai --target optimas-crewai
super agent compile optimas_autogen --target optimas-autogen
super agent compile optimas_dspy --target optimas-dspy
```

## 📊 Target Compatibility Matrix

| Target | Compile | Evaluate | Optimize | Run | Status | Notes |
|--------|---------|----------|----------|-----|--------|-------|
| **OpenAI SDK** | ✅ | ✅ | ✅ | ✅ | **Fully Working** | Most reliable, no threading issues |
| **CrewAI** | ✅ | ✅ | ✅ | ✅ | **Fully Working** | Requires manual dependency installation |
| **AutoGen** | ✅ | ✅ | ⚠️ | ✅ | **Mostly Working** | Optimization works but can be slow |
| **DSPy** | ✅ | ✅ | ✅ | ✅ | **Fully Working** | All optimizers now working properly |

## 🔧 Environment Variables

### OPRO Optimization Variables

```bash
# Core OPRO settings
SUPEROPTIX_OPRO_MAX_TOKENS=256          # Max tokens per prompt
SUPEROPTIX_OPRO_NUM_CANDIDATES=3        # Number of prompt candidates
SUPEROPTIX_OPRO_MAX_WORKERS=3           # Max concurrent workers
SUPEROPTIX_OPRO_TEMPERATURE=0.8         # Creativity level (0.0-1.0)
SUPEROPTIX_OPRO_COMPILE_TIMEOUT=120     # Timeout in seconds
```

### MIPRO Optimization Variables

```bash
# MIPRO settings (for DSPy targets)
SUPEROPTIX_MIPRO_NUM_CANDIDATES=3       # Number of candidates
SUPEROPTIX_MIPRO_NUM_THREADS=3          # Number of threads
```

### COPRO Optimization Variables

```bash
# COPRO settings (for DSPy targets)
SUPEROPTIX_COPRO_BREADTH=3              # Search breadth
SUPEROPTIX_COPRO_DEPTH=3                # Search depth
```

### LiteLLM Configuration Variables

```bash
# LiteLLM settings (affects DSPy and CrewAI)
LITELLM_TIMEOUT=60                      # Request timeout
LITELLM_MAX_RETRIES=3                   # Max retry attempts
LITELLM_MAX_RESPONSE=4000               # Max response tokens
LITELLM_CACHE_ENABLED=false             # Disable caching
LITELLM_LOG_LEVEL=ERROR                 # Log level
```

## 🎯 Target-Specific Configuration

### OpenAI SDK Target (Recommended)

```yaml
# optimas_openai_playbook.yaml
name: optimas_openai
description: OpenAI SDK integration with Optimas
language_model:
  provider: ollama
  model: llama3.2:1b
  base_url: http://localhost:11434
  api_key: ""

components:
  - name: implement_feature
    type: optimas-openai
    description: "OpenAI component for implementing features"
    inputs:
      - name: feature_requirement
        type: string
        description: "Description of the feature to implement"
    outputs:
      - name: implementation
        type: string
        description: "The implemented feature code"
```

**✅ Why OpenAI SDK is recommended:**
- Most reliable and stable
- No threading issues
- Fast optimization and execution
- Works perfectly with all optimizers

### CrewAI Target

```yaml
# optimas_crewai_playbook.yaml
name: optimas_crewai
description: CrewAI integration with Optimas
language_model:
  provider: ollama
  model: llama3.2:1b
  base_url: http://localhost:11434
  api_key: ""

components:
  - name: implement_feature
    type: optimas-crewai
    description: "CrewAI agent for implementing features"
    inputs:
      - name: feature_requirement
        type: string
        description: "Description of the feature to implement"
    outputs:
      - name: implementation
        type: string
        description: "The implemented feature code"
```

**⚠️ CrewAI Dependencies:**
```bash
# Install manually to avoid conflicts
pip install crewai
pip install json-repair>=0.30.0
```

### AutoGen Target

```yaml
# optimas_autogen_playbook.yaml
name: optimas_autogen
description: AutoGen integration with Optimas
language_model:
  provider: ollama
  model: llama3.2:1b
  base_url: http://localhost:11434
  api_key: ""
  model_info:
    model_name: "llama3.2:1b"
    max_tokens: 4096
    temperature: 0.7
    top_p: 0.9

components:
  - name: implement_feature
    type: optimas-autogen
    description: "AutoGen agent for implementing features"
    inputs:
      - name: feature_requirement
        type: string
        description: "Description of the feature to implement"
    outputs:
      - name: implementation
        type: string
        description: "The implemented feature code"
```

**⚠️ AutoGen Notes:**
- Requires detailed `model_info` for non-OpenAI models
- Optimization can be slow but works reliably
- Best for complex multi-agent workflows

### DSPy Target

```yaml
# optimas_dspy_playbook.yaml
name: optimas_dspy
description: DSPy integration with Optimas
language_model:
  provider: ollama
  model: llama3.2:1b
  base_url: http://localhost:11434
  api_key: ""

components:
  - name: implement_feature
    type: optimas-dspy
    description: "DSPy module for implementing features"
    inputs:
      - name: feature_requirement
        type: string
        description: "Description of the feature to implement"
    outputs:
      - name: implementation
        type: string
        description: "The implemented feature code"
```

**✅ DSPy Features:**
- All optimizers (OPRO, MIPRO, COPRO) now working properly
- Excellent for research and production optimization
- Fast optimization and execution
- Great for prompt engineering workflows

## 🚀 Complete Workflow Examples

### OpenAI SDK Workflow (Recommended)

```bash
# 1. Compile
super agent compile optimas_openai --target optimas-openai

# 2. Evaluate
super agent evaluate optimas_openai --engine optimas --target optimas-openai

# 3. Optimize with environment variables
SUPEROPTIX_OPRO_MAX_TOKENS=256 \
SUPEROPTIX_OPRO_NUM_CANDIDATES=3 \
SUPEROPTIX_OPRO_MAX_WORKERS=3 \
SUPEROPTIX_OPRO_TEMPERATURE=0.8 \
super agent optimize optimas_openai --engine optimas --target optimas-openai

# 4. Run
super agent run optimas_openai --engine optimas --target optimas-openai --goal "Write a Python function to add two numbers"
```

### CrewAI Workflow

```bash
# 1. Compile
super agent compile optimas_crewai --target optimas-crewai

# 2. Evaluate
super agent evaluate optimas_crewai --engine optimas --target optimas-crewai

# 3. Optimize
SUPEROPTIX_OPRO_MAX_TOKENS=256 \
SUPEROPTIX_OPRO_NUM_CANDIDATES=3 \
SUPEROPTIX_OPRO_MAX_WORKERS=3 \
super agent optimize optimas_crewai --engine optimas --target optimas-crewai

# 4. Run
super agent run optimas_crewai --engine optimas --target optimas-crewai --goal "Write a Python function to calculate factorial"
```

### AutoGen Workflow

```bash
# 1. Compile
super agent compile optimas_autogen --target optimas-autogen

# 2. Evaluate
super agent evaluate optimas_autogen --engine optimas --target optimas-autogen

# 3. Optimize (can be slow)
SUPEROPTIX_OPRO_MAX_TOKENS=256 \
SUPEROPTIX_OPRO_NUM_CANDIDATES=3 \
SUPEROPTIX_OPRO_MAX_WORKERS=3 \
SUPEROPTIX_OPRO_COMPILE_TIMEOUT=180 \
super agent optimize optimas_autogen --engine optimas --target optimas-autogen

# 4. Run
super agent run optimas_autogen --engine optimas --target optimas-autogen --goal "Write a Python function to reverse a string"
```

### DSPy Workflow

```bash
# 1. Compile
super agent compile optimas_dspy --target optimas-dspy

# 2. Evaluate
super agent evaluate optimas_dspy --engine optimas --target optimas-dspy

# 3. Optimize
SUPEROPTIX_OPRO_MAX_TOKENS=256 \
SUPEROPTIX_OPRO_NUM_CANDIDATES=3 \
SUPEROPTIX_OPRO_MAX_WORKERS=3 \
SUPEROPTIX_OPRO_TEMPERATURE=0.8 \
super agent optimize optimas_dspy --engine optimas --target optimas-dspy

# 4. Run
super agent run optimas_dspy --engine optimas --target optimas-dspy --goal "Write a Python function to calculate fibonacci numbers"
```

## 🔍 Troubleshooting

### Common Issues

#### 1. DSPy Optimization Performance

**For Best Results:**
- Use appropriate optimization parameters for your use case
- Monitor optimization progress and adjust parameters as needed
- Consider using MIPRO or COPRO optimizers for specific DSPy workflows

#### 2. CrewAI Dependency Conflicts

**Symptoms:**
```
json-repair version conflicts
```

**Solutions:**
```bash
pip install crewai --no-deps
pip install json-repair>=0.30.0
```

#### 3. AutoGen Model Info Errors

**Symptoms:**
```
model_info is required when model name is not a valid OpenAI model
```

**Solutions:**
- Add detailed `model_info` section in playbook
- Use OpenAI-compatible model names

#### 4. Optimization Timeouts

**Symptoms:**
```
OPRO timed out after 120s on component
```

**Solutions:**
- Increase timeout: `SUPEROPTIX_OPRO_COMPILE_TIMEOUT=300`
- Reduce model size or token limits
- Use smaller optimization parameters

### Performance Optimization

#### For Fast Optimization:
```bash
SUPEROPTIX_OPRO_MAX_TOKENS=128
SUPEROPTIX_OPRO_NUM_CANDIDATES=2
SUPEROPTIX_OPRO_MAX_WORKERS=2
SUPEROPTIX_OPRO_TEMPERATURE=0.7
```

#### For High-Quality Optimization:
```bash
SUPEROPTIX_OPRO_MAX_TOKENS=512
SUPEROPTIX_OPRO_NUM_CANDIDATES=5
SUPEROPTIX_OPRO_MAX_WORKERS=4
SUPEROPTIX_OPRO_TEMPERATURE=0.9
SUPEROPTIX_OPRO_COMPILE_TIMEOUT=300
```

## 📚 Best Practices

### 1. Target Selection
- **Production**: Use OpenAI SDK target (most reliable)
- **Multi-agent**: Use CrewAI or AutoGen targets
- **Research & Optimization**: Use DSPy target (fully supported)

### 2. Environment Variables
- Set all relevant variables before running commands
- Use inline variable setting for reproducibility
- Monitor timeout values for large models

### 3. Model Configuration
- Use local models (Ollama) for development
- Ensure proper `model_info` for non-OpenAI models
- Test with smaller models first

### 4. Optimization Strategy
- Start with OPRO (most reliable)
- Use MIPRO/COPRO only with DSPy targets
- Monitor optimization progress and adjust parameters

## 🔗 Related Documentation

- [Optimas Examples](../examples/agents/optimas-examples.md) - Working examples for all targets
- [CLI Reference](../reference/cli.md) - Complete command reference
- [Agent Development](../guides/agent-development.md) - Building custom agents


