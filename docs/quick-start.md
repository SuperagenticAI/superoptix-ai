# 🚀 Quick Start Guide: Build a Software Development Team in 10 Minutes

<div style="text-align: center; margin: 2rem 0; padding: 2rem; background: var(--primary-gradient); border-radius: var(--border-radius); color: var(--text-primary); box-shadow: var(--shadow-heavy);">
    <h2 style="margin-bottom: 1rem; font-size: 2rem; background: var(--text-gradient); background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-weight: var(--font-weight-bold);">🚀 Welcome to the Quick Start Guide!</h2>
    <p style="font-size: 1.1rem; margin-bottom: 1.5rem; color: var(--text-secondary);">Get ready to build a fully functional AI-powered software development team in just <strong>10 minutes</strong>!</p>
    <p style="font-size: 1.2rem; margin-bottom: 2rem; font-weight: var(--font-weight-semibold); color: var(--text-primary);">No prior AI experience required - we'll guide you every step of the way.</p>
    
    <div style="display: flex; justify-content: center; gap: 1rem; flex-wrap: wrap; margin-top: 1.5rem;">
        <div style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            ⏱️ 10 Minutes
        </div>
        <div style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            🤖 3 AI Agents
        </div>
        <div style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            🎻 Multi-Agent Orchestra
        </div>
        <div style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            🎯 Production Ready
        </div>
    </div>
</div>

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
  - Install Ollama:  
    ```bash
    curl -fsSL https://ollama.com/install.sh | sh
    ```
  - _You can also use MLX or Huggingface for local models, but we'll use Ollama for this guide._

---

## 🛠️ Installation Options

Choose your preferred method:

=== "🚀 Recommended: uv (Fastest)"
    
    ```bash
    # Install uv (if not already installed)
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix
    
    # Verify installation
    super --help
    
    # Get comprehensive documentation
    super docs
    ```
    
    **💡 Note:** The first execution of `super` commands may take a few seconds as Python compiles bytecodes.

=== "🐍 Standard: pip"
    
    ```bash
    # Install SuperOptiX
    pip install superoptix
    
    # Verify installation
    super --help
    
    # Get comprehensive documentation
    super docs
    ```
    
    **💡 Note:** The first execution of `super` commands may take a few seconds as Python compiles bytecodes.

=== "🎯 All Features"
    
    ```bash
    # Install with all optional features
    pip install superoptix[all]
    
    # This includes:
    # - Vector databases (ChromaDB, LanceDB, etc.)
    # - UI components (Streamlit, Plotly)
    # - Observability (MLflow, monitoring)
    # - Cloud integrations (AWS, Azure, GCP)
    
    # Verify installation
    super --help
    
    # Get comprehensive documentation
    super docs
    ```
    
    **💡 Note:** The first execution of `super` commands may take a few seconds as Python compiles bytecodes.

---

## 🔧 Optional Dependencies

SuperOptiX supports various optional dependencies for enhanced functionality. Install them based on your needs:

=== "🤖 Local Model Management"
    
    **MLX (Apple Silicon)**
    ```bash
    pip install superoptix[mlx]
    ```
    - `mlx-lm==0.26.0` - Apple MLX framework for local inference
    
    **HuggingFace**
    ```bash
    pip install superoptix[huggingface]
    ```
    - `transformers==4.53.2` - HuggingFace transformers library
    - `torch==2.7.1` - PyTorch for model inference
    - `fastapi==0.116.1` - Web framework for model serving
    - `huggingface-hub==0.33.4` - HuggingFace Hub integration
    - `uvicorn==0.35.0` - ASGI server for FastAPI

=== "🗄️ Vector Databases"
    
    **ChromaDB**
    ```bash
    pip install superoptix[chromadb]
    ```
    
    **LanceDB**
    ```bash
    pip install superoptix[lancedb]
    ```
    
    **FAISS**
    ```bash
    pip install superoptix[faiss]
    ```
    
    **Weaviate**
    ```bash
    pip install superoptix[weaviate]
    ```
    
    **Qdrant**
    ```bash
    pip install superoptix[qdrant]
    ```
    
    **Milvus**
    ```bash
    pip install superoptix[milvus]
    ```
    
    **All Vector Databases**
    ```bash
    pip install superoptix[vectordb]
    ```

=== "📊 Observability & UI"
    
    **Observability**
    ```bash
    pip install superoptix[observability]
    ```
    - MLflow, Langfuse, monitoring tools
    
    **UI Components**
    ```bash
    pip install superoptix[ui]
    ```
    - Streamlit, Plotly, Pandas
    
    **Web Framework**
    ```bash
    pip install superoptix[web]
    ```
    - FastAPI, Uvicorn, Pydantic

---

## 🤖 Step 0: Install AI Models (Optional but Recommended)

After installing SuperOptiX, you'll need AI models to power your agents. For this guide, we'll use local models via Ollama:

```bash
# Download models for different agent tiers
super model install llama3.2:1b   # For Oracles tier (faster, lighter)
super model install llama3.2:8b   # For Genies tier (more capable)
```

**💡 Pro Tip:** You can also use cloud models (OpenAI, Anthropic) by setting API keys in your project's `.env` file.

---

## 🛠️ Step 1: Initialize Your SWE Project

```bash
super init swe
cd swe
ls -la
```

**💡 Pro Tip:** Add `--verbose` to see detailed project setup information:

```bash
super init swe --verbose
```

You should see a `.super` file in the root. **All further commands should be run from this directory.**

---

## 🤖 Step 2: Pull a Developer Agent

```bash
super agent pull developer
```

**💡 Pro Tip:** Add `--verbose` to see detailed agent information and guidance:

```bash
super agent pull developer --verbose
```

<details><summary>Output</summary>

