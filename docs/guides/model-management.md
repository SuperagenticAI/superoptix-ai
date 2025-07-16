# 🧠 Model Management Guide

> **Master SuperOptiX's current model management capabilities and tier system**

---

## 🎯 Overview

SuperOptiX provides a **unified model management system** that handles local language models across multiple backends. This guide covers the current implementation and how to effectively manage models within the SuperOptiX ecosystem.

### 🧠 Current Capabilities

- **📋 Model Listing**: List and filter installed models
- **🔍 Model Discovery**: Get guidance on available models and backends
- **📦 Model Installation**: Install models across different backends
- **ℹ️ Model Information**: Get detailed model information
- **🖥️ Server Management**: Start local model servers
- **🧠 DSPy Integration**: Create DSPy clients for models
- **🔧 Backend Status**: Check backend availability and status

---

## 🏗️ Model Tier System

SuperOptiX uses a **progressive tier system** that determines agent capabilities and features:

### 🎭 **Oracle Tier (Free)**
- **Basic question-answering** with Chain of Thought reasoning
- **Simple evaluation** (exact match, F1)
- **Basic optimization** (BootstrapFewShot)
- **Sequential task orchestration** only
- **No tools, memory, or RAG**

### 🧞 **Genie Tier (Free)**
- **All Oracle capabilities** plus:
- **Tool integration** and ReAct reasoning
- **RAG (knowledge retrieval)** capabilities
- **Agent memory** (short-term and episodic)
- **Basic streaming** responses
- **Sequential orchestration** only

### 🚀 **Higher Tiers (Enterprise)**
- **Parallel execution** strategies
- **Kubernetes-style orchestration**
- **Advanced enterprise features**
- **Production-grade scaling**

---

## 📋 Model Listing & Discovery

### 1. **List Installed Models**

```bash
# List all installed models
super model list

# List all available models (including uninstalled)
super model list --all

# Filter by backend
super model list --backend ollama
super model list --backend mlx
super model list --backend huggingface
super model list --backend lmstudio

# Filter by size
super model list --size tiny
super model list --size small
super model list --size medium
super model list --size large

# Filter by task
super model list --task chat
super model list --task code
super model list --task reasoning
super model list --task embedding

# Combine filters
super model list --backend ollama --size small --task chat

# Verbose information
super model list --verbose
```

### 2. **Model Discovery**

```bash
# Get comprehensive discovery guide
super model discover

# Get detailed installation guide
super model guide
```

---

## 📦 Model Installation

### 1. **Install Models by Backend**

```bash
# Install Ollama models (default backend)
super model install llama3.2:3b
super model install llama3.2:8b
super model install llama3.2:70b

# Install MLX models
super model install -b mlx mlx-community/phi-2
super model install -b mlx mlx-community/Llama-3.2-3B-Instruct-4bit

# Install HuggingFace models
super model install -b huggingface microsoft/Phi-4
super model install -b huggingface microsoft/DialoGPT-small

# Install LM Studio models
super model install -b lmstudio llama-3.2-1b-instruct
super model install -b lmstudio your-model-name

# Force reinstall if needed
super model install llama3.2:3b --force
```

### 2. **Backend-Specific Setup**

#### **🦙 Ollama (Recommended for Beginners)**
```bash
# Install Ollama
curl -fsSL https://ollama.ai/install.sh | sh

# Start Ollama (runs automatically)
ollama serve

# Install models
super model install llama3.2:3b
super model install llama3.2:8b
```

#### **🍎 MLX (Apple Silicon)**
```bash
# Install MLX dependencies
pip install mlx-lm

# Or install with SuperOptiX
pip install "superoptix[mlx]"

# Install models
super model install -b mlx mlx-community/phi-2
super model install -b mlx mlx-community/Llama-3.2-3B-Instruct-4bit
```

#### **🤗 HuggingFace (Advanced Users)**
```bash
# Install HuggingFace dependencies
pip install transformers torch fastapi uvicorn

# Or install with SuperOptiX
pip install "superoptix[huggingface]"

# Install models
super model install -b huggingface microsoft/Phi-4
super model install -b huggingface microsoft/DialoGPT-small
```

#### **🎮 LM Studio (Windows Users)**
```bash
# Download LM Studio from https://lmstudio.ai
# Install and launch LM Studio
# Download a model through the interface
# Start the server (default port: 1234)

# Models are managed through LM Studio app
super model install -b lmstudio your-model-name
```

---

## 🖥️ Server Management

### 1. **Start Model Servers**

```bash
# Start MLX server
super model server mlx phi-2 --port 8000
super model server mlx mlx-community/Llama-3.2-3B-Instruct-4bit --port 8000

# Start HuggingFace server
super model server huggingface microsoft/Phi-4 --port 8001
super model server huggingface microsoft/DialoGPT-small --port 8001

# Start LM Studio server
super model server lmstudio llama-3.2-1b-instruct --port 1234
super model server lmstudio your-model-name --port 1234
```

### 2. **Server Backend Details**

| Backend | Server Required | Default Port | Platform | Auto-Start |
|---------|----------------|--------------|----------|------------|
| 🦙 Ollama | No | 11434 | All | Yes |
| 🍎 MLX | Yes | 8000 | Apple Silicon | No |
| 🤗 HuggingFace | Yes | 8001 | All | No |
| 🎮 LM Studio | Yes | 1234 | Windows/macOS | No |

---

## 🧠 DSPy Integration

### 1. **Create DSPy Clients**

