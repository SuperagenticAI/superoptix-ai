# 🔧 Installation Guide

Welcome to SuperOptiX! This guide will help you install the King of Agent Frameworks on your system. We support multiple installation methods and platforms to fit your development workflow.

!!! tip "🚀 Quick Start"
    **New to SuperOptiX?** Start with our [Quick Start Guide](quick-start.md) after installation!

## 📋 Prerequisites

Before installing SuperOptiX, ensure you have:

- **Python 3.11+** (required)
- **Git** (for development installations)
- **Package Manager** (pip, conda, or uv)

!!! warning "Python Version Requirement"
    SuperOptiX requires **Python 3.11 or higher**. Check your version with:
    ```bash
    python --version
    ```

## 🎯 Installation Methods

Choose your preferred installation method:

=== "🚀 UV (Recommended)"
    
    **UV** is the fastest Python package manager, offering lightning-fast installations and dependency resolution.
    
    ### Install UV First
    ```bash
    # macOS/Linux
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Windows (PowerShell)
    powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
    ```
    
    ### Install SuperOptiX with UV
    ```bash
    # Basic installation
    uv pip install superoptix --prerelease=allow
    
    # With specific extras
    uv pip install "superoptix[ui,vectordb,observability]"
    
    # Latest from PyPI
    uv pip install superoptix --prerelease=allow
    ```

=== "🐍 Pip"
    
    **Pip** is the standard Python package manager, available on all platforms.
    
    ### Install SuperOptiX with Pip
    ```bash
    # Basic installation
    pip install superoptix
    
    # With specific extras
    pip install "superoptix[ui,vectordb,observability]"
    
    # Latest from PyPI
    pip install superoptix
    ```

=== "🐍 Conda"
    
    **Conda** is great for managing Python environments and scientific computing dependencies.
    
    ### Create Conda Environment
    ```bash
    # Create new environment
    conda create -n superoptix python=3.11 -y
    
    # Activate environment
    conda activate superoptix
    
    # Install SuperOptiX
    pip install superoptix
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
    uv pip install superoptix --prerelease=allow
    ```
    
    ### Using Conda
    ```bash
    # Install Miniconda
    brew install --cask miniconda
    
    # Create environment
    conda create -n superoptix python=3.11 -y
    conda activate superoptix
    pip install superoptix
    ```

=== "🐧 Linux"
    
    ### Ubuntu/Debian
    ```bash
    # Update system
    sudo apt update && sudo apt upgrade -y
    
    # Install Python 3.11+
    sudo apt install python3.11 python3.11-venv python3-pip -y
    
    # Install UV
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix --prerelease=allow
    ```
    
    ### CentOS/RHEL/Fedora
    ```bash
    # Fedora
    sudo dnf install python3.11 python3-pip -y
    
    # CentOS/RHEL
    sudo yum install python3.11 python3-pip -y
    
    # Install UV
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Install SuperOptiX
    uv pip install superoptix --prerelease=allow
    ```

=== "🪟 Windows"
    
    ### Using PowerShell
    ```powershell
    # Install UV (recommended)
    powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
    
    # Install SuperOptiX
    uv pip install superoptix --prerelease=allow
    ```
    
    ### Using Conda
    ```powershell
    # Download and install Miniconda
    # https://docs.conda.io/en/latest/miniconda.html
    
    # Create environment
    conda create -n superoptix python=3.11 -y
    conda activate superoptix
    pip install superoptix
    ```

## 🔧 Optional Dependencies

SuperOptiX is modular - install only what you need! Here are the available extras:

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

### Still Having Issues?

- 📖 Check our [Troubleshooting Guide](troubleshooting.md)
- 🐛 Report issues on [GitHub](https://github.com/SuperagenticAI/superoptix/issues) 