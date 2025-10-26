---
title: Quick Start - SuperOptiX
---

# 🚀 Quick Start Guide: Build a Software Development Team in 10 Minutes

## 🚀 Welcome to the Quick Start Guide!

Get ready to build a fully functional AI-powered software development team in just **10 minutes**!

No prior AI experience required - we'll guide you every step of the way.

## 🎯 What You'll Build in 10 Minutes

By the end of this guide, you'll have:

- ✅ A fully functional software development team (Developer, QA Engineer, DevOps Engineer)
- ✅ Automated optimization and evaluation
- ✅ Multi-agent orchestration
- ✅ Production-ready deployment specs

---

## 📋 Requirements

### 🖥️ Hardware Requirements

- **Minimum 16GB GPU RAM** for agent optimization (Step 5)
- **8GB+ system RAM** recommended
- **Stable internet connection** for model downloads and API calls

### 🐍 Software Requirements

- **Python 3.11 or higher**
- **SuperOptiX Python package** (install with pip, conda, or uv)
- **Ollama** (for local LLMs)

Install Ollama:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

_You can also use MLX or Huggingface for local models, but we'll use Ollama for this guide._

!!! warning "Windows Users - Important!"
    **On Windows, set PYTHONUTF8=1** to ensure proper UTF-8 encoding support:
    ```cmd
    set PYTHONUTF8=1
    ```
    Or add it to your system environment variables for permanent setting.

---

## 🛠️ Installation Options

!!! info "Stable Release"
    SuperOptiX 0.2.0 is now stable! No pre-release flags needed.

!!! success "Batteries Included"
    SuperOptiX now includes **DSPy, GEPA, and MCP client** by default!
    
    - **DSPy** - Framework for GEPA optimization
    - **GEPA** - Graph-Enhanced Prompting Algorithm for memory optimization
    - **MCP Client** - Model Context Protocol for tool usage and knowledge access
    - **Super CLI** - Conversational AI-powered command-line interface

Choose your preferred method:

=== "🚀 Recommended: Simple Install"

    ```bash
    # Install SuperOptiX (includes DSPy, GEPA, MCP by default)
    pip install superoptix
    
    # Verify installation
    super --version
    
    # Start conversational CLI
    super
    
    # Get comprehensive documentation
    super docs
    ```
    
    **✅ Everything works out of the box!**

=== "⚡ Fast: uv"

    ```bash
    # Install uv (if not already installed)
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix
    
    # Verify installation
    super --version
    
    # Start conversational CLI
    super
    ```
    
    **💡 Note:** The first execution of `super` commands may take a few seconds as Python compiles bytecodes.

=== "🎯 All Optional Features"

    ```bash
    # Install with all optional frameworks and features
    pip install superoptix[all]
    
    # This adds (on top of defaults):
    # - Additional frameworks (OpenAI, Google, Microsoft, DeepAgents)
    # - Vector databases (ChromaDB, Qdrant, Milvus, etc.)
    # - UI components (Streamlit, Plotly)
    # - Observability (MLflow, Langfuse)
    
    # Verify installation
    super --version
    ```
    
    **Note:** DSPy, GEPA, and MCP are already included in the base install!

### Add Additional Frameworks (Optional)

!!! tip "DSPy Already Included"
    You don't need to install DSPy separately - it comes with the base install!

=== "🤖 OpenAI Agents SDK"

    ```bash
    pip install superoptix[frameworks-openai]
    ```
    
    **Adds:** OpenAI Agents SDK 0.4.1

=== "🔮 Google ADK"

    ```bash
    pip install superoptix[frameworks-google]
    
    # Set API key
    export GOOGLE_API_KEY=your-google-api-key
    ```
    
    **Adds:** Google ADK 1.17.0

=== "🏢 Microsoft"

    ```bash
    pip install superoptix[frameworks-microsoft]
    ```
    
    **Includes:** agent-framework (latest)