```
================================================================================

🤖 Adding agent 'developer'...
╭──────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ 🎉 AGENT ADDED SUCCESSFULLY! Pre-built Agent Ready                                                       │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭──────────────────────────────────────────── 📋 Agent Details ────────────────────────────────────────────╮
│                                                                                                          │
│  🤖 Name: Developer Assistant                                                                          │
│  🏢 Industry: Software | 🔮 Tier: Oracles                                                                │
│  🔧 Tasks: 1 | 📁 Location: swe/agents/developer/playbook/developer_playbook.yaml                    │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭──────────────────────────────────────── 🛠️ Customization Options ────────────────────────────────────────╮
│                                                                                                          │
│  ✨ Pre-built Agent - Ready to Customize!                                                                │
│                                                                                                          │
│  📝 Modify: persona, tasks, inputs/outputs, model settings                                               │
│  📖 Guide: super docs → Agent Playbook Specifications                                                    │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─────────────────────────────────────────── 🎯 Workflow Guide ────────────────────────────────────────────╮
│                                                                                                          │
│  🚀 NEXT STEPS                                                                                           │
│                                                                                                          │
│  super agent compile developer - Generate executable pipeline                                          │
│  super agent run developer --goal "goal" - Execute optimized agent                                     │
│                                                                                                          │
│  💡 Comprehensive guide: super docs | 🔍 More agents: super agent list --pre-built                       │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
================================================================================
🎉 Agent 'Developer Assistant' ready for customization and deployment! 🚀
```

</details>

The agent playbook contains all configuration, feature specs, and scenarios for the developer agent.

### 📋 Understanding the Playbook Structure

SuperOptiX uses **SuperSpec** - a powerful DSL (Domain Specific Language) for writing agent specifications, context engineering, and agent engineering practices. Here's what the developer playbook contains:

<details><summary>📄 View Complete Developer Playbook YAML</summary>

```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: Developer Assistant
  id: developer
  namespace: software
  version: 1.0.0
  agent_type: Supervised
  level: oracles
  description: An agent that helps write clean, efficient, and maintainable code.
spec:
  language_model:
    location: local
    provider: ollama
    model: llama3.2:1b
    api_base: http://localhost:11434
  persona:
    name: DevBot
    role: Software Developer
    goal: Write clean, efficient, and maintainable code
    traits:
    - analytical
    - detail-oriented
    - problem-solver
  tasks:
  - name: implement_feature
    instruction: You are a Software Developer. Your goal is to write clean, efficient,
      and maintainable code. Implement the feature based on the provided requirement.
    inputs:
    - name: feature_requirement
      type: str
      description: A detailed description of the feature to implement.
      required: true
    outputs:
    - name: implementation
      type: str
      description: The code implementation of the feature.
  agentflow:
  - name: generate_code
    type: Generate
    task: implement_feature
  evaluation:
    builtin_metrics:
    - name: answer_exact_match
      threshold: 1.0
  feature_specifications:
    scenarios:
    - name: developer_comprehensive_task
      description: Given a complex software requirement, the agent should provide
        detailed analysis and recommendations
      input:
        feature_requirement: Complex software scenario requiring comprehensive analysis
      expected_output:
        implementation: Detailed step-by-step analysis with software-specific recommendations
    - name: developer_problem_solving
      description: When facing software challenges, the agent should demonstrate systematic
        problem-solving approach
      input:
        feature_requirement: Challenging software problem requiring creative solutions
      expected_output:
        implementation: Structured problem-solving approach with multiple solution
          options
    - name: developer_best_practices
      description: When asked about software best practices, the agent should provide
        current industry standards and guidelines
      input:
        feature_requirement: Industry best practices for software operations
      expected_output:
        implementation: Comprehensive best practices guide with implementation steps
    - name: developer_compliance_guidance
      description: Given regulatory requirements, the agent should provide compliance
        guidance specific to software
      input:
        feature_requirement: Compliance requirements for software operations
      expected_output:
        implementation: Detailed compliance checklist with regulatory requirements
    - name: developer_strategic_planning
      description: When developing software strategies, the agent should provide forward-thinking
        recommendations
      input:
        feature_requirement: Strategic planning for software growth and optimization
      expected_output:
        implementation: Comprehensive strategic plan with measurable objectives and
          timelines
  optimization:
    strategy: few_shot_bootstrapping
    metric: answer_correctness
    metric_threshold: 0.7
    few_shot_bootstrapping_config:
      max_bootstrapped_demos: 4
      max_rounds: 1
```

</details>

### 🔧 Key SuperSpec Components:

- **📋 Metadata**: Agent identity, version, and tier information

- **🤖 Persona**: Role definition, traits, and behavioral characteristics

- **⚙️ Tasks**: Specific capabilities with inputs/outputs and instructions

- **🔄 AgentFlow**: Execution logic and task orchestration

- **🧪 Feature Specifications**: BDD scenarios for evaluation and testing

- **🎯 Optimization**: DSPy configuration for performance improvement

This declarative approach makes agent development **reproducible**, **testable**, and **maintainable** - just like infrastructure as code!

---

## ⚙️ Step 3: Compile the Agent

```bash
super agent compile developer
```

**💡 Pro Tip:** Add `--verbose` to see detailed guidance and feature explanations:

```bash
super agent compile developer --verbose
```

<details><summary>Output</summary>

