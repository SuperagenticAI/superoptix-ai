# 🐍 Environment Setup Guide

This guide covers setting up your development environment for SuperOptiX, including Python environments, virtual environments, and best practices for different operating systems.

## 🎯 Overview

A properly configured environment is crucial for SuperOptiX development. This guide covers:

- **🐍 Python Setup**: Installing and configuring Python
- **🔧 Virtual Environments**: Isolating project dependencies
- **📦 Package Management**: Using pip, uv, conda, and poetry
- **🛠️ Development Tools**: IDE setup and debugging tools

## 🐍 Python Setup

### **Python Version Requirements**

SuperOptiX requires Python 3.11+ (3.12 recommended):

```bash
# Check your Python version
python --version
# or
python3 --version

# Should show Python 3.11.x or 3.12.x
```

### **Installing Python**

=== "🍎 macOS"
    ```bash
    # Using Homebrew (recommended)
    brew install python@3.12
    
    # Using pyenv (for multiple Python versions)
    brew install pyenv
    pyenv install 3.12.0
    pyenv global 3.12.0
    
    # Using official installer
    # Download from https://www.python.org/downloads/
    ```

=== "🐧 Linux (Ubuntu/Debian)"
    ```bash
    # Update package list
    sudo apt update
    
    # Install Python 3.12
    sudo apt install python3.12 python3.12-venv python3.12-pip
    
    # Set as default (optional)
    sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1
    ```

=== "🪟 Windows"
    ```bash
    # Using winget
    winget install Python.Python.3.12
    
    # Using Chocolatey
    choco install python
    
    # Using official installer
    # Download from https://www.python.org/downloads/
    ```

=== "🌐 Cross-platform (pyenv)"
    ```bash
    # Install pyenv
    curl https://pyenv.run | bash
    
    # Add to shell profile (.bashrc, .zshrc, etc.)
    echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
    echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(pyenv init -)"' >> ~/.bashrc
    
    # Install Python 3.12
    pyenv install 3.12.0
    pyenv global 3.12.0
    ```

## 🔧 Virtual Environments

### **Why Virtual Environments?**

Virtual environments isolate project dependencies, preventing conflicts between different projects:

- **Isolation**: Each project has its own Python packages
- **Reproducibility**: Exact dependency versions for consistent builds
- **Clean Development**: No system-wide package pollution
- **Easy Cleanup**: Remove entire environment when done

=== "🐍 venv (Built-in)"
    ```bash
    # Create a new virtual environment
    python -m venv superoptix-env
    
    # Activate the environment
    # On macOS/Linux:
    source superoptix-env/bin/activate
    
    # On Windows:
    superoptix-env\Scripts\activate
    
    # Install SuperOptiX
    pip install superoptix
    
    # Deactivate when done
    deactivate
    ```

=== "📦 conda (Recommended)"
    ```bash
    # Install Miniconda (lightweight)
    # Download from https://docs.conda.io/en/latest/miniconda.html
    
    # Create a new conda environment
    conda create -n superoptix python=3.12
    
    # Activate the environment
    conda activate superoptix
    
    # Install SuperOptiX
    pip install superoptix
    
    # Deactivate when done
    conda deactivate
    ```

=== "⚡ uv (Ultra-fast)"
    ```bash
    # Install uv
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Create a new project
    uv init superoptix-project
    cd superoptix-project
    
    # Add SuperOptiX to dependencies
    uv add superoptix
    
    # Install dependencies
    uv sync
    
    # Run with uv
    uv run super --version
    ```

=== "📚 Poetry"
    ```bash
    # Install Poetry
    curl -sSL https://install.python-poetry.org | python3 -
    
    # Create a new project
    poetry new superoptix-project
    cd superoptix-project
    
    # Add SuperOptiX dependency
    poetry add superoptix
    
    # Activate virtual environment
    poetry shell
    
    # Run commands
    poetry run super --version
    ```

## 📦 Package Management

=== "📦 pip (Standard)"
    ```bash
    # Install SuperOptiX
    pip install superoptix
    
    # Install with optional dependencies
    pip install superoptix[vectordb,ui,observability]
    
    # Install latest version
    pip install --upgrade superoptix
    ```

=== "⚡ uv (Recommended)"
    ```bash
    # Install SuperOptiX
    uv pip install superoptix
    
    # Install with optional dependencies
    uv pip install "superoptix[vectordb,ui,observability]"
    
    # Create requirements.txt
    uv pip freeze > requirements.txt
    
    # Install from requirements
    uv pip install -r requirements.txt
    ```

=== "📦 conda"
    ```bash
    # Install from conda-forge (if available)
    conda install -c conda-forge superoptix
    
    # Or use pip within conda environment
    conda activate superoptix
    pip install superoptix
    ```

## 🛠️ Development Tools

### **IDE Setup**

=== "💻 VS Code"
    ```bash
    # Install VS Code extensions
    code --install-extension ms-python.python
    code --install-extension charliermarsh.ruff
    code --install-extension ms-python.pylint
    ```

    **VS Code Settings (`settings.json`):**
    ```json
    {
      "python.defaultInterpreterPath": "./superoptix-env/bin/python",
      "python.formatting.provider": "ruff",
      "python.linting.enabled": true,
      "python.linting.pylintEnabled": true,
      "python.linting.ruffEnabled": true,
      "editor.formatOnSave": true,
      "editor.codeActionsOnSave": {
        "source.organizeImports": true
      }
    }
    ```

=== "🐍 PyCharm"
    ```bash
    # 1. Open Project: Open your SuperOptiX project
    # 2. Configure Interpreter: 
    #    Go to File > Settings > Project > Python Interpreter
    #    Add your virtual environment
    # 3. Install Extensions:
    #    - Ruff
    #    - Pylint
    ```