=== "🌊 DeepAgents"

    ```bash
    pip install superoptix[frameworks-deepagents]
    ```
    
    **Includes:** deepagents (latest)

=== "👥 CrewAI"

    ```bash
    pip install superoptix[frameworks-crewai]
    ```
    
    **Includes:** crewai 1.2.0
    
    ⚠️ **Cannot be installed with DSPy** (dependency conflict)

---

## 🔧 Optional Dependencies

SuperOptiX supports various optional dependencies for enhanced functionality. Install them based on your needs:

=== "🤖 Local Model Management"

    **MLX (Apple Silicon)**
    
    ```bash
    pip install superoptix[mlx]
    ```
    - `mlx-lm==0.26.3` - Apple MLX framework for local inference
    
    **HuggingFace**
    
    ```bash
    pip install superoptix[huggingface]
    ```
    - `transformers==4.46.1` - HuggingFace transformers library
    - `torch==2.7.1` - PyTorch for model inference
    - `fastapi==0.116.1` - Web framework for model serving
    - `huggingface-hub>=0.34.0` - Model hub integration

=== "🗄️ Vector Databases"

    ```bash
    # ChromaDB (lightweight, in-memory)
    pip install superoptix[chromadb]
    
    # LanceDB (high-performance, disk-based)
    pip install superoptix[lancedb]
    
    # All vector databases (ChromaDB, LanceDB, Weaviate, Qdrant, Milvus)
    pip install superoptix[vectordb]
    ```

=== "📊 Observability & UI"

    ```bash
    # MLflow tracking
    pip install superoptix[mlflow]
    
    # Streamlit UI
    pip install superoptix[ui]
    
    # All observability tools (MLflow, LangFuse, Weights & Biases)
    pip install superoptix[observability]
    ```

---

## 🤖 Step 0: Install AI Models (Optional but Recommended)

For the best experience with local LLMs, install Ollama models:

```bash
# Install a powerful model for orchestration (recommended)
ollama pull llama3.1:8b

# Or install a smaller, faster model
ollama pull llama3.2:3b

# Verify installation
ollama list
```

**Model Recommendations:**
- **llama3.1:8b** - Best balance of quality and speed (recommended)
- **llama3.2:3b** - Faster, good for development
- **qwen2.5:14b** - Best quality, slower

---

## 🛠️ Step 1: Initialize Your SWE Project

```bash
super init swe
cd swe
```

This creates your project structure:

```
swe/
├── agents/       # Agent playbooks and specifications
├── evals/        # Evaluation datasets and results
├── guardrails/   # Safety and validation rules
├── knowledge/    # RAG knowledge bases
├── memory/       # Agent memory systems
├── optimizers/   # GEPA optimization results
├── orchestras/   # Multi-agent orchestra configs
├── pipelines/    # Compiled agent code
├── protocols/    # MCP protocol configurations
├── servers/      # API server configurations
├── teams/        # Team configurations
├── tools/        # Custom tools
└── .super        # Project marker file
```

---

## 🤖 Step 2: Pull a Developer Agent

```bash
super agent pull developer
```

This downloads a pre-built developer agent playbook to `agents/developer_playbook.yaml`.

<details><summary>📋 Understanding the Playbook Structure</summary>

The playbook defines everything about your agent using SuperSpec DSL:

```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: developer
  id: developer
  namespace: software
  version: 1.0.0
  level: oracles
  description: Software developer agent that implements features and writes code
spec:
  target_framework: dspy
  language_model:
    provider: ollama
    model: llama3.1:8b
    api_base: http://localhost:11434
  persona:
    role: Software Developer
    goal: Implement high-quality, well-documented code solutions
    backstory: |
      You are an experienced software developer with expertise in multiple
      programming languages and frameworks. You write clean, maintainable code
      following best practices and design patterns.
    reasoning:
      steps:
        - Understand the feature requirements
        - Design the implementation approach
        - Write clean, tested code
        - Document the solution
  input_fields:
    - name: feature
      type: text
      description: Feature description to implement
  output_fields:
    - name: implementation
      type: text
      description: Complete code implementation
  feature_specifications:
    scenarios:
      - name: Implement REST endpoint
        input:
          feature: "Create a user registration endpoint"
        expected_output:
          implementation: "Complete working code"
      - name: Fix bug
        input:
          feature: "Fix authentication bug in login"
        expected_output:
          implementation: "Bug fix with explanation"
```

