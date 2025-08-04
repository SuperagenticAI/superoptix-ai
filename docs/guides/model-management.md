# 🧠 Model Management Guide

SuperOptiX provides comprehensive model management capabilities with support for multiple backends, automatic installation, and direct model execution.

## Overview

The model management system allows you to:
- **Install models** across different backends (Ollama, MLX, HuggingFace)
- **Run models directly** without server setup
- **Auto-install models** when they're not found
- **Manage model lifecycle** with installation, removal, and updates

## Quick Start

### Running Models Directly

The easiest way to use models is with the `super model run` command:

```bash
# Run a model with auto-installation
super model run llama3.2:3b "Write a Python function to add two numbers"

# Specify backend explicitly
super model run llama3.2:3b "Write a hello world program" --backend ollama

# Interactive mode
super model run llama3.2:3b "" --interactive
```

### Installing Models

Install models for specific backends:

```bash
# Install Ollama model
super model install llama3.2:3b --backend ollama

# Install MLX model
super model install mlx-community/Llama-3.2-3B-Instruct-4bit --backend mlx

# Install HuggingFace model
super model install microsoft/phi-1_5 --backend huggingface
```

## Supported Backends

### Ollama
- **Best for:** Local models, easy setup
- **Models:** All Ollama-compatible models
- **Installation:** `ollama pull <model>`
- **Execution:** `ollama run <model> <prompt>`

### MLX
- **Best for:** Apple Silicon optimization
- **Models:** MLX-community models
- **Installation:** Downloads from HuggingFace Hub
- **Execution:** Direct MLX-LM inference

### HuggingFace
- **Best for:** Wide model selection, research
- **Models:** All HuggingFace models
- **Installation:** Downloads from HuggingFace Hub
- **Execution:** Direct transformers pipeline

### LM Studio
- **Best for:** Desktop GUI, server mode
- **Models:** LM Studio compatible models
- **Installation:** Manual via LM Studio app
- **Execution:** Server mode only (not supported for direct execution)

## Model Execution

### Single Prompt Mode

Run a single prompt against a model:

```bash
# Basic usage
super model run <model_name> "<prompt>"

# Examples
super model run llama3.2:3b "Write a Python function to calculate fibonacci"
super model run mlx-community/phi-2 "Explain quantum computing in simple terms"
super model run microsoft/phi-1_5 "Write a simple calculator program"
```

### Interactive Mode

Start an interactive conversation:

```bash
super model run <model_name> "" --interactive
```

**Interactive Commands:**
- `quit` or `exit`: End the session
- `clear`: Clear conversation history
- `Ctrl+C`: Interrupt current generation

### Generation Parameters

Control model behavior:

```bash
# Set temperature (creativity)
super model run llama3.2:3b "Write a story" --temperature 0.9

# Set max tokens (response length)
super model run llama3.2:3b "Explain AI" --max-tokens 500

# Combine parameters
super model run llama3.2:3b "Write a poem" --temperature 0.8 --max-tokens 200
```

## Auto-Installation

Models are automatically installed when they're not found:

```bash
# This will auto-install the model if not found
super model run mlx-community/Llama-3.2-3B-Instruct-4bit "Hello world"
```

**Auto-Installation Features:**
- **Backend detection:** Automatically determines the correct backend
- **Progress feedback:** Shows download progress
- **Error handling:** Provides clear error messages
- **Cache management:** Handles model caching efficiently

## Model Management Commands

### List Models

```bash
# List all installed models
super model list

# List models by backend
super model list --backend ollama
super model list --backend mlx
super model list --backend huggingface

# Filter by size
super model list --size small

# Filter by task
super model list --task code
```

### Remove Models

```bash
# Remove from specific backend
super model remove llama3.2:3b --backend ollama

# Remove from all backends
super model remove llama3.2:3b --all-backends
```

**Note**: LM Studio models cannot be removed via CLI and require manual deletion:
1. Open LM Studio application
2. Go to 'My Models' section  
3. Right-click on the model and select 'Delete'
4. Or manually delete from: `~/.cache/lm-studio/models/`

### Get Model Information

```bash
# Get detailed model info
super model info llama3.2:3b

# Get info for specific backend
super model info microsoft/phi-1_5 --backend huggingface
```

### Refresh Cache

