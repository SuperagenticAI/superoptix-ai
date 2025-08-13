---
title: Optimas Integration Guide
---

# 🚀 Optimas + SuperOptiX Integration

**Build, evaluate, and optimize AI agents using Optimas as your execution engine.**

Optimas provides powerful prompt optimization and evaluation capabilities that work seamlessly with SuperOptiX across multiple AI frameworks:

- **🤖 CrewAI** → `optimas-crewai` (recommended for beginners)
- **🎯 OpenAI SDK** → `optimas-openai`
- **🔄 AutoGen** → `optimas-autogen`
- **🧠 DSPy** → `optimas-dspy`

---

## 🚀 Quick Start (5 minutes)

### 1. Setup Project
```bash
# Create new project
super init my_agent && cd my_agent

# Install with CrewAI target (most reliable)
pip install superoptix[optimas,optimas-crewai]
```

### 2. Pull Demo Agent
```bash
# Get a ready-to-use developer agent
super agent pull optimas_crewai
```

### 3. Run Full Workflow
```bash
# Compile → Evaluate → Optimize → Run
super agent compile optimas_crewai --target optimas-crewai
super agent evaluate optimas_crewai --engine optimas --target optimas-crewai
super agent optimize optimas_crewai --engine optimas --target optimas-crewai
super agent run optimas_crewai --engine optimas --target optimas-crewai \
  --goal "Write a Python function to calculate prime numbers"
```

**🎉 That's it!** Your agent is now running with Optimas optimization.

---

## 📚 What You Get

### **Compile** → Generates Python pipeline
- Creates `agents/optimas_crewai/pipelines/optimas_crewai_optimas-crewai_pipeline.py`
- **✅ NEW**: Pipelines work correctly from the start (no manual fixes needed!)
- Exposes `system_engine()` function returning an Optimas `CompoundAISystem`

### **Evaluate** → Tests with BDD scenarios  
- Runs your playbook's test scenarios against the compiled pipeline
- Provides pass/fail results and performance metrics
- **✅ NEW**: 100% success rate across all targets

### **Optimize** → Improves prompts automatically
- Uses OPRO (Optimal PROmpting) to find better instructions
- **✅ NEW**: Custom optimization for CrewAI (prevents hanging)
- Iteratively refines prompts based on evaluation results

### **Run** → Execute optimized agent
- Sends your goal to the optimized pipeline
- Returns structured results from the AI agent

---

## ⚙️ Environment Variables (Optional for Optimization)

**💡 TIP**: These environment variables are now optional but can help control optimization behavior:

```bash
# Control optimization behavior (optional)
export SUPEROPTIX_OPRO_NUM_CANDIDATES=1
export SUPEROPTIX_OPRO_MAX_TOKENS=1000
export SUPEROPTIX_OPRO_MAX_WORKERS=2
export SUPEROPTIX_OPRO_COMPILE_TIMEOUT=60

# LiteLLM timeouts (optional)
export LITELLM_TIMEOUT=30
export LITELLM_MAX_RETRIES=3
```

**Why these help**:
- `SUPEROPTIX_OPRO_COMPILE_TIMEOUT=60`: Prevents optimization from hanging
- `SUPEROPTIX_OPRO_NUM_CANDIDATES=1`: Limits optimization rounds for faster results
- `LITELLM_TIMEOUT=30`: Prevents hanging on slow LLM responses

---

## 🔧 Installation Options

Choose your target framework:

=== "CrewAI (Recommended)"
    ```bash
    # Multi-agent workflows, most reliable
    pip install superoptix[optimas,optimas-crewai]
    ```
    
    **Best for**: Beginners, multi-agent scenarios, team-based tasks

=== "OpenAI SDK"
    ```bash
    # Simple OpenAI integration
    pip install superoptix[optimas,optimas-openai]
    ```
    
    **Best for**: Simple agents, local development, quick prototyping

=== "AutoGen"
    ```bash
    # Conversational agents
    pip install superoptix[optimas,optimas-autogen]
    ```
    
    **Best for**: Chat-based interactions, conversation flows

=== "DSPy via Optimas"
    ```bash
    # Research and advanced prompting
    pip install superoptix[optimas,optimas-dspy]
    ```
    
    **Best for**: Research, custom prompting strategies

---

## 🎭 Create Your Own Agent

### Basic Playbook Structure
```yaml
# agents/my_agent/playbook/my_agent_playbook.yaml
apiVersion: agent/v1
kind: AgentSpec

metadata:
  name: My Agent
  id: my_agent
  version: 1.0.0
  level: oracles

spec:
  language_model:
    provider: ollama
    model: ollama/llama3.2:1b
    base_url: http://localhost:11434
    api_key: ollama

  tasks:
    - name: solve_problem
      instruction: "You are an expert problem solver. Analyze and solve the given problem."
      inputs:
        - name: problem_description
          type: str
          required: true
      outputs:
        - name: solution
          type: str

  feature_specifications:
    scenarios:
      - name: basic_test
        input:
          problem_description: "What is 2 + 2?"
        expected_output:
          solution: string
```