```
================================================================================

🔨 Compiling agent 'developer'...
╭───────────────────────────────────────── ⚡ Compilation Details ─────────────────────────────────────────╮
│                                                                                                          │
│  🤖 COMPILATION IN PROGRESS                                                                              │
│                                                                                                          │
│  🎯 Agent: Developer Assistant                                                                           │
│  🏗️ Framework: DSPy (default) Junior Pipeline — other frameworks coming soon                             │
│  🔧 Process: YAML playbook → Executable Python pipeline                                                  │
│  📁 Output: swe/agents/developer/pipelines/developer_pipeline.py                                         │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
🐍 Converted field names to snake_case for DSPy compatibility

🤖 Generating Mixin Oracles-Tier pipeline (DSPy default template)...
🧩 Mixin Pipeline (DSPy Default): Reusable components for complex agents.
🔧 Developer Controls: Modular mixins keep your codebase clean and customizable
🚀 Framework: DSPy (additional frameworks & custom builders coming soon) 
🔧 Oracles-Tier Features: Basic Chain of Thought + Sequential Orchestra
✅ Successfully generated Oracles-tier pipeline (mixin) at: 
/Users/super/swe/swe/agents/developer/pipelines/developer_pipeline.py

💡 Mixin pipeline features (DSPy Default):
   • Promotes code reuse and modularity
   • Separates pipeline logic into reusable mixins
   • Ideal for building complex agents with shared components
   • Built on DSPy – support for additional frameworks is on our roadmap

🎯 Oracles Tier Features

  ✅ Basic Predict and Chain of Thought modules
  ✅ Bootstrap Few-Shot optimization
  ✅ Basic evaluation metrics
  ✅ Sequential task orchestration
  ✅ Basic tracing and observability

ℹ️  Advanced features available in commercial version
╭──────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ 🎉 COMPILATION SUCCESSFUL! Pipeline Generated                                                            │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭──────────────────────────────────────── 🛠️ Customization Required ────────────────────────────────────────╮
│                                                                                                          │
│  ⚠️ Auto-Generated Pipeline                                                                             │
│                                                                                                          │
│  🚨 Starting foundation - Customize for production use                                                   │
│  💡 You own this code - Modify for your specific requirements                                            │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────── 🧪 Testing Enhancement ─────────────────────────────────────────╮
│                                                                                                          │
│  🧪 Current BDD Scenarios: 5 found                                                                       │
│                                                                                                          │
│  🎯 Recommendations:                                                                                     │
│  • Add comprehensive test scenarios to your playbook                                                     │
│  • Include edge cases and error handling scenarios                                                       │
│  • Test with real-world data samples                                                                     │
│                                                                                                          │
│  💡 Why scenarios matter: Training data for optimization & quality gates                                 │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─────────────────────────────────────────── 🎯 Workflow Guide ────────────────────────────────────────────╮
│                                                                                                          │
│  🚀 NEXT STEPS                                                                                           │
│                                                                                                          │
│  super agent evaluate developer - Establish baseline performance                                         │
│  super agent optimize developer - Enhance performance using DSPy                                         │
│  super agent evaluate developer - Measure improvement                                                    │
│  super agent run developer --goal "goal" - Execute optimized agent                                       │
│                                                                                                          │
│  💡 Follow BDD/TDD workflow: evaluate → optimize → evaluate → run                                        │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
================================================================================
🎉 Agent 'Developer Assistant' pipeline ready! Time to make it yours! 🚀
```

</details>

---

## 🧪 Step 4: Evaluate the Agent

```bash
super agent evaluate developer
```

**💡 Pro Tip:** Add `--verbose` to see detailed test results and guidance:

```bash
super agent evaluate developer --verbose
```

<details><summary>Output</summary>

