---
title: Optimas Examples
---

# 🎯 Ready-to-Run Optimas Examples

**Copy-paste commands that actually work.** These examples use the demo agents from `superoptix/agents/optimas/` and show you exactly how to get started with each Optimas target.

---

## 🚀 Quick Demo (CrewAI Target)

**Start here if you're new to Optimas!**

```bash
# 1. Create project
super init demo_optimas && cd demo_optimas

# 2. Install CrewAI target (most reliable)
pip install superoptix[optimas,optimas-crewai]

# 3. Pull demo agent
super agent pull optimas_crewai

# 4. Run full workflow
super agent compile optimas_crewai --target optimas-crewai
super agent evaluate optimas_crewai --engine optimas --target optimas-crewai
super agent optimize optimas_crewai --engine optimas --target optimas-crewai
super agent run optimas_crewai --engine optimas --target optimas-crewai \
  --goal "Write a Python function to calculate prime numbers"
```

**🎉 Result**: You'll have a working, optimized developer agent that generates code!

---

## 📚 Available Demo Agents

| Agent | Target | Description | Best For | Status |
|-------|--------|-------------|----------|---------|
| `optimas_crewai` | `optimas-crewai` | CrewAI framework | **Beginners**, multi-agent workflows | ✅ **100% Working** |
| `optimas_openai` | `optimas-openai` | OpenAI SDK via Optimas | Simple agents, local development | ✅ **100% Working** |
| `optimas_autogen` | `optimas-autogen` | AutoGen framework | Conversational agents | ✅ **100% Working** |
| `optimas_dspy` | `optimas-dspy` | DSPy framework | Research, custom prompting | ✅ **100% Working** |

**🎯 All targets now have 100% success rate!** No more manual fixes needed.

---

## 🎯 Per-Target Examples

### 1. CrewAI Target (Recommended)

**What it does**: Integrates CrewAI agents with Optimas for team-based workflows.

```bash
# Install (separate to avoid DSPy conflicts)
pip install superoptix[optimas,optimas-crewai]

# Pull and setup
super agent pull optimas_crewai

# Full workflow (no environment variables needed!)
super agent compile optimas_crewai --target optimas-crewai
super agent evaluate optimas_crewai --engine optimas --target optimas-crewai
super agent optimize optimas_crewai --engine optimas --target optimas-crewai
super agent run optimas_crewai --engine optimas --target optimas-crewai \
  --goal "Design a software architecture for a web app"
```

**✅ Why it's great**: 
- Most reliable for beginners
- Works well with local Ollama
- Good for complex multi-step tasks
- **✅ NEW**: Custom optimization prevents hanging

---

### 2. OpenAI SDK Target

**What it does**: Wraps OpenAI SDK calls in Optimas for evaluation and optimization.

```bash
# Install
pip install superoptix[optimas,optimas-openai]

# Pull and setup
super agent pull optimas_openai

# Full workflow
super agent compile optimas_openai --target optimas-openai
super agent evaluate optimas_openai --engine optimas --target optimas-openai
super agent optimize optimas_openai --engine optimas --target optimas-openai
super agent run optimas_openai --engine optimas --target optimas-openai \
  --goal "Create a Python class for managing a shopping cart"
```

**✅ Why it's great**: 
- Simple and straightforward
- Fast optimization cycles
- Works with any Ollama model
- Good for quick prototyping

---

### 3. AutoGen Target

**What it does**: Wraps AutoGen conversational agents with Optimas optimization.

```bash
# Install (now includes autogen-ext dependency)
pip install superoptix[optimas,optimas-autogen]

# Pull and setup
super agent pull optimas_autogen

# Full workflow
super agent compile optimas_autogen --target optimas-autogen
super agent evaluate optimas_autogen --engine optimas --target optimas-autogen
super agent optimize optimas_autogen --engine optimas --target optimas-autogen
super agent run optimas_autogen --engine optimas --target optimas-autogen \
  --goal "Explain quantum computing in simple terms"
```

**✅ Why it's great**: 
- **✅ NEW**: `autogen-ext` dependency now included
- Good for chat-based interactions
- Stable optimization cycles
- Works reliably with Ollama

---

### 4. DSPy Target

**What it does**: Wraps DSPy components inside Optimas for research workflows.

