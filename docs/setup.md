# 🔧 Installation Guide

Welcome to SuperOptiX! This guide will help you install the Full Stack Agentic AI Optimization Framework on your system.

!!! tip "🚀 Quick Start"
    **New to SuperOptiX?** Start with our [Quick Start Guide](quick-start.md) after installation!

!!! warning "Pre-Release Version 0.2.0b1"
    This is a pre-release version. Use `--pre` flag for installation:
    ```bash
    pip install superoptix==0.2.0b1 --pre
    ```

## 📋 Prerequisites

### Required

- **Python 3.11+** (required)
- **Git** (required for DSPy installation)
- **Package Manager** (pip, conda, or uv)

### Verify Requirements

```bash
# Check Python version
python --version  # Should be 3.11 or higher

# Check Git
git --version  # Should show git version
```

### Install Git (if needed)

=== "macOS"
    ```bash
    xcode-select --install
    ```

=== "Linux"
    ```bash
    # Ubuntu/Debian
    sudo apt-get install git
    
    # CentOS/RHEL
    sudo yum install git
    ```

=== "Windows"
    Download from [git-scm.com](https://git-scm.com/downloads)

!!! warning "Python Version Requirement"
    SuperOptiX requires **Python 3.11 or higher**. Check your version with:
    ```bash
    python --version
    ```

## 🎯 Installation Methods

!!! tip "Framework-Free Core"
    **SuperOptiX 0.2.0b1 core is now framework-independent!** 🎉
    
    Install only what you need. Choose from 6 AI frameworks, or use core without any.

Choose your preferred installation method:

=== "Core Only (Framework-Free)"
    ```bash
    pip install superoptix==0.2.0b1 --pre
    ```
    **Includes:** CLI tools, SuperSpec DSL, YAML processing, template engine
    
    **Does NOT include:** Any AI frameworks (DSPy, CrewAI, etc.)
    
    **Use for:** Framework-independent workflows, custom integrations

=== "With DSPy Framework"
    ```bash
    pip install superoptix[frameworks-dspy]==0.2.0b1 --pre
    ```
    **Includes:** SuperOptiX core + DSPy 3.0.4b1 + GEPA 0.0.17
    
    **Use for:** GEPA optimization, DSPy pipelines, evaluation

=== "With Specific Framework"
    ```bash
    # OpenAI Agents SDK
    pip install superoptix[frameworks-openai]==0.2.0b1 --pre
    
    # Google ADK
    pip install superoptix[frameworks-google]==0.2.0b1 --pre
    
    # Microsoft Agent Framework
    pip install superoptix[frameworks-microsoft]==0.2.0b1 --pre
    
    # DeepAgents
    pip install superoptix[frameworks-deepagents]==0.2.0b1 --pre
    
    # CrewAI (conflicts with DSPy)
    pip install superoptix[frameworks-crewai]==0.2.0b1 --pre
    ```
    
    **Choose ONE or COMBINE** (except DSPy + CrewAI)

=== "All DSPy-Compatible Frameworks"
    ```bash
    pip install superoptix[frameworks]==0.2.0b1 --pre
    ```
    **Includes:** DSPy, OpenAI SDK, Google ADK, Microsoft, DeepAgents
    
    **Excludes:** CrewAI (conflicts with DSPy's json-repair)

=== "With MCP Optimization"
    ```bash
    pip install superoptix[mcp]==0.2.0b1 --pre
    ```
    **Includes:** MCP SDK 1.19.0 for tool optimization

=== "With Everything"
    ```bash
    pip install superoptix[all]==0.2.0b1 --pre
    ```
    **Includes:** All frameworks + MCP + vector DBs + observability

=== "Using UV"
    ```bash
    # Install UV first
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix==0.2.0b1 --pre
    ```

=== "Using Conda"
    ```bash
    # Create environment
    conda create -n superoptix python=3.11 -y
    conda activate superoptix
    
    # Install SuperOptiX
    pip install superoptix==0.2.0b1 --pre
    ```

## 🖥️ Platform-Specific Instructions

=== "🍎 macOS"
    
    ### Using Homebrew (Recommended)
    ```bash
    # Install Python 3.11+
    brew install python@3.11
    
    # Install UV (recommended)
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix==0.2.0b1 --pre
    ```
    
    ### Using Conda
    ```bash
    # Install Miniconda
    brew install --cask miniconda
    
    # Create environment
    conda create -n superoptix python=3.11 -y
    conda activate superoptix
    pip install superoptix==0.2.0b1 --pre
    ```

=== "🐧 Linux"
    
    ### Ubuntu/Debian
    ```bash
    # Update system
    sudo apt update && sudo apt upgrade -y
    
    # Install Python 3.11+ and Git
    sudo apt install python3.11 python3.11-venv python3-pip git -y
    
    # Install UV
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix==0.2.0b1 --pre
    ```
    
    ### CentOS/RHEL/Fedora
    ```bash
    # Fedora
    sudo dnf install python3.11 python3-pip git -y
    
    # CentOS/RHEL
    sudo yum install python3.11 python3-pip git -y
    
    # Install UV
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix==0.2.0b1 --pre
    ```

=== "🪟 Windows"
    
    !!! warning "Windows Users - Important!"
        
        **On Windows, set PYTHONUTF8=1** to ensure proper UTF-8 encoding support:
        
        ```cmd
        set PYTHONUTF8=1
        ```
        
        Or add it to your system environment variables for permanent setting.
    
    ### Using PowerShell
    ```powershell
    # Install Git first
    # Download from: https://git-scm.com/downloads
    
    # Install UV (recommended)
    powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
    
    # Install SuperOptiX
    uv pip install superoptix==0.2.0b1 --prerelease=allow
    ```
    
    ### Using Conda
    ```powershell
    # Download and install Miniconda
    # https://docs.conda.io/en/latest/miniconda.html
    
    # Install Git
    # Download from: https://git-scm.com/downloads
    
    # Create environment
    conda create -n superoptix python=3.11 -y
    conda activate superoptix
    pip install superoptix==0.2.0b1 --pre
    ```

## 🔧 Optional Dependencies

SuperOptiX is modular - install only what you need! Here are the available extras:

### 🌐 Framework Support (NEW in 0.2.0b1)

SuperOptiX now supports 6 major AI agent frameworks. Install the ones you need:

| Framework | Install Command | Version | Includes |
|-----------|----------------|---------|----------|
| **DSPy** ⭐ | `pip install superoptix[frameworks-dspy]==0.2.0b1 --pre` | 3.0.4b1 | DSPy + GEPA 0.0.17 |
| **OpenAI SDK** | `pip install superoptix[frameworks-openai]==0.2.0b1 --pre` | 0.4.1 | openai-agents, openai SDK |
| **Google ADK** | `pip install superoptix[frameworks-google]==0.2.0b1 --pre` | 1.17.0 | google-adk, google-generativeai |
| **Microsoft** | `pip install superoptix[frameworks-microsoft]==0.2.0b1 --pre` | latest | agent-framework, azure-identity |
| **DeepAgents** | `pip install superoptix[frameworks-deepagents]==0.2.0b1 --pre` | latest | deepagents |
| **CrewAI** ⚠️ | `pip install superoptix[frameworks-crewai]==0.2.0b1 --pre` | 1.2.0 | crewai (conflicts with DSPy) |

⭐ **Recommended:** DSPy for GEPA optimization  
⚠️ **Note:** CrewAI and DSPy cannot be installed together

**Framework-Specific Setup:**

=== "DSPy (Recommended)"
    ```bash
    # Install
    pip install superoptix[frameworks-dspy]==0.2.0b1 --pre
    ```
    
    **Includes:** DSPy 3.0.4b1 + GEPA 0.0.17
    
    **Use for:** GEPA optimization, evaluation, orchestration
    
    **No API key required** - Works with Ollama, OpenAI, Anthropic, etc.

=== "OpenAI SDK"
    ```bash
    # Install
    pip install superoptix[frameworks-openai]==0.2.0b1 --pre
    
    # For OpenAI API (optional, Ollama works too)
    export OPENAI_API_KEY=your-key
    ```

=== "Google ADK"
    ```bash
    # Install
    pip install superoptix[frameworks-google]==0.2.0b1 --pre
    
    # Set API key
    export GOOGLE_API_KEY=your-google-api-key
    ```

=== "Microsoft"
    ```bash
    # Install
    pip install superoptix[frameworks-microsoft]==0.2.0b1 --pre
    
    # For Azure OpenAI
    export AZURE_OPENAI_ENDPOINT=your-endpoint
    export AZURE_OPENAI_API_KEY=your-key
    ```

=== "DeepAgents"
    ```bash
    # Install
    pip install superoptix[frameworks-deepagents]==0.2.0b1 --pre
    ```
    
    **Use for:** LangGraph-based planning and complex workflows

=== "CrewAI"
    ```bash
    # Install
    pip install superoptix[frameworks-crewai]==0.2.0b1 --pre
    ```
    
    ⚠️ **Cannot be installed with DSPy** (json-repair conflict)
    
    **Use for:** Multi-agent crew workflows without DSPy optimization

### 🔌 MCP Tool Optimization (NEW in 0.2.0b1)

Optimize MCP tool descriptions and system prompts with GEPA:

```bash
pip install superoptix[mcp]==0.2.0b1 --pre
```

**Includes:** MCP SDK 1.19.0

**Use Cases:**
- Optimize MCP tool descriptions
- Improve system prompts for tool usage
- Multi-tool selection optimization
- Local and remote MCP servers

**Example:**
```python
from superoptix.optimizers import MCPAdapter
import gepa

adapter = MCPAdapter(
    tool_names=["read_file", "write_file"],
    task_model="ollama/llama3.2:1b",
    metric_fn=my_metric,
)

result = gepa.optimize(
    seed_candidate={"tool_description": "Read files"},
    adapter=adapter,
    trainset=dataset,
)
```

See [MCP Optimization Tutorial](../tutorials/mcp-optimization.md) for details.

### 📦 Other Optional Dependencies

=== "🤖 Local Model Management"
    
    **For running models locally on your machine**
    
    **MLX (Apple Silicon)**
    ```bash
    pip install "superoptix[mlx]"
    ```
    **Includes:**
    - mlx-lm==0.26.0 (Apple MLX framework for local inference)
    
    **HuggingFace**
    ```bash
    pip install "superoptix[huggingface]"
    ```
    **Includes:**
    - transformers==4.53.2 (HuggingFace transformers library)
    - torch==2.7.1 (PyTorch for model inference)
    - fastapi==0.116.1 (Web framework for model serving)
    - huggingface-hub==0.33.4 (HuggingFace Hub integration)
    - uvicorn==0.35.0 (ASGI server for FastAPI)

=== "🎨 UI & Visualization"
    
    **For SuperOptiX Agent Studio and observability dashboards**
    
    ```bash
    # Install UI dependencies
    pip install "superoptix[ui]"
    ```
    
    **Includes:**
    - Streamlit (Agent Studio)
    - Plotly (Interactive charts)
    - Pandas (Data manipulation)

=== "🧠 Vector Databases (RAG)"
    
    **For Retrieval-Augmented Generation and memory systems**
    
    ```bash
    # Individual databases
    pip install "superoptix[chromadb]"    # ChromaDB (recommended)
    pip install "superoptix[lancedb]"     # LanceDB (fast local)
    pip install "superoptix[faiss]"       # FAISS (high performance)
    pip install "superoptix[weaviate]"    # Weaviate (semantic search)
    pip install "superoptix[qdrant]"      # Qdrant (production)
    pip install "superoptix[milvus]"      # Milvus (enterprise)
    
    # All vector databases
    pip install "superoptix[vectordb]"
    ```

=== "🔍 Observability & Monitoring"
    
    **For tracing, monitoring, and MLflow integration**
    
    ```bash
    # Install observability dependencies
    pip install "superoptix[observability]"
    ```
    
    **Includes:**
    - MLflow (Experiment tracking)
    - Pandas (Data analysis)
    - Plotly (Visualization)

=== "🌐 Web Frameworks"
    
    **For building web APIs and services**
    
    ```bash
    # Install web dependencies
    pip install "superoptix[web]"
    ```
    
    **Includes:**
    - FastAPI (Modern web framework)
    - Uvicorn (ASGI server)
    - Pydantic (Data validation)

=== "📊 Data Processing"
    
    **For data analysis and machine learning**
    
    ```bash
    # Install data processing dependencies
    pip install "superoptix[data]"
    ```
    
    **Includes:**
    - Pandas (Data manipulation)
    - Scikit-learn (Machine learning)
    - Matplotlib (Plotting)
    - Seaborn (Statistical visualization)

=== "🤖 AI Framework Integration"
    
    **For advanced AI orchestration and multi-agent systems**
    
    ```bash
    # Install core AI framework dependencies
    pip install "superoptix[optimas]"
    ```
    
    **Includes:**
    - DSPy (Prompt optimization framework)
    - OpenAI (LLM integration)
    - AutoGen (Multi-agent conversations)
    - Optimas AI (Advanced orchestration)
    
    !!! warning "CrewAI Dependency Conflict"
        **CrewAI has a known dependency conflict** with DSPy due to incompatible `json-repair` version requirements:
        
        - **DSPy 3.0.0** requires `json-repair>=0.30.0`
        - **CrewAI 0.157.0** requires `json-repair==0.25.2`
        
        **To use CrewAI with SuperOptiX, install it manually:**
        ```bash
        # 1. Install SuperOptiX with DSPy support
        pip install "superoptix[optimas]"
        
        # 2. Install CrewAI without dependencies
        pip install crewai==0.157.0 --no-deps
        
        # 3. Ensure compatible json-repair version
        pip install "json-repair>=0.30.0"
        ```
        
        This approach bypasses the dependency conflict while maintaining compatibility.

## 🔍 Verification

After installation, verify SuperOptiX is working correctly:

```bash
# Check installation
python -c "import superoptix; print('SuperOptiX installed successfully!')"

# Check CLI
super --version

# Check available commands
super --help
```

## 🚀 Next Steps

1. **Set up your LLM**: Follow our [LLM Setup Guide](llm-setup.md)
2. **Create your first agent**: Try our [Quick Start Guide](quick-start.md)
3. **Explore the framework**: Check out our [Agent Patterns](agent-patterns.md)

## 🆘 Troubleshooting

### Common Issues

**Import Error**: Make sure you're using Python 3.11+
```bash
python --version
```

**Permission Error**: Use virtual environments
```bash
# Create virtual environment
python -m venv superoptix-env
source superoptix-env/bin/activate  # Linux/macOS
# or
superoptix-env\Scripts\activate     # Windows
```

**Package Not Found**: Update pip
```bash
pip install --upgrade pip
```

**CrewAI Installation Conflicts**: If you encounter dependency conflicts when installing CrewAI with SuperOptiX:
```bash
# The issue: CrewAI requires json-repair==0.25.2, but DSPy needs json-repair>=0.30.0
# Solution: Install manually with --no-deps flag
pip install "superoptix[optimas]"  # Install DSPy support first
pip install crewai==0.157.0 --no-deps  # Install CrewAI without dependencies
pip install "json-repair>=0.30.0"  # Ensure compatible version
```

### Still Having Issues?

- 📖 Check our [Troubleshooting Guide](troubleshooting.md)
- 🐛 Report issues on [GitHub](https://github.com/SuperagenticAI/superoptix/issues) 