```bash
# Refresh model cache
super model refresh
```

## Backend-Specific Features

### Ollama Backend

**Installation:**
```bash
# Install via Ollama
ollama pull llama3.2:3b

# Or use SuperOptiX
super model install llama3.2:3b --backend ollama
```

**Execution:**
```bash
# Direct execution
super model run llama3.2:3b "Write code"
```

### MLX Backend

**Installation:**
```bash
# Auto-installation
super model run mlx-community/phi-2 "Hello"

# Manual installation
super model install mlx-community/phi-2 --backend mlx
```

**Execution:**
```bash
# Direct execution (Apple Silicon optimized)
super model run mlx-community/phi-2 "Write a function"
```

### HuggingFace Backend

**Installation:**
```bash
# Auto-installation
super model run microsoft/phi-1_5 "Hello"

# Manual installation
super model install microsoft/phi-1_5 --backend huggingface
```

**Execution:**
```bash
# Direct execution (uses transformers pipeline)
super model run microsoft/phi-1_5 "Write code"
```

## Advanced Usage

### DSPy Integration

Create DSPy clients for advanced AI workflows:

```bash
# Create DSPy client
super model dspy ollama/llama3.2:3b --temperature 0.7

# Use in Python
from superoptix.models.manager import SuperOptiXModelManager
manager = SuperOptiXModelManager()
client = manager.create_dspy_client("ollama/llama3.2:3b")
```

### Server Mode

Start model servers for API access:

```bash
# Start MLX server
super model server mlx mlx-community/phi-2 --port 8000

# Start HuggingFace server
super model server huggingface microsoft/phi-1_5 --port 8001
```

### Model Discovery

Discover available models:

```bash
# Interactive discovery
super model discover

# Show installation guides
super model guide

# List backends
super model backends
```

### Model Conversion and Quantization

Convert and quantize models for MLX backend:

```bash
# Convert HuggingFace model to MLX format
super model convert microsoft/phi-2 --quantize --bits 4

# Quantize existing MLX model
super model quantize my-model --bits 4 --output my-model-q4

# Dequantize a quantized model
super model quantize my-model-q4 --dequantize --output my-model-dequantized
```

**Note:** These commands are experimental and require MLX backend to be available.

## Troubleshooting

### Common Issues

**Model not found:**
```bash
# Check if model exists
super model list --backend ollama

# Try auto-installation
super model run <model_name> "test"
```

**Installation fails:**
```bash
# Check backend availability
super model backends

# Refresh cache
super model refresh

# Try manual installation
super model install <model_name> --backend <backend>
```

**Execution errors:**
```bash
# Check model status
super model info <model_name>

# Try different backend
super model run <model_name> "test" --backend <backend>
```

### Performance Tips

1. **Use appropriate backends:**
   - Ollama: Good for local models
   - MLX: Best for Apple Silicon
   - HuggingFace: Wide model selection

2. **Model size considerations:**
   - Small models: Faster, less accurate
   - Large models: Slower, more accurate

3. **Memory management:**
   - Close unused models
   - Use `super model refresh` to clean cache

## Examples

### Code Generation

```bash
# Generate Python function
super model run llama3.2:3b "Write a Python function to sort a list"

# Generate JavaScript code
super model run microsoft/phi-1_5 "Write a JavaScript function to validate email"
```

### Content Creation

```bash
# Write a blog post
super model run llama3.2:3b "Write a blog post about AI trends"

# Create a story
super model run mlx-community/phi-2 "Write a short story about a robot"
```

### Analysis

```bash
# Analyze text
super model run microsoft/phi-1_5 "Analyze this text: [your text here]"

# Explain concept
super model run llama3.2:3b "Explain machine learning in simple terms"
```

## Best Practices

1. **Start with auto-installation:** Let SuperOptiX handle model setup
2. **Use appropriate models:** Match model size to your needs
3. **Experiment with parameters:** Adjust temperature and max_tokens
4. **Use interactive mode:** For complex conversations
5. **Monitor performance:** Check response times and quality

## Next Steps

- Explore [Agent Development](../guides/agent-development.md) for building AI agents
- Learn about [Orchestra Development](../guides/orchestra-development.md) for multi-agent systems
- Check out [Tool Development](../guides/tool-development.md) for custom tools 