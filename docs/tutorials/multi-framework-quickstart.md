---
title: Multi-Framework Quick Start - SuperOptiX
---

# Multi-Framework Quick Start

Build and optimize AI agents across **6 major frameworks** in **10 minutes**.

## What You'll Build

By the end of this guide, you'll have:

- ✅ A fully functional AI agent in your chosen framework
- ✅ Automated evaluation with RSpec-style BDD scenarios
- ✅ GEPA optimization with proven improvements
- ✅ Production-ready agent deployment

## Requirements

### Hardware

- **Minimum**: 16GB GPU RAM for optimization
- **Recommended**: 8GB+ system RAM
- **Network**: Stable internet connection for model downloads

### Software

- **Python 3.11 or higher**
- **Ollama** (for local LLMs)

!!! warning "Windows Users"
    Set `PYTHONUTF8=1` to ensure proper UTF-8 encoding support:
    ```cmd
    set PYTHONUTF8=1
    ```
    
## Installation

!!! tip "Stable Release Available!"
    SuperOptiX is now available as a stable release.

!!! info "Git Required"
    Git is required for installation. Verify: `git --version`
    
    **Install Git:**
    
    - **macOS:** `xcode-select --install`
    - **Linux:** `sudo apt-get install git`
    - **Windows:** [Download Git](https://git-scm.com/downloads)

!!! tip "Framework-Free Core"
    SuperOptiX core is now **framework-independent**! Install only what you need.

Choose your framework(s) and install SuperOptiX:

=== "Core Only (Includes DSPy)"
    ```bash
    pip install superoptix
    ```
    **Includes:** CLI tools, SuperSpec DSL, YAML processing, DSPy
    
    **Use for:** GEPA optimization, DSPy pipelines, evaluation

=== "DSPy Framework"
    ```bash
    pip install superoptix[frameworks-dspy]
    ```
    **Includes:** SuperOptiX core + DSPy + GEPA
    
    ⚠️ **Cannot be installed with CrewAI** (json-repair conflict)

=== "OpenAI Agents SDK"
    ```bash
    pip install superoptix[frameworks-openai]
    ```
    **Includes:** openai-agents, openai SDK

=== "Google ADK"
    ```bash
    pip install superoptix[frameworks-google]
    ```
    **Includes:** google-adk, google-generativeai
    
    **Setup API Key:**
    ```bash
    export GOOGLE_API_KEY=your-google-api-key
    ```

=== "Microsoft Agent Framework"
    ```bash
    pip install superoptix[frameworks-microsoft]
    ```
    **Includes:** agent-framework, azure-identity

=== "DeepAgents"
    ```bash
    pip install superoptix[frameworks-deepagents]
    ```
    **Includes:** deepagents

=== "CrewAI"
    ```bash
    pip install superoptix[frameworks-crewai]
    ```
    **Includes:** crewai
    
    ⚠️ **Cannot be installed with DSPy** (json-repair conflict)

=== "All DSPy-Compatible Frameworks"
    ```bash
    pip install superoptix[frameworks]
    ```
    **Includes:** DSPy, OpenAI SDK, Google ADK, Microsoft, DeepAgents
    
    **Excludes:** CrewAI (due to DSPy conflict)

=== "With MCP Optimization"
    ```bash
    pip install superoptix[frameworks,mcp]
    ```
    **Includes:** DSPy-compatible frameworks + MCP SDK

=== "Everything (DSPy path)"
    ```bash
    pip install superoptix[all]
    ```
    **Includes:** DSPy + compatible frameworks + vector DBs + observability
    
    **Excludes:** CrewAI

!!! tip "First Execution"
    The first execution of `super` commands may take a few seconds as Python compiles bytecodes.

## Step 1: Initialize Project

```bash
# Create a new project
super init my_first_agent
cd my_first_agent
```

This creates a standard project structure:

```
my_first_agent/
├── agents/          # Agent playbooks
├── pipelines/       # Compiled agents
├── evals/          # Evaluation results
└── optimizers/     # Optimization data
```

## Step 2: Choose Your Framework and Pull an Agent

SuperOptiX supports 6 major frameworks. Choose the one that fits your needs:

=== "DSPy (Recommended)"

    ```bash
    # DSPy: Stanford research framework
    super agent pull sentiment_analyzer
    ```
    
    **Best for**: Complex reasoning, research, 10+ optimizable variables
    
    **Proven**: 37.5% → 80% improvement with GEPA

=== "OpenAI SDK"

    ```bash
    # OpenAI SDK: Simple and fast
    super agent pull assistant_openai
    ```
    
    **Best for**: Simple agents, fast prototyping
    
    **Proven**: 100% pass rate with GEPA

=== "CrewAI"

    ```bash
    # CrewAI: Multi-agent collaboration
    super agent pull researcher_crew
    ```
    
    **Best for**: Multi-agent teams, role-based agents
    
    **Proven**: 100% pass rate with GEPA

=== "Google ADK"

    ```bash
    # Google ADK: Gemini 2.0 native
    super agent pull assistant_adk
    ```
    
    **Best for**: Gemini integration, free tier available
    
    **Ready**: For optimization

=== "Microsoft"

    ```bash
    # Microsoft: Enterprise Azure
    super agent pull assistant_microsoft
    ```
    
    **Best for**: Enterprise Azure integration
    
    **Ready**: For optimization

=== "DeepAgents"

    ```bash
    # DeepAgents: Complex planning
    super agent pull research_agent_deepagents
    ```
    
    **Best for**: LangGraph planning, advanced reasoning
    
    **Ready**: For optimization

!!! tip "Browse All Agents"
    
    ```bash
    # See all pre-built agents
    super market browse agents
    
    # List demo agents
    super agent list --pre-built
    ```

## Step 3: Compile the Agent

```bash
# Compile for your chosen framework
super agent compile <agent_name>

# Example: DSPy
super agent compile sentiment_analyzer

# Example: OpenAI SDK
super agent compile assistant_openai
```

This generates framework-specific Python code in the `pipelines/` directory.

## Step 4: Evaluate Performance

```bash
# Run baseline evaluation
super agent evaluate <agent_name>

# Example
super agent evaluate sentiment_analyzer
```

You'll see results like:

```
Evaluation Results:
==================
Pass Rate: 37.5% (3/8 scenarios)
Average Score: 6.2/10
```

## Step 5: Optimize with GEPA

Now comes the magic! **GEPA (Genetic-Pareto)** automatically improves your agent's performance.

### The Universal Optimizer

- Works on **ALL 6 frameworks** (DSPy, OpenAI SDK, CrewAI, Google ADK, Microsoft, DeepAgents)
- Proven results: DSPy 37.5% → 80%, OpenAI/CrewAI 100% pass rates
- Sample efficient: Improves with just 3-10 scenarios
- Framework-agnostic: Same command for all frameworks!

```bash
# GEPA works on ALL frameworks! Same command!
super agent optimize <agent_name> --auto medium

# Examples:
super agent optimize sentiment_analyzer --auto medium        # DSPy
super agent optimize assistant_openai --auto medium          # OpenAI SDK
super agent optimize researcher_crew --auto medium           # CrewAI
super agent optimize assistant_adk --auto medium             # Google ADK
super agent optimize assistant_microsoft --auto medium       # Microsoft
super agent optimize research_agent_deepagents --auto medium # DeepAgents
```

### Optimization Levels

| Level | Time | Iterations | Best For |
|-------|------|------------|----------|
| `light` | ~5 min | 2-3 | Quick iteration, prototyping |
| `medium` | ~10-15 min | 5 | Most use cases (Recommended) |
| `intensive` | ~30+ min | 10+ | Critical production agents |

!!! warning "API Usage"
    Optimization makes multiple LLM API calls. Monitor your usage if using cloud models. Works great with Ollama (local, free)!

## Step 6: Re-evaluate to See Improvement

```bash
# Evaluate optimized version
super agent evaluate <agent_name> --load-optimized
```

You'll see dramatic improvements:

```
Evaluation Results (Optimized):
================================
Pass Rate: 80.0% (6.5/8 scenarios)  ← UP from 37.5%!
Average Score: 9.1/10                ← UP from 6.2/10!
Improvement: +42.5 percentage points
```

## Step 7: Run Your Optimized Agent

```bash
# Run the optimized agent
super agent run <agent_name>

# Example with custom input
super agent run sentiment_analyzer \
  --input "This product exceeded all my expectations!"
```

## Complete Example

Here's the full workflow for a DSPy sentiment analyzer:

```bash
# 1. Initialize
super init sentiment_project
cd sentiment_project

# 2. Pull agent
super agent pull sentiment_analyzer

# 3. Compile
super agent compile sentiment_analyzer

# 4. Baseline evaluation
super agent evaluate sentiment_analyzer
# Result: 37.5% pass rate

# 5. Optimize
super agent optimize sentiment_analyzer --auto medium
# GEPA optimizes agent with 5 iterations

# 6. Re-evaluate
super agent evaluate sentiment_analyzer --load-optimized
# Result: 80.0% pass rate (+42.5 points!)

# 7. Run
super agent run sentiment_analyzer
```

## What's Next?

Congratulations! You've just built, evaluated, and optimized your first AI agent with SuperOptiX.

### Learn More

- **[Multi-Framework Guide](../guides/multi-framework.md)** - Compare all 6 frameworks
- **[GEPA Optimization](../guides/gepa-optimization.md)** - Deep dive into optimization
- **[SuperSpec DSL](../guides/superspec.md)** - Build custom agents
- **[Evaluation & Testing](../guides/evaluation-testing.md)** - Advanced testing strategies

### Try Different Frameworks

```bash
# Try OpenAI SDK
super agent pull assistant_openai
super agent compile assistant_openai
super agent evaluate assistant_openai
super agent optimize assistant_openai --auto medium

# Try CrewAI
super agent pull researcher_crew
super agent compile researcher_crew
super agent evaluate researcher_crew
super agent optimize researcher_crew --auto medium
```

### Build Custom Agents

Create your own agent with SuperSpec:

```yaml
# my_agent_playbook.yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: my_custom_agent
spec:
  target_framework: dspy  # or openai, crewai, google-adk, microsoft, deepagents
  language_model:
    provider: ollama
    model: llama3.1:8b
  persona:
    role: Data Analyst
    goal: Analyze data and provide insights
  feature_specifications:
    scenarios:
      - name: Basic analysis
        input:
          data: "Sales data for Q1"
        expected_output:
          analysis: "Comprehensive analysis"
```

Then compile and optimize:

```bash
super agent compile my_custom_agent
super agent evaluate my_custom_agent
super agent optimize my_custom_agent --auto medium
```

## Troubleshooting

### Common Issues

!!! question "Installation fails"
    Try using `pip install superoptix[all]` or check Python version with `python --version` (must be 3.11+)

!!! question "Optimization fails"
    Check that you have at least 16GB GPU RAM and Ollama is running with `ollama list`

!!! question "No improvement after optimization"
    Ensure your RSpec-style BDD scenarios are well-defined and provide clear success criteria

### Get Help

- **Documentation**: [https://superoptix.ai/docs](https://superoptix.ai/docs)
- **GitHub Issues**: [https://github.com/SuperagenticAI/SuperOptiX/issues](https://github.com/SuperagenticAI/SuperOptiX/issues)
- **Website**: [https://superoptix.ai](https://superoptix.ai)

## Summary

You've learned how to:

1. ✅ Install SuperOptiX
2. ✅ Initialize a project
3. ✅ Choose from 6 frameworks
4. ✅ Compile agents
5. ✅ Evaluate performance
6. ✅ Optimize with GEPA
7. ✅ Deploy to production

**Ready to build more?** Check out our [Guides](../guides/index.md) for in-depth tutorials!