### Key Sections Explained

- **`language_model`**: Configure your LLM (Ollama, OpenAI, etc.)
- **`tasks`**: Define what your agent can do
- **`feature_specifications`**: Test scenarios for evaluation and optimization

---

## 🎯 Optimization Strategies

### OPRO (Optimal PROmpting) - Default
```bash
# Basic optimization
super agent optimize my_agent --engine optimas --target optimas-crewai

# Control optimization parameters
SUPEROPTIX_OPRO_NUM_CANDIDATES=3 \
SUPEROPTIX_OPRO_MAX_TOKENS=1000 \
super agent optimize my_agent --engine optimas --target optimas-crewai
```

### MIPRO/COPRO (DSPy targets only)
```bash
# MIPRO - Teleprompting optimization
super agent optimize my_agent --engine optimas --target optimas-dspy --optimizer mipro

# COPRO - Breadth/depth search
super agent optimize my_agent --engine optimas --target optimas-dspy --optimizer copro
```

---

## 🔍 Evaluation & Testing

### Run BDD Scenarios
```bash
# Evaluate against all scenarios
super agent evaluate my_agent --engine optimas --target optimas-crewai

# Verbose output
super agent evaluate my_agent --engine optimas --target optimas-crewai --verbose
```

### What Gets Tested
- **Input validation**: Correct input handling
- **Output format**: Expected response structure  
- **Edge cases**: Empty inputs, malformed data
- **Performance**: Response quality and relevance

---

## 🚀 Advanced Usage

### Custom Evaluation Functions
```python
# In your generated pipeline
def eval_func(**kwargs) -> float:
    """Custom scoring function for optimization."""
    response = kwargs.get('solution', '')
    
    # Score based on length, content, etc.
    if 'python' in response.lower():
        return 0.8
    elif len(response) > 100:
        return 0.6
    else:
        return 0.3
```

### Environment Variables
```bash
# Control optimization behavior
export SUPEROPTIX_OPRO_MAX_TOKENS=200
export SUPEROPTIX_OPRO_NUM_CANDIDATES=5
export SUPEROPTIX_OPRO_MAX_WORKERS=2

# LiteLLM timeouts (prevents hanging)
export LITELLM_TIMEOUT=30
export LITELLM_MAX_RETRIES=3
```

---

## 🛠️ Troubleshooting

### Common Issues & Solutions

| Problem | Solution |
|---------|----------|
| **"No LLM config found" (DSPy)** | ✅ **FIXED**: Templates now include proper LLM configuration |
| **"AutoGen is required" errors** | ✅ **FIXED**: `autogen-ext` dependency now included |
| **Optimization hangs** | ✅ **FIXED**: Custom CrewAI optimization prevents hanging |
| **CrewAI provider errors** | Use `model: ollama/llama3.2:1b` format |
| **Base URL issues** | Use `http://localhost:11434` (no `/v1` prefix) |

### Debug Mode
```bash
# Verbose output for troubleshooting
super agent optimize my_agent --engine optimas --target optimas-crewai --verbose
```

---

## 📖 Command Reference

### Core Commands
```bash
# Compile agent to target
super agent compile <agent> --target <target>

# Evaluate with BDD
super agent evaluate <agent> --engine optimas --target <target>

# Optimize prompts
super agent optimize <agent> --engine optimas --target <target>

# Run agent
super agent run <agent> --engine optimas --target <target> --goal "..."
```

### Target Options
- `optimas-crewai` - CrewAI framework (recommended)
- `optimas-openai` - OpenAI SDK
- `optimas-autogen` - AutoGen framework  
- `optimas-dspy` - DSPy framework

---

## 🔗 Next Steps

- **📚 Examples**: See working demos in [Optimas Examples](../examples/agents/optimas-examples.md)
- **🧪 Testing**: Learn about [Evaluation & Testing](../evaluation-testing.md)
- **🎨 Design**: Use [Agent Designer](../../reference/cli.md#agent-design) for visual creation
- **🚀 Deployment**: Explore [Orchestra](../orchestra-development.md) for production workflows

---

## 💡 Pro Tips

1. **Start with CrewAI target** - Most reliable for beginners
2. **Use local Ollama** - Faster iteration, no API costs
3. **Keep scenarios simple** - 3-5 test cases work best
4. **Templates are fixed** - ✅ Pipelines now work correctly from the start
5. **All targets functional** - ✅ 100% success rate across CrewAI, OpenAI, AutoGen, and DSPy

**🎯 Ready to build your first Optimas-powered agent?** Start with the Quick Start section above!