=== "🚀 Cursor"
    ```bash
    # Install Cursor extensions
    # Cursor comes with excellent Python support built-in
    
    # Recommended extensions for Python development:
    # - Python (built-in)
    # - Ruff (built-in)
    # - GitLens (built-in)
    ```

=== "🌊 WindSurf"
    ```bash
    # WindSurf provides AI-powered code assistance
    # Install from https://windsurf.ai
    
    # Configure Python interpreter in settings
    # Enable Ruff for code formatting and linting
    ```

=== "📓 Jupyter Notebooks"
    ```bash
    # Install Jupyter
    pip install jupyter notebook
    
    # Install SuperOptiX in Jupyter environment
    pip install superoptix
    
    # Start Jupyter
    jupyter notebook
    ```

### **Code Quality Tools**

#### **Ruff (Code Formatting & Linting)**

Ruff is an extremely fast Python linter and formatter written in Rust:

```bash
# Install Ruff
pip install ruff

# Format code
ruff format .

# Lint code
ruff check .

# Fix issues automatically
ruff check --fix .

# Check formatting
ruff format --check .
```

**Ruff Configuration (`.ruff.toml`):**
```toml
# Target Python version
target-version = "py312"

# Line length
line-length = 88

# Enable all rules
select = ["ALL"]

# Ignore specific rules
ignore = [
    "E501",  # Line too long
    "D100",  # Missing docstring in public module
    "D104",  # Missing docstring in public package
]

# Format settings
[format]
quote-style = "double"
indent-style = "space"
skip-magic-trailing-comma = false
line-ending = "auto"
```

#### **Pre-commit Hooks**

```bash
# Install pre-commit
pip install pre-commit

# Create .pre-commit-config.yaml
cat > .pre-commit-config.yaml << EOF
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.6
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
EOF

# Install hooks
pre-commit install
```

## 🔧 Environment Variables

### **Setting Environment Variables**

=== "🍎 macOS/Linux"
    ```bash
    # Temporary (current session)
    export OPENAI_API_KEY="your-api-key"
    export ANTHROPIC_API_KEY="your-api-key"
    
    # Permanent (add to ~/.bashrc or ~/.zshrc)
    echo 'export OPENAI_API_KEY="your-api-key"' >> ~/.bashrc
    echo 'export ANTHROPIC_API_KEY="your-api-key"' >> ~/.bashrc
    source ~/.bashrc
    ```

=== "🪟 Windows"
    ```cmd
    # Temporary (current session)
    set OPENAI_API_KEY=your-api-key
    set ANTHROPIC_API_KEY=your-api-key
    
    # Permanent (System Properties > Environment Variables)
    # Or use PowerShell:
    [Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "your-api-key", "User")
    ```

=== "📄 .env Files"
    ```bash
    # Create .env file
    cat > .env << EOF
    OPENAI_API_KEY=your-api-key
    ANTHROPIC_API_KEY=your-api-key
    GOOGLE_API_KEY=your-api-key
    AZURE_OPENAI_API_KEY=your-azure-key
    AZURE_OPENAI_ENDPOINT=https://your-resource.openai.azure.com/
    EOF
    
    # Load with python-dotenv
    pip install python-dotenv
    
    # In your Python code
    from dotenv import load_dotenv
    load_dotenv()
    ```

## 🧪 Testing Your Environment

### **Environment Validation**

```bash
# Test Python installation
python --version
pip --version

# Test SuperOptiX installation
super --version

# Test basic functionality
python -c "
from superoptix import SuperOptiX
print('SuperOptiX imported successfully!')
"
```

### **Dependency Check**

```bash
# Check installed packages
pip list | grep superoptix

# Check for conflicts
pip check

# Verify environment isolation
which python
which pip
```

## 🚨 Troubleshooting

### **Common Issues**

=== "🐍 Python Version Issues"
    ```bash
    # Check available Python versions
    python --version
    python3 --version
    python3.12 --version
    
    # Use specific version
    python3.12 -m pip install superoptix
    ```

=== "🔐 Permission Issues"
    ```bash
    # Don't use sudo with pip
    # Instead, use virtual environments
    
    # If you must install globally
    pip install --user superoptix
    ```

=== "🛤️ Path Issues"
    ```bash
    # Check PATH
    echo $PATH
    
    # Add Python to PATH (if needed)
    export PATH="$HOME/.local/bin:$PATH"
    ```

=== "🔧 Virtual Environment Issues"
    ```bash
    # Recreate virtual environment
    rm -rf superoptix-env
    python -m venv superoptix-env
    source superoptix-env/bin/activate
    pip install superoptix
    ```

### **Performance Optimization**

=== "⚡ Using uv for Faster Installs"
    ```bash
    # Install uv
    curl -LsSf https://astral.sh/uv/install.sh | sh
    
    # Use uv instead of pip
    uv pip install superoptix
    ```

=== "📦 Using Conda for Better Dependency Resolution"
    ```bash
    # Create conda environment
    conda create -n superoptix python=3.12
    conda activate superoptix
    pip install superoptix
    ```

## 📚 Next Steps

Now that your environment is set up:

1. **Install SuperOptiX** following the [Installation Guide](setup.md)
2. **Configure LLMs** with the [LLM Setup Guide](llm-setup.md)
3. **Create your first agent** with the [Quick Start Guide](quick-start.md)
4. **Learn project structure** with the [Project Structure Guide](project-structure.md)

For advanced development setup, see the [Development Guide](../development/index.md). 