### 🔧 Key SuperSpec Components:

- **metadata**: Agent identity, tier, version
- **language_model**: Which LLM to use (Ollama, OpenAI, etc.)
- **persona**: Role, goal, backstory (optimizable by GEPA!)
- **reasoning**: Step-by-step thinking process
- **input_fields**: What the agent accepts
- **output_fields**: What the agent returns
- **feature_specifications**: RSpec-style BDD test scenarios for evaluation

</details>

---

## ⚙️ Step 3: Compile the Agent

```bash
super agent compile developer
```

This generates executable Python code in `pipelines/developer_pipeline.py`.

**What happens:**
- Jinja2 templates render framework-specific code
- Agent persona is extracted as the optimizable variable
- RSpec-style BDD scenarios are converted to DSPy evaluation examples
- Ready-to-run Python pipeline is created

---

## 🧪 Step 4: Evaluate the Agent

```bash
super agent evaluate developer
```

This tests the agent against RSpec-style BDD scenarios to establish baseline performance.

<details><summary>🧪 Understanding Evaluation Results</summary>

#### 📋 How RSpec-Style BDD Specs Become DSPy Gold Examples

SuperOptiX converts your RSpec-style BDD scenarios into DSPy evaluation examples:

```python
# RSpec-Style BDD Scenario (YAML)
- name: Implement REST endpoint
  input:
    feature: "User login endpoint"
  expected_output:
    implementation: "Complete implementation"

# Becomes DSPy Example
Example(
    feature="User login endpoint",
    implementation="Complete implementation"
).with_inputs("feature")
```

#### 🔍 Why Scores Are Low

Initial scores of 37.5%-66% are **normal and expected**:
- Agents start with generic prompts
- Not yet optimized for specific scenarios
- This is why we optimize!

#### ⚠️ Note on Model Pass Rates

Different models have different baseline capabilities:
- **GPT-4**: 60-80% baseline
- **Llama 3.1:8b**: 40-60% baseline
- **Llama 3.2:3b**: 30-50% baseline

**After GEPA optimization:** All models improve 20-40%!

</details>

---

## 🎯 Step 5: Optimize the Agent

```bash
super agent optimize developer --auto medium
```

GEPA automatically improves the agent's instructions through evolutionary optimization!

**What happens during optimization:**

1. **Analysis** - GEPA analyzes failed scenarios
2. **Mutation** - Generates improved prompt variations using reflection
3. **Evaluation** - Tests each variation against RSpec-style BDD scenarios
4. **Selection** - Keeps best-performing prompts
5. **Iteration** - Repeats until convergence

**Optimization Levels:**
- `--auto light` - 3-5 iterations, faster (5-10 min)
- `--auto medium` - 10-15 iterations, balanced (15-25 min)
- `--auto intensive` - 20-30 iterations, thorough (30-60 min)

**Pro Tip:** Add `--fresh` flag to clear the cache and see real optimization progress (great for demos!):
```bash
super agent optimize developer --auto light --fresh
```

---

## 🧪 Step 6: Re-Evaluate the Agent (After Optimization)

```bash
super agent evaluate developer --load-optimized
```

This loads the optimized agent and re-evaluates to measure improvement.

You'll typically see **25-40% improvement** in pass rates!

---

## ▶️ Step 7: Run the Agent Independently

```bash
super agent run developer --goal "Implement a user registration API endpoint with email validation"
```

Test your optimized agent on a real-world task!

---

## ➕ Step 8: Add More Agents (QA & DevOps)

```bash
# Pull QA engineer
super agent pull qa_engineer

# Pull DevOps engineer
super agent pull devops_engineer

# Compile both agents
super agent compile qa_engineer
super agent compile devops_engineer
```

