# Development Guide

This guide explains how to set up and work with the SuperOptiX framework for local development and customization.

## Prerequisites

- Python 3.11 or higher
- `uv` package manager (install from https://docs.astral.sh/uv/getting-started/installation/)
- Git

## Quick Start

### Option 1: Using pip (Recommended)

1. **Install SuperOptiX**
   ```bash
   pip install superoptix
   ```

2. **Initialize a project**
   ```bash
   super init my-project
   cd my-project
   ```

3. **Start using the framework**
   ```bash
   super --help
   ```

### Option 2: Using uv for Development

1. **Install SuperOptiX with uv**
   ```bash
   uv add superoptix
   ```

2. **Initialize a project**
   ```bash
   uv run super init my-project
   cd my-project
   ```

3. **Start using the framework**
   ```bash
   uv run super --help
   ```

## Framework Usage

### Basic Commands
```bash
# Initialize a new project
super init my-project

# List available agents
super agent list

# Pull a pre-built agent
super agent pull developer

# Compile an agent
super agent compile developer

# Run an agent
super agent run developer --goal "Build a web app"
```

### Advanced Features
```bash
# Model management
super model list
super model install llama3.2:3b

# Orchestration
super orchestra create my-orchestra
super orchestra run my-orchestra

# Observability
super observe dashboard
```

## Framework Management

### Updating SuperOptiX
```bash
# Update to latest version
pip install --upgrade superoptix

# Check current version
super --version
```

### Model Management
```bash
# List available models
super model list

# Install a model
super model install llama3.2:3b

# Check model info
super model info llama3.2:3b
```

## Framework Structure

Understanding the framework layout:

```
superoptix/
├── 🎯 superoptix/           # Core framework
│   ├── cli/                 # Command-line interface
│   ├── agents/              # Pre-built agent playbooks
│   ├── compiler/            # Agent compilation system
│   ├── memory/              # Multi-layered memory systems
│   ├── observability/       # Tracing and monitoring
│   ├── runners/             # Agent execution engines
│   └── tools/               # Built-in agent tools
├── 📚 docs/                 # Documentation
└── 🧪 tests/                # Test suite
```

## Framework Updates

SuperOptiX is regularly updated with new features and improvements:

1. **Automatic Updates**: Framework updates are released through PyPI
2. **Version Management**: Use `super --version` to check your version
3. **Release Notes**: Check our documentation for latest changes

## Environment Variables

For framework usage, you may need to set:
- `SUPEROPTIX_API_KEY`: For premium features (if applicable)
- `SUPEROPTIX_MODEL_BACKEND`: Default model backend (ollama, mlx, etc.)

## Troubleshooting

### Common Issues

1. **Installation issues**: Ensure Python 3.8+ is installed
2. **Model backend issues**: Check model backend configuration
3. **Agent compilation errors**: Verify agent playbook syntax
4. **Permission errors**: Check file permissions in project directory

### Environment Management

- **Virtual environments**: Recommended for isolation
- **Model backends**: Configure appropriate backend for your system
- **Project isolation**: Each project has its own configuration

### Getting Help

- Check our [documentation](https://docs.super-agentic.ai)
- Visit our [support portal](https://support.super-agentic.ai)
- Join our [community forum](https://community.super-agentic.ai) 