```bash
# Create Ollama DSPy client
super model dspy ollama/llama3.2:3b
super model dspy ollama/llama3.2:8b

# Create MLX DSPy client
super model dspy mlx/phi-2
super model dspy mlx-community/Llama-3.2-3B-Instruct-4bit

# Create HuggingFace DSPy client
super model dspy huggingface/microsoft/Phi-4
super model dspy microsoft/Phi-4

# Create LM Studio DSPy client
super model dspy lmstudio/llama-3.2-1b-instruct
super model dspy lmstudio/your-model-name

# DSPy client with custom parameters
super model dspy ollama/llama3.2:3b --temperature 0.7 --max-tokens 2048
```

### 2. **DSPy Integration Examples**

```python
# In your agent playbook or pipeline
from dspy import Predict
from superoptix.models.backends.ollama import OllamaClient

# Create the client
client = OllamaClient(
    model="llama3.2:3b",
    temperature=0.7,
    max_tokens=2048
)

# Use with DSPy modules
predictor = Predict(client)

# Example usage
response = predictor("Explain quantum computing in simple terms")
print(response)
```

---

## 📊 Model Information

### 1. **Get Model Details**

```bash
# Get model information
super model info llama3.2:3b
super model info mlx-community/phi-2
super model info microsoft/Phi-4
super model info llama-3.2-1b-instruct
```

### 2. **Check Backend Status**

```bash
# Check all backends
super model backends
```

---



## 🔧 Configuration Management

### 1. **Model Configuration in Playbooks**

```yaml
# In your agent playbook
spec:
  language_model:
    provider: "ollama"  # or "mlx", "huggingface", "lmstudio"
    model: "llama3.2:3b"
    temperature: 0.7
    max_tokens: 2048
    api_base: "http://localhost:11434"  # for MLX/HuggingFace servers
```

### 2. **Backend-Specific Configuration**

#### **Ollama Configuration**
```yaml
language_model:
  provider: "ollama"
  model: "llama3.2:3b"
  temperature: 0.7
  max_tokens: 2048
  # No api_base needed - uses default localhost:11434
```

#### **MLX Configuration**
```yaml
language_model:
  provider: "mlx"
  model: "mlx-community/phi-2"
  temperature: 0.7
  max_tokens: 2048
  api_base: "http://localhost:8000"  # MLX server port
```

#### **HuggingFace Configuration**
```yaml
language_model:
  provider: "huggingface"
  model: "microsoft/Phi-4"
  temperature: 0.7
  max_tokens: 2048
  api_base: "http://localhost:8001"  # HuggingFace server port
```

#### **LM Studio Configuration**
```yaml
language_model:
  provider: "lmstudio"
  model: "llama-3.2-1b-instruct"
  temperature: 0.7
  max_tokens: 2048
  api_base: "http://localhost:1234"  # LM Studio server port
```

---

## 🚨 Troubleshooting

### Common Issues

#### **Model Not Found**
```bash
# Check available models
super model list --all

# Use correct model name
super model install llama3.2:3b  # ✅ Correct
super model install llama3.2     # ❌ Wrong
```

#### **Server Connection Failed**
```bash
# Check if server is running
# For Ollama: ollama serve
# For MLX: super model server mlx phi-2 --port 8000
# For LM Studio: Start in LM Studio app
# For HuggingFace: super model server huggingface model --port 8001
```

#### **Port Already in Use**
```bash
# Use different port
super model server mlx phi-2 --port 8001
super model server huggingface microsoft/Phi-4 --port 8002
```

#### **Apple Silicon Required**
```bash
# Use Ollama instead
super model install llama3.2:3b
super model dspy ollama/llama3.2:3b
```

#### **Missing Python Packages**
```bash
# Install MLX dependencies
pip install mlx-lm

# Install HuggingFace dependencies
pip install transformers torch fastapi uvicorn

# Or install with SuperOptiX extras
pip install "superoptix[mlx]"
pip install "superoptix[huggingface]"
```

---

## 🎯 Best Practices

### 1. **Model Selection**

- **Start with Ollama**: Easiest for beginners, works on all platforms
- **Use MLX on Apple Silicon**: Best performance for Apple Silicon Macs
- **Choose HuggingFace for advanced use**: Maximum flexibility and model variety
- **Use LM Studio on Windows**: Good GUI interface for Windows users

### 2. **Server Management**

- **Ollama**: No manual server management needed
- **MLX/HuggingFace**: Start servers when needed, use different ports
- **LM Studio**: Manage through the application interface
- **Monitor resources**: Keep an eye on memory usage

### 3. **DSPy Integration**

- **Test models first**: Use `super model info` to verify installation
- **Start with simple prompts**: Test basic functionality before complex tasks
- **Monitor performance**: Check response times and quality
- **Use appropriate parameters**: Adjust temperature and max_tokens for your use case

### 4. **Tier Compliance**

- **Oracle agents**: Use any model, no special requirements
- **Genie agents**: Models should support tool calling and reasoning
- **Higher tiers**: Enterprise features require specific model capabilities

---

## 🔗 Related Resources

- [Model Intelligence Guide](./model-intelligence.md) - Advanced model management features
- [Cloud Inference Guide](./cloud-inference.md) - Cloud provider integration guides
- [Agent Development Guide](./agent-development.md) - Using models with agents
- [CLI Reference](../reference/cli.md) - Complete command reference
- [Troubleshooting Guide](../troubleshooting.md) - Common issues and solutions

---

*Ready to manage your models effectively? Start with `super model discover` to explore available models and backends! 🚀* 