Now you have a complete 3-agent team ready for orchestration!

**💡 Tip:** You can optimize these agents too using steps 4-6, but for this quick start, we'll use them as-is for the orchestra.

---

## 🎼 Step 9: Create and Run a Multi-Agent Orchestra

### Create the Orchestra

```bash
super orchestra create sdlc
```

This auto-detects your agents and creates an orchestra configuration in `orchestras/sdlc_orchestra.yaml`.

### List Available Orchestras

```bash
super orchestra list
```

Shows all orchestras in your project.

### Run the Orchestra

```bash
super orchestra run sdlc --goal "Build a complete web application for a task management system with user authentication, CRUD operations, and real-time notifications. Include comprehensive testing and deployment configuration."
```

**What Just Happened:**

1. **Developer** analyzed the goal and provided implementation reasoning
2. **DevOps Engineer** created a CI/CD pipeline configuration based on the developer's output
3. **QA Engineer** created a comprehensive test plan based on both previous outputs

The orchestra automatically:

- ✅ Coordinated agent communication
- ✅ Passed context between tasks
- ✅ Generated artifacts in the workspace
- ✅ Completed the full SDLC workflow

**Generated artifacts:**

- `implement_feature_implementation.txt` - Developer's implementation
- `configure_ci_pipeline_result.json` - DevOps pipeline configuration
- `create_test_plan_test_plan.txt` - QA test plan

---

## 🔎 Step 10: Observe and Monitor Agent Traces

After running your orchestra, you can observe and monitor agent traces for deeper insights and debugging:

```bash
super observe traces developer
```

You can also launch the observability dashboard for a visual experience:

```bash
super observe dashboard
```

Explore more observability and monitoring commands:

```bash
super observe -h
```

This lets you inspect agent traces, view execution history, and monitor performance in real time.

---

## 🎉 Congratulations! You've Built Your First AI Development Team!

**🎉 Congratulations!** You just:

- ✅ Built a complete AI-powered software development team
- ✅ Automatically optimized your developer agent with GEPA
- ✅ Validated agents with real-world RSpec-style BDD scenarios
- ✅ Orchestrated them for production workflows
- ✅ Generated production-ready artifacts

## 🧭 Next: Build More Powerful Agents (Genies Tier)

You just built Oracles-tier agents, which do not use tools. To build more advanced agents with custom tools and RAG pipelines, try:

```bash
super agent pull scrum_master --tier genies
```

This will pull a Genies-tier agent, allowing you to configure tools and retrieval-augmented generation for more complex workflows!

Or browse other agents and tools:

```bash
# Browse available agents
super market browse agents

# Browse DSPy ReAct tools
super market browse tools
```

### 🎭 The Kubernetes Moment - Multi-Agent Orchestration

**🎉 The Kubernetes moment!** SuperOptiX just orchestrated your agents like a container orchestration platform:

- 🎭 **Orchestrated multiple agents automatically** - Just like Kubernetes manages containers
- 🔄 **Managed agent communication** - Seamless data flow between developer, DevOps, and QA
- 📊 **Coordinated responses** - Each agent built on the previous one's output
- 🚀 **Scaled based on demand** - Ready to handle complex workflows
- 📋 **Generated production artifacts** - Implementation, CI/CD config, and test plans

This is revolutionary! No other framework provides this level of automated multi-agent coordination with real-world validation.

---

## 🧪 Understanding the Evaluation-First Process

SuperOptiX follows **RSpec-Style BDD (Behavior-Driven Development)** principles, putting evaluation at the core of AI agent development:

### The SuperOptiX Workflow

```mermaid
graph LR
    A[super init] --> B[super agent pull]
    B --> C[super agent compile]
    C --> D[super agent evaluate]
    D --> E[super agent optimize]
    E --> F[super agent evaluate]
    F --> G[super agent run]
    G --> H[super orchestra create]
    H --> I[super orchestra run]
```