```
════════════════════════════════════════════════════════════════════════════════════════════════════
                       🧪 SuperOptiX BDD Spec Runner - Professional Agent Validation

════════════════════════════════════════════════════════════════════════════════════════════════════

╭─────────────────────────────────────── 📋 Spec Execution Session ────────────────────────────────────────╮
│ 🎯 Agent:               developer                                                                        │
│ 📅 Session:             2025-07-08 10:31:32                                                              │
│ 🔧 Mode:                Standard validation                                                              │
│ 📊 Verbosity:           Summary                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

/Users/super/miniconda3/lib/python3.12/site-packages/google/protobuf/runtime_version.py:98: UserWarning: 
Protobuf gencode version 5.27.2 is exactly one major version older than the runtime version 6.31.1 at 
grpc_health/v1/health.proto. Please update the gencode to avoid compatibility violations in the next runtime
release.
  warnings.warn(
🔍 Tracing enabled for agent developer_20250708_103133
📁 Traces will be stored in: /Users/super/swe/.superoptix/traces
🚀 Configuring llama3.2:1b with ollama for oracles-tier capabilities
📝 Using ChatAdapter for optimal local model compatibility
✅ Model connection successful: ollama/llama3.2:1b
📋 Loaded 5 BDD specifications for execution
✅ DeveloperPipeline (Oracle tier) initialized with 5 BDD scenarios
✅ Pipeline loaded
ℹ️  Using base model (no optimization found)

🔍 Discovering BDD Specifications...
📋 Found 5 BDD specifications

🧪 Executing BDD Specification Suite
────────────────────────────────────────────────────────────
Progress: 🧪 Running 5 BDD specifications...
⠋ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 0/5❌ developer_comprehensive_task
❌ developer_problem_solving
❌ developer_best_practices
❌ developer_compliance_guidance
❌ developer_strategic_planning

Test Results:
FFFFF

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Specification                ┃    Status    ┃  Score   ┃ Description                                   ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━╇━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ developer_comprehensiv...    │   ❌ FAIL    │   0.29   │ Given a complex software requirement, t...    │
│ developer_problem_solving    │   ❌ FAIL    │   0.23   │ When facing software challenges, the ag...    │
│ developer_best_practices     │   ❌ FAIL    │   0.31   │ When asked about software best practice...    │
│ developer_compliance_g...    │   ❌ FAIL    │   0.21   │ Given regulatory requirements, the agen...    │
│ developer_strategic_pl...    │   ❌ FAIL    │   0.27   │ When developing software strategies, th...    │
└──────────────────────────────┴──────────────┴──────────┴───────────────────────────────────────────────┘

╭──────────────────────────────────── 🔴 Specification Results Summary ────────────────────────────────────╮
│                                                                                                          │
│  📊 Total Specs:         5                🎯 Pass Rate:         0.0%                                     │
│  ✅ Passed:              0                🤖 Model:             ollama_chat/llama3.2:1b                  │
│  ❌ Failed:              5                💪 Capability:        0.26                                     │
│  🏆 Quality Gate:        ❌ NEEDS WORK    🚀 Status:            ⚙️  Base Model                            │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

🔍 Failure Analysis - Grouped by Issue Type
────────────────────────────────────────────────────────────────────────────────

📋 Semantic Relevance Issues (5 failures)
────────────────────────────────────────────────────────────
💡 Fix Suggestions:
   🎯 Make the response more relevant to the expected output
   📝 Use similar terminology and technical concepts
   🔍 Ensure the output addresses all aspects of the input requirement
   💡 Review the expected output format and structure

Affected Specifications:
   • developer_comprehensive_task (score: 0.288)
   • developer_problem_solving (score: 0.226)
   • developer_best_practices (score: 0.314)
   • developer_compliance_guidance (score: 0.208)
   • developer_strategic_planning (score: 0.274)

╭───────────────────────────────────────── 🎯 AI Recommendations ──────────────────────────────────────────╮
│                                                                                                          │
│  💡 Poor performance. 5 scenarios failing.                                                               │
│  💡 Strong recommendation: Run optimization before production use.                                       │
│  💡 Consider using a more capable model (llama3.1:8b or gpt-4).                                          │
│  💡 Review scenario complexity vs model capabilities.                                                    │
│  💡 Fix semantic relevance in 5 scenario(s) - improve response clarity.                                  │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

╭───────────────────────────────────────────── 🎯 Next Steps ──────────────────────────────────────────────╮
│                                                                                                          │
│  🔧 5 specification(s) need attention.                                                                   │
│                                                                                                          │
│  Recommended actions for better quality:                                                                 │
│  • Review the grouped failure analysis above                                                             │
│  • super agent optimize developer - Optimize agent performance                                           │
│  • super agent evaluate developer - Re-evaluate to measure improvement                                   │
│  • Use --verbose flag for detailed failure analysis                                                      │
│                                                                                                          │
│  You can still test your agent:                                                                          │
│  • super agent run developer --goal "your goal" - Works even with failing specs                          │
│  • super agent run developer --goal "Create a simple function" - Try basic goals                         │
│  • 💡 Agents can often perform well despite specification failures                                       │
│                                                                                                          │
│  For production use:                                                                                     │
│  • Aim for ≥80% pass rate before deploying to production                                                 │
│  • Run optimization and re-evaluation cycles until quality gates pass                                    │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

════════════════════════════════════════════════════════════════════════════════════════════════════
                     🏁 Specification execution completed - 0.0% pass rate (0/5 specs)

════════════════════════════════════════════════════════════════════════════════════════════════════

╭─────────────────────────────────── 🎯 What would you like to do next? ───────────────────────────────────╮
│                                                                                                          │
│  🔧 To improve your agent's performance:                                                                 │
│     super agent optimize developer - Optimize the pipeline for better results                            │
│                                                                                                          │
│  🚀 To run your agent:                                                                                   │
│     super agent run developer --goal "your specific goal here"                                           │
│                                                                                                          │
│  💡 Example goals:                                                                                       │
│     • super agent run developer --goal "Create a Python function to calculate fibonacci numbers"         │
│     • super agent run developer --goal "Write a React component for a todo list"                         │
│     • super agent run developer --goal "Design a database schema for an e-commerce site"                 │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

</details>

### 🧪 Understanding Evaluation Results

The evaluation shows that your agent scored **0.0% pass rate** (0/5 scenarios). Here's what happened:

#### 📋 How BDD Specs Become DSPy Gold Examples

Your BDD scenarios from the playbook are automatically converted into **DSPy gold examples** for optimization:

1. **🎯 Scenario Extraction**: Each BDD scenario becomes a training example
2. **📝 Input/Output Pairs**: `feature_requirement` → `implementation` pairs
3. **🧠 DSPy Training Data**: Used to optimize prompts and reasoning chains
4. **⚡ Few-Shot Learning**: Creates better examples for the model

#### 🔍 Why Scores Are Low

The low scores are expected with `llama3.2:1b` because:

- **Small model capacity**: Limited reasoning and context understanding

- **Complex scenarios**: BDD specs test sophisticated software development tasks

- **High expectations**: Scenarios expect detailed, professional-level responses

#### ⚠️ Note on Model Pass Rates

!!! warning "Pass rates may be low with small models"
    
    **Pass rates may be low with small models like `llama3.2:1b`.** For higher pass rates and production use, try a larger model (e.g., `llama3.2:8b` or `gpt-4`) or further optimize your agent.

**💡 Don't worry!** Even with low evaluation scores, your agent can still perform well on real tasks. The evaluation is a **quality gate** for production readiness.

---

## 🎯 Step 5: Optimize the Agent

> ⚠️ **IMPORTANT WARNING: Optimization is Resource-Intensive**
> 
> **🚨 System Requirements:**
> - **Minimum 16GB GPU RAM** required for optimization
> - **8GB+ system RAM** recommended
> - **Stable internet connection** for API calls
> 
> **💡 Optimization Details:**
> - Makes multiple LLM API calls (can be costly)
> - Uses DSPy BootstrapFewShot strategy
> - May take several minutes to complete
> - **Use responsibly** - monitor your API usage
> 
> **🔄 Skip this step** if you don't meet the requirements or want to avoid costs. Your agent will still work without optimization.

```bash
super agent optimize developer
```

**💡 Pro Tip:** Add `--verbose` to see detailed guidance and optimization information:

```bash
super agent optimize developer --verbose
```

<details><summary>Output</summary>

```
================================================================================

🚀 Optimizing agent 'developer'...
╭──────────────────────────────────────── ⚡ Optimization Details ─────────────────────────────────────────╮
│                                                                                                          │
│  🤖 OPTIMIZATION IN PROGRESS                                                                             │
│                                                                                                          │
│  🎯 Agent: Developer                                                                                     │
│  🔧 Strategy: DSPy BootstrapFewShot                                                                      │
│  📊 Data Source: BDD scenarios from playbook                                                             │
│  💾 Output: swe/agents/developer/pipelines/developer_optimized.json                                      │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