```bash
# Install with DSPy target
pip install superoptix[optimas,optimas-dspy]

# Pull and setup
super agent pull optimas_dspy

# Full workflow
super agent compile optimas_dspy --target optimas-dspy
super agent evaluate optimas_dspy --engine optimas --target optimas-dspy
super agent optimize optimas_dspy --engine optimas --target optimas-dspy
super agent run optimas_dspy --engine optimas --target optimas-dspy \
  --goal "Generate a research hypothesis about AI safety"
```

**✅ Why it's great**: 
- **✅ NEW**: Templates now include proper LLM configuration
- Access to MIPRO/COPRO optimizers
- Research-grade prompting strategies
- No more "No LLM config found" errors

---

## 🔧 Customization Examples

### Change the Model

Edit your agent's playbook to use different models:

```yaml
# In agents/optimas_crewai/playbook/optimas_crewai_playbook.yaml
spec:
  language_model:
    provider: ollama
    model: ollama/llama3.1:8b  # Change to different model
    base_url: http://localhost:11434  # ✅ NEW: No /v1 prefix needed
    api_key: ollama
```

### Add More Test Scenarios

```yaml
# Add to feature_specifications.scenarios
- name: complex_algorithm
  input:
    feature_requirement: "Implement a binary search tree with insert, delete, and search operations"
  expected_output:
    implementation: string
- name: data_structures
  input:
    feature_requirement: "Create a priority queue using a min-heap"
  expected_output:
    implementation: string
```

### Custom Optimization Parameters

```bash
# Control optimization behavior (optional)
SUPEROPTIX_OPRO_NUM_CANDIDATES=3 \
SUPEROPTIX_OPRO_MAX_TOKENS=1000 \
SUPEROPTIX_OPRO_MAX_WORKERS=2 \
super agent optimize optimas_crewai --engine optimas --target optimas-crewai
```

---

## 🚨 Troubleshooting

### ✅ **Most Issues Are Now Fixed!**

| Issue | Status | Solution |
|-------|--------|----------|
| **"No LLM config found" (DSPy)** | ✅ **FIXED** | Templates now include proper LLM configuration |
| **"AutoGen is required" errors** | ✅ **FIXED** | `autogen-ext` dependency now included |
| **Optimization hangs** | ✅ **FIXED** | Custom CrewAI optimization prevents hanging |
| **Base URL issues** | ✅ **FIXED** | Use `http://localhost:11434` (no `/v1`) |

### Still Having Issues?

```bash
# Check if Ollama is running
ollama list

# Pull the model if needed
ollama pull llama3.2:1b

# Verify project setup
pwd  # Should show /path/to/your/project
ls -la .super  # Should show project config file
```

---

## 📊 What You'll See

### Successful Compilation
```
✅ Agent 'optimas_crewai' compiled successfully!
📁 Generated: agents/optimas_crewai/pipelines/optimas_crewai_optimas-crewai_pipeline.py
🚀 Ready for evaluation and optimization!
```

### Evaluation Results
```
🧪 Evaluating agent 'optimas_crewai' with 8 scenarios...
✅ basic_impl: PASSED
✅ edge_case_empty_input: PASSED  
✅ parse_numbers: PASSED
✅ string_ops: PASSED
✅ error_handling: PASSED
✅ data_structures: PASSED
✅ algorithms: PASSED
✅ file_operations: PASSED

🎉 All 8/8 scenarios passed!
```

### Optimization Progress
```
🚀 Optimizing agent 'optimas_crewai'...
📊 OPRO: Iteration 1/3
🔍 Evaluating candidate prompt...
📈 Score: 0.75 → 0.82
✅ Optimization complete! Best score: 0.82
```

---

## 🎯 Next Steps

1. **Try different goals** - Test with various programming tasks
2. **Experiment with models** - Test different Ollama models
3. **Customize scenarios** - Add your own test cases
4. **Build your own agent** - Create a custom playbook
5. **Explore other targets** - Try OpenAI, AutoGen, or DSPy

---

## 💡 Pro Tips

- **Start with CrewAI target** - Most reliable for learning
- **Use small models first** - Faster iteration during development
- **Keep scenarios focused** - Test one thing at a time
- **✅ Templates are fixed** - Pipelines now work correctly from the start
- **✅ All targets functional** - 100% success rate across all frameworks

**🎯 Ready to dive in?** Start with the Quick Demo above and then explore your favorite target!