### Why Evaluation-First for AI?

- ✅ **Test-Driven Development**: Define success criteria before building
- ✅ **Real-world validation**: Test with actual scenarios
- ✅ **Data-driven optimization**: Improve based on evaluation results
- ✅ **Quality assurance**: Ensure production readiness
- ✅ **Continuous improvement**: Iterative development cycle
- ✅ **Documentation**: Scenarios serve as living documentation

---

## 🎯 Next Steps

### For Beginners

1. **Explore the marketplace**: `super market browse agents`
2. **Try different agents**: Pull and experiment with various agent types
3. **Experiment with tiers**: Start with oracles, move to genies

```bash
super agent pull developer --tier genies
```

### For Intermediate Users

1. **Create custom agents**: Use `super spec generate`
2. **Build orchestras**: Create multi-agent workflows
3. **Enable observability**: Monitor agent performance

### For Advanced Users

1. **Design complex systems**: Multi-agent organizations
2. **Custom tool development**: Extend the framework
3. **Production deployment**: Kubernetes integration

---

## 🆘 Getting Help

### Documentation

```bash
# Comprehensive documentation
super docs
```

### Resources

- **Website**: [superoptix.ai](https://superoptix.ai)
- **GitHub**: [@SuperagenticAI/superoptix-ai](https://github.com/SuperagenticAI/superoptix-ai)
- **PyPI**: [superoptix](https://pypi.org/project/superoptix/)

### Quick Commands

```bash
# List all available commands
super --help

# Get help for specific commands
super agent --help
super orchestra --help
super spec --help
super market --help
```

---

## 🔍 Verbose Mode: Get Detailed Information

SuperOptiX commands support a `--verbose` flag that provides detailed guidance, explanations, and recommendations. This is perfect for learning and debugging.

### Commands with Verbose Mode

**Agent Management:**

```bash
# Compile with detailed guidance
super agent compile developer --verbose

# Evaluate with detailed test results
super agent evaluate developer --verbose

# Optimize with detailed information
super agent optimize developer --verbose

# Run with detailed execution info
super agent run developer --goal "your goal" --verbose
```

**Orchestra Management:**

```bash
# Create with detailed configuration
super orchestra create my_orchestra --verbose

# Run with detailed execution info
super orchestra run my_orchestra --goal "your goal" --verbose
```

### What You Get in Verbose Mode

- 📋 **Detailed explanations** of what each step does
- 🎯 **AI recommendations** for improvement
- 📊 **Comprehensive test results** and analysis
- 🔧 **Configuration guidance** and best practices
- 🚀 **Next steps** and workflow recommendations
- 💡 **Troubleshooting tips** and common solutions

### When to Use Verbose Mode

- 🆕 **Learning SuperOptiX** - Understand what's happening under the hood
- 🐛 **Debugging issues** - Get detailed error information and suggestions
- 📈 **Optimizing performance** - See detailed metrics and recommendations
- 🎯 **Production planning** - Get comprehensive guidance for deployment

---

## 🎉 Welcome to SuperOptiX!

You've just taken your first steps into the future of AI agent development.

Ready to build something amazing?

<div align="center" style="margin: 30px 0;">
  <a href="tutorials/genies-agent/" style="background: #4CAF50; color: white; padding: 12px 24px; text-decoration: none; border-radius: 4px; margin: 5px; display: inline-block; font-weight: bold;">🚀 Build Your First Genies Agent</a>
  <a href="guides/marketplace/" style="background: #2196F3; color: white; padding: 12px 24px; text-decoration: none; border-radius: 4px; margin: 5px; display: inline-block; font-weight: bold;">🏪 Explore the Marketplace</a>
  <a href="guides/superspec/" style="background: #9C27B0; color: white; padding: 12px 24px; text-decoration: none; border-radius: 4px; margin: 5px; display: inline-block; font-weight: bold;">💎 Learn SuperSpec DSL</a>
</div>

_**Happy building!** 🚀_