🔍 Checking for existing optimized pipeline...
╭───────────────────────────────────────── 🚀 Optimization Notice ─────────────────────────────────────────╮
│ 🔧 DSPy Optimization in progress                                                                         │
│                                                                                                          │
│ • This step fine-tunes prompts and may take several minutes.                                             │
│ • API calls can incur compute cost – monitor your provider dashboard.                                    │
│ • You can abort anytime with CTRL+C; your base pipeline remains intact.                                  │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

🚀 Starting optimization using 'bootstrap' strategy...
/Users/super/miniconda3/lib/python3.12/site-packages/google/protobuf/runtime_version.py:98: UserWarning: Pr
otobuf gencode version 5.27.2 is exactly one major version older than the runtime version 6.31.1 at grpc_hea
lth/v1/health.proto. Please update the gencode to avoid compatibility violations in the next runtime release
.
  warnings.warn(
🔍 Tracing enabled for agent developer_20250708_103142
📁 Traces will be stored in: /Users/super/swe/.superoptix/traces
🚀 Configuring llama3.2:1b with ollama for oracles-tier capabilities
📝 Using ChatAdapter for optimal local model compatibility
✅ Model connection successful: ollama/llama3.2:1b
📋 Loaded 5 BDD specifications for execution
✅ DeveloperPipeline (Oracle tier) initialized with 5 BDD scenarios
✅ Found 5 scenarios for optimization
🚀 Training with 5 examples...
💾 Optimized model saved to /Users/super/swe/swe/agents/developer/pipelines/develop
er_optimized.json
╭──────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ 🎉 OPTIMIZATION SUCCESSFUL! Agent Enhanced                                                               │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭──────────────────────────────────────── 📊 Optimization Results ─────────────────────────────────────────╮
│                                                                                                          │
│  📈 Performance Improvement:                                                                             │
│  • Training Examples: 0                                                                                  │
│  • Optimization Score: None                                                                              │
│                                                                                                          │
│  💡 What changed: DSPy optimized prompts and reasoning chains                                            │
│  🚀 Ready for testing: Enhanced agent performance validated                                              │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─────────────────────────────────────────── 🤖 AI Enhancement ────────────────────────────────────────────╮
│                                                                                                          │
│  🧠 Smart Optimization: DSPy BootstrapFewShot                                                            │
│                                                                                                          │
│  ⚡ Automatic improvements: Better prompts, reasoning chains                                             │
│  🎯 Quality assurance: Test before production use                                                        │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─────────────────────────────────────────── 🎯 Workflow Guide ────────────────────────────────────────────╮
│                                                                                                          │
│  🚀 NEXT STEPS                                                                                           │
│                                                                                                          │
│  super agent evaluate developer - Measure optimization improvement                                       │
│  super agent run developer --goal "goal" - Execute enhanced agent                                        │
│  super orchestra create - Ready for multi-agent orchestration                                            │
│                                                                                                          │
│  💡 Follow BDD/TDD workflow: evaluate → optimize → evaluate → run                                        │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
================================================================================
🎉 Agent 'developer' optimization complete! Ready for testing! 🚀
```

</details>

### 🎯 What Happened During Optimization?

SuperOptiX created an optimized pipeline file: `swe/agents/developer/pipelines/developer_optimized.json`

This file contains:

1. **🧠 Optimized Prompts**: DSPy automatically improved the reasoning chains and prompts
2. **📚 Few-Shot Demos**: Generated examples from your BDD scenarios for better performance
3. **⚡ Enhanced Reasoning**: Better step-by-step thinking patterns
4. **🎯 Context-Aware Responses**: Improved understanding of software development tasks

The optimization process:

- ✅ **Used your 5 BDD scenarios** as training data
- ✅ **Applied DSPy BootstrapFewShot** strategy for automatic improvement
- ✅ **Generated optimized weights** for better performance
- ✅ **Preserved your original pipeline** while creating an enhanced version

**💡 The optimized file is automatically loaded** when you run your agent, giving you better results without any code changes!

---

## 🧪 Step 6: Re-Evaluate the Agent (After Optimization)

```bash
super agent evaluate developer
```

The re-evaluation shows similar results to the initial evaluation, with slight improvements in scores. This is expected with the small model we're using.

---

## ▶️ Step 7: Run the Agent Independently

Now let's test if the agent can execute goals independently:

```bash
super agent run developer --goal "Build a snake game in Python"
```

**💡 Pro Tip:** Add `--verbose` to see detailed execution information and guidance:

```bash
super agent run developer --goal "Build a snake game in Python" --verbose
```

<details><summary>Output</summary>

```
🚀 Running agent 'developer'...

Loading pipeline... ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━   0% -:--:--
🚀 Using pre-optimized pipeline from developer_optimized.json

Looking for pipeline at: 
/Users/super/swe/swe/agents/developer/pipelines/developer_pipeline.py
/Users/super/miniconda3/lib/python3.12/site-packages/google/protobuf/runtime_version.py:98: UserWarning: 
Protobuf gencode version 5.27.2 is exactly one major version older than the runtime version 6.31.1 at 
grpc_health/v1/health.proto. Please update the gencode to avoid compatibility violations in the next runtime
release.
  warnings.warn(
🔍 Tracing enabled for agent developer_20250708_111157
📁 Traces will be stored in: /Users/super/swe/.superoptix/traces
🚀 Configuring llama3.2:1b with ollama for oracles-tier capabilities
📝 Using ChatAdapter for optimal local model compatibility
✅ Model connection successful: ollama/llama3.2:1b
📋 Loaded 5 BDD specifications for execution
✅ DeveloperPipeline (Oracle tier) initialized with 5 BDD scenarios
Loading pipeline... ━━━━━━━━━━━━━━━━╺━━━━━━━━━━━━━━━━━━━━━━━  40% -:--:--📦 Loading pre-optimized model from
 developer_optimized.json
✅ Pre-optimized model loaded successfully
╭──────────────────────────────────────────── Agent Execution ─────────────────────────────────────────────╮
│ 🤖 Running Developer Pipeline                                                                            │
│                                                                                                          │
│ Executing Task: Build a snake game in Python                                                             │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯

           Analysis Results
┏━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Aspect         ┃ Value                                                                                   ┃
┡━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ Reasoning      │ Implement a basic Snake game using Pygame library, including features such as screen    │
│                │ rendering, user input handling, and collision detection.                                │
│ Implementation │ Here is an example implementation of the Snake game in Python using Pygame:             │
│                │                                                                                         │
│                │ import pygame;                                                                          │
│                │ import sys;                                                                             │
│                │ import random;                                                                          │
│                │                                                                                         │
│                │ # Initialize Pygame                                                                     │
│                │ pygame.init();                                                                          │
│                │ # Set up some constants                                                                 │
│                │ WIDTH = 800;                                                                            │
│                │ HEIGHT = 600;                                                                           │
│                │ FPS = 10;                                                                               │
│                │ WHITE = (255, 255, 255);                                                                │
│                │ RED = (255, 0, 0);                                                                      │
│                │ GREEN = (0, 255, 0);                                                                    │
│                │ colors = [WHITE, RED, GREEN];                                                           │
│                │                                                                                         │
│                │ # Set up the display                                                                    │
│                │ screen = pygame.display.set_mode((WIDTH, HEIGHT));                                      │
│                │ pygame.display.set_caption('Snake Game');                                               │
│                │                                                                                         │
│                │ # Define some functions to handle user input and game logic                             │
│                │ def draw_snake(snake_block):                                                            │
│                │     for x in range(100):                                                                │
│                │         pygame.draw.rect(screen, colors[0], (x*20, HEIGHT//2 + y*20, 20, 20));          │
│                │         if x > 80:                                                                      │
│                │             break;                                                                      │
│                │ draw_snake(snake_block+1)                                                               │
│                │                                                                                         │
│                │ def check_collision(x, y):                                                              │
│                │     for i in range(len(snake_block)):s snake_block[0] + snake_block[1]                  │
│                │     # Check horizontal collision                                                        │
│                │     if abs(s snake_block[0][0] - x) < 20 and abs(s snake_block[-1][0] - x) < 20:        │
│                │         return True;                                                                    │
│                │     # Check vertical collision                                                          │
│                │     if abs(s snake_block[0][1] - y) < 20 and abs(s snake_block[-1][1] - y) < 20:        │
│                │         return True;                                                                    │
│                │     # Check diagonal collision                                                          │
│                │     for i in range(2):for j in range(2):                                                │
│                │         if abs(s snake_block) == 20:                                                    │
│                │             return True;                                                                │
│                │     return False;                                                                       │
│                │ def move_left(snake_block):                                                             │
│                │     new_head = [snake_block[0][0] - 20, snake_block[0][1]]                              │
│                │     while check_collision(new_head[0], new_head[1]):                                    │
│                │         new_head = [snake_block[0][0] - 20, snake_block[0][1]]                          │
│                │     return new_head                                                                     │
│                │ def move_right(snake_block):                                                            │
│                │     new_head = [snake_block[0][0] + 20, snake_block[0][1]]                              │
│                │     while check_collision(new_head[0], new_head[1]):                                    │
│                │         new_head = [snake_block[0][0] + 20, snake_block[0][1]]                          │
│                │     return new_head                                                                     │
│                │ def move_up(snake_block):                                                               │
│                │     new_head = [snake_block[0][0], snake_block[0][1] - 20]                              │
│                │     while check_collision(new_head[0], new_head[1]):                                    │
│                │         new_head = [snake_block[0][0], snake_block[0][1] - 20]                          │
│                │     return new_head                                                                     │
│                │ def move_down(snake_block):                                                             │
│                │     new_head = [snake_block[0][0], snake_block[0][1] + 20]                              │
│                │     while check_collision(new_head[0], new_head[1]):                                    │
│                │         new_head = [snake_block[0][0], snake_block[0][1] + 20]                          │
│                │     return new_head                                                                     │
│                │ # Initialize the game variables                                                         │
│                │ head = [200, 300];                                                                      │
│                │ direction = 'right';                                                                    │
│                │ score = 0;                                                                              │
│                │ game_over = False;                                                                      │
│                │ snake_length = 10;                                                                      │
│                │ snake_block = [[200, 300], [220, 320], [240, 40], [260, 60], [280, 80]];                │
│ Trained        │ True                                                                                    │
│ Usage          │ {'ollama_chat/llama3.2:1b': {'completion_tokens': 852, 'prompt_tokens': 1264,           │
│                │ 'total_tokens': 2116, 'completion_tokens_details': 0, 'prompt_tokens_details': 0}}      │
│ Agent_Id       │ developer_20250708_111157                                                               │
│ Tier           │ oracles                                                                                 │
└────────────────┴─────────────────────────────────────────────────────────────────────────────────────────┘

Pre-Optimized Pipeline: ✅ YES
Runtime Optimization: ⚪ NO

Validation Status: ✅ PASSED
Validation Warnings: []

🎉 Agent execution completed successfully!

╭─────────────────────────────────── 🚀 What would you like to do next? ───────────────────────────────────╮
│                                                                                                          │
│  🔧 Improve your agent:                                                                                  │
│     super agent evaluate developer - Test agent performance with BDD specs                               │
│     super agent optimize developer - Optimize for better results                                         │
│                                                                                                          │
│  🎯 Create more agents:                                                                                  │
│     super agent add - Add a new agent to your project                                                    │
│     super agent design - Design a custom agent with AI assistance                                        │
│     super agent pull <agent_name> - Install a pre-built agent                                            │
│                                                                                                          │
│  🎼 Build orchestras (multi-agent workflows):                                                            │
│     super orchestra create <orchestra_name> - Create a new orchestra                                     │
│     super orchestra list - See existing orchestras                                                       │
│     super orchestra run <orchestra_name> --goal "complex task" - Run multi-agent workflow                │
│                                                                                                          │
│  📊 Explore and manage:                                                                                  │
│     super agent list - See all your agents                                                               │
│     super agent inspect developer - Detailed agent information                                           │
│     super marketplace - Browse available agents and tools                                                │
│                                                                                                          │
│  💡 Quick tips:                                                                                          │
│     • Use --optimize flag for runtime optimization                                                       │
│     • Add BDD specifications to your playbook for better testing                                         │
│     • Create orchestras for complex, multi-step workflows                                                │
│                                                                                                          │
╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

</details>

**🎉 Success!** Your developer agent can execute goals independently and provided a complete Snake game implementation using Pygame. This demonstrates that the agent works both:

- ✅ **Independently** - Can handle single tasks with detailed implementations
- ✅ **In orchestration** - Can work as part of a multi-agent team

---

## ➕ Step 8: Add More Agents (QA & DevOps)

```bash
super agent pull qa_engineer
super agent pull devops_engineer
super agent compile --all
```

<details><summary>Output</summary>

```
================================================================================

🤖 Adding agent 'qa_engineer'...
🎉 AGENT ADDED SUCCESSFULLY! Pre-built Agent Ready
📋 Agent Details:
  Name: QA Engineer Assistant
  Industry: Software | Tier: Oracles
  Tasks: 1 | Location: swe/agents/qa_engineer/playbook/qa_engineer_playbook.yaml
✨ Pre-built Agent - Ready to Customize!
📝 Modify: persona, tasks, inputs/outputs, model settings
📖 Guide: super docs → Agent Playbook Specifications

🤖 Adding agent 'devops_engineer'...
🎉 AGENT ADDED SUCCESSFULLY! Pre-built Agent Ready
📋 Agent Details:
  Name: DevOps Engineer Assistant
  Industry: Software | Tier: Oracles
  Tasks: 1 | Location: swe/agents/devops_engineer/playbook/devops_engineer_playbook.yaml
✨ Pre-built Agent - Ready to Customize!
📝 Modify: persona, tasks, inputs/outputs, model settings
📖 Guide: super docs → Agent Playbook Specifications

🚀 Compiling all 3 agents in project 'swe'...
================================================================================

🔨 Compiling agent 'developer'...
🎉 COMPILATION SUCCESSFUL! Pipeline Generated

🔨 Compiling agent 'devops_engineer'...
🎉 COMPILATION SUCCESSFUL! Pipeline Generated

🔨 Compiling agent 'qa_engineer'...
🎉 COMPILATION SUCCESSFUL! Pipeline Generated

🎉 ALL AGENTS COMPILED SUCCESSFULLY!
✅ Successful: 3 agent(s)
🚀 Ready for testing and customization!
```

</details>

!!! tip "Quick Start Note"
    
    You can evaluate and optimize these agents just like the developer, but for this quick start, we'll just compile them and get them ready for orchestration.

---

## 🎼 Step 9: Create and Run a Multi-Agent Orchestra

Now let's create an orchestra to coordinate your agents!

```bash
super orchestra create sdlc
```

**💡 Pro Tip:** Add `--verbose` to see detailed orchestra configuration and guidance:

```bash
super orchestra create sdlc --verbose
```

<details><summary>Output</summary>

```
🔎 Found 3 existing agent(s): developer, devops_engineer, qa_engineer. Adding them to the orchestra.
📝 Loaded 3 task(s) from agent playbooks.

✅ Created new orchestra definition at: swe/orchestras/sdlc_orchestra.yaml
👉 Orchestra automatically configured with tasks from agent playbooks.
   Found 3 task(s): implement_feature, configure_ci_pipeline, create_test_plan

💡 Customization Guidance:
   This is an automatic orchestra created based on your agent playbooks.
   You should refine this orchestra based on your specific goal to make it more targeted.
   You can:
   • Add more agents that align with your goal
   • Modify task descriptions to be more specific
   • Adjust execution strategy (sequential/parallel)
   • Add dependencies between tasks
   • Set custom timeouts and priorities

📋 Version Information:
   🆓 Free Version: Sequential execution strategy only
   💎 Pro Version: Parallel, hierarchical, mixed strategies + Kubernetes orchestration
   ℹ️  Orchestra kind 'basic' is supported in both versions

🚀 Ready to run: super orchestra run sdlc --goal "your specific goal here"
📝 Edit file: swe/orchestras/sdlc_orchestra.yaml

🎯 Orchestra Workflow Recommendations:
   Before running this orchestra, ensure your agents are optimized:
   1. Compile all agents: super agent compile --all
   2. Evaluate baseline: super agent evaluate <agent_name>
   3. Optimize agents: super agent optimize <agent_name> *(requires 16GB+ GPU RAM)*
   4. Re-evaluate improvement: super agent evaluate <agent_name>
   5. Then run orchestra: super orchestra run sdlc --goal "goal"

💡 Well-optimized individual agents lead to better orchestration results!
⚠️ **Note:** Step 3 (optimization) is resource-intensive and requires 16GB+ GPU RAM. Skip if you don't meet the requirements.
```

</details>

The orchestra automatically created a YAML configuration file that coordinates your three agents:

<details><summary>📄 View Complete Orchestra YAML Configuration</summary>

```yaml
# sdlc_orchestra.yaml
metadata:
  name: "Sdlc Orchestra"
  id: "sdlc"
  version: "1.0.0"
  kind: "basic"
  description: "An orchestra to accomplish a specific goal with flexible execution strategies."

orchestra:
  id: "sdlc"
  name: "Sdlc Orchestra"
  description: "An orchestra to accomplish a specific goal with flexible execution strategies."
  
  workspace:
    type: local_fs 
    path: "./orchestra_workspaces/sdlc"
  
  execution:
    strategy: "sequential"
    max_parallel_tasks: 1
    task_timeout_seconds: 300
    retry_strategy: "exponential_backoff"
    enable_metrics: true
    enable_trace: true

agents:
  - developer
  - devops_engineer
  - qa_engineer

tasks:
  - name: implement_feature
    agent: developer
    description: >
      Apply developer expertise to '{goal}'. Software Your goal is to write clean, efficient, and maintainable code. Implement the feature based on the provided requirement
    priority: "medium"
    timeout_seconds: 600
  - name: configure_ci_pipeline
    agent: devops_engineer
    description: >
      Apply devops engineer expertise to '{goal}'. DevOps Engineer. Your goal is to streamline development and deployment. Configure a basic CI/CD pipeline based on the project requirements
    context: ["implement_feature"]
    priority: "medium"
    timeout_seconds: 600
  - name: create_test_plan
    agent: qa_engineer
    description: >
      Apply qa engineer expertise to '{goal}'. Quality Assurance Engineer. Your goal is to ensure software quality. Create a high-level test plan including test cases for the given feature
    context: ["configure_ci_pipeline"]
    priority: "medium"
    timeout_seconds: 600
```

</details>

Now run the orchestra with a specific goal:

```bash
super orchestra run sdlc --goal "Build a simple login feature for a web application"
```

**💡 Pro Tip:** Add `--verbose` to see detailed execution information and guidance:

```bash
super orchestra run sdlc --goal "Build a simple login feature for a web application" --verbose
```

<details><summary>Output</summary>

```
🎼 Running Orchestra: sdlc
🎭 Agent Tier: oracles
📁 Using orchestra file: /Users/super/swe/swe/orchestras/sdlc_orchestra.yaml
📁 Created workspace directory: /Users/super/swe/orchestra_workspaces/sdlc
📂 Using workspace: /Users/super/swe/orchestra_workspaces/sdlc
🔐 Validating tier access for oracles tier...
✅ Tier validation passed!
🎼 Using basic orchestration mode
🚀 Running Basic Orchestra: Sdlc Orchestra
📋 Executing 3 tasks sequentially...

🔄 Task 1/3: implement_feature
🤖 Running Developer Pipeline
Executing Task: Build a simple login feature for a web application
✅ Task implement_feature completed in 2.95s

🔄 Task 2/3: configure_ci_pipeline
🤖 Running Devops_Engineer Pipeline
Executing Task: [Previous task output passed as context]
✅ Task configure_ci_pipeline completed in 2.29s

🔄 Task 3/3: create_test_plan
🤖 Running Qa_Engineer Pipeline
Executing Task: [Previous task outputs passed as context]
✅ Task create_test_plan completed in 2.13s

🎉 Orchestra completed successfully!
```

</details>

**🎉 What just happened?** Your three agents worked together sequentially:

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

_Example output:_
```shell
🔍 Loading traces for agent: developer
✅ Loaded 2 trace events
                     Traces for Agent: developer                     
┏━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━┳━━━━━━━━━┳━━━━━━━━━━┓
┃ Time     ┃ Component       ┃ Event           ┃ Status  ┃ Duration ┃
┡━━━━━━━━━━╇━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━╇━━━━━━━━━╇━━━━━━━━━━┩
│ 11:11:57 │ agent.developer │ agent_run_start │ success │ -        │
│ 11:12:03 │ agent.developer │ agent_run_end   │ success │ 6515.7ms │
└──────────┴─────────────────┴─────────────────┴─────────┴──────────┘

📊 Total: 2 | Errors: 0 | Avg: 6515.7ms
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
- ✅ Automatically optimized your agents with DSPy
- ✅ Validated them with real-world BDD scenarios
- ✅ Orchestrated them like Kubernetes for production workflows
- ✅ Generated production-ready artifacts

## 🧭 Next: Build More Powerful Agents (Genies Tier)

You just built an Oracles-tier agent, which does not use tools. To build more advanced agents with custom tools and RAG pipelines, try:

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

SuperOptiX follows **BDD (Behavior-Driven Development)** principles, putting evaluation at the core of AI agent development:

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

1. **Explore the marketplace**: `super marketplace browse`
2. **Try different agents**: `super agent pull` different types
3. **Experiment with tiers**: Start with oracles, move to genies

   ```bash
   super agent pull developer --tier genies
   ```

### For Intermediate Users

1. **Create custom agents**: Use `super spec generate`
2. **Build orchestras**: `super orchestra generate`
3. **Enable observability**: `super observe enable`

### For Advanced Users

1. **Design sovereign systems**: Multi-agent organizations
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

<div style="text-align: center; margin: 2rem 0; padding: 2rem; background: var(--primary-gradient); border-radius: var(--border-radius); color: var(--text-primary); box-shadow: var(--shadow-heavy);">
    <h2 style="margin-bottom: 1rem; font-size: 2rem; background: var(--text-gradient); background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-weight: var(--font-weight-bold);">🎉 Welcome to SuperOptiX!</h2>
    <p style="font-size: 1.1rem; margin-bottom: 1.5rem; color: var(--text-secondary);">You've just taken your first steps into the future of AI agent development.</p>
    <p style="font-size: 1.2rem; margin-bottom: 2rem; font-weight: var(--font-weight-semibold); color: var(--text-primary);">Ready to build something amazing?</p>
    
    <div style="display: flex; justify-content: center; gap: 1rem; flex-wrap: wrap; margin-top: 1.5rem;">
        <a href="../tutorials/genies-agent" style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; text-decoration: none; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); transition: var(--transition-smooth); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            🚀 Build Your First Genies Agent
        </a>
        <a href="../guides/marketplace" style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; text-decoration: none; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); transition: var(--transition-smooth); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            🏪 Explore the Marketplace
        </a>
        <a href="../guides/superspec" style="background: var(--md-default-bg-color); color: var(--text-primary); padding: 0.75rem 1.5rem; border-radius: 8px; text-decoration: none; font-weight: var(--font-weight-semibold); border: 2px solid var(--border-medium); transition: var(--transition-smooth); backdrop-filter: blur(10px); box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
            💎 Learn SuperSpec DSL
        </a>
    </div>
</div>

<div style="text-align: center; margin-top: 1rem; color: #666; font-style: italic;">
    *Happy building! 🚀*
</div> 