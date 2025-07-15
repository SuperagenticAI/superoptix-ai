# 🔌 SuperOptiX Python API Reference

Welcome to the comprehensive Python API reference for SuperOptiX. This documentation covers all public classes, functions, and modules available in the SuperOptiX framework.

## 📚 Complete API Reference

| Module | Description | Key Classes/Functions | Documentation |
|--------|-------------|----------------------|---------------|
| **🎯 Core Pipeline** | Base pipeline classes and utilities | `SuperOptixPipeline`, `BasePipeline`, `PipelineUtils`, `RAGMixin` | [Core Pipeline](core.md) |
| **🤖 Model Management** | Model intelligence and backend management | `SuperOptiXModelManager`, `ModelRegistry`, `TierSystem`, `ModelConfig` | [Model Management](models.md) |
| **🧠 Memory Systems** | Agent memory and context management | `AgentMemory`, `EpisodicMemory`, `LongTermMemory`, `ShortTermMemory` | [Memory Systems](memory.md) |
| **🛠️ Tools Framework** | Tool system and built-in tools | `BaseTool`, `ToolRegistry`, `ToolFactory`, `BuiltinTools` | [Tools Framework](tools.md) |
| **📝 SuperSpec DSL** | DSL parser, validator, and generator | `SuperSpecXParser`, `SuperSpecXValidator`, `SuperSpecXGenerator` | [SuperSpec DSL](superspec.md) |
| **📊 Observability** | Tracing, debugging, and monitoring | `SuperOptixTracer`, `ObservabilityDashboard`, `Debugger` | [Observability](observability.md) |
| **🏃 Runners** | DSPy and orchestra runners | `DSPyRunner`, `OrchestraRunner`, `PipelineRunner` | [Runners](runners.md) |
| **💻 CLI Commands** | Command-line interface reference | `main`, `agent`, `model`, `marketplace`, `observability` | [CLI Commands](cli.md) |

## 🚀 Quick Navigation

## 🚀 Getting Started

```python
import superoptix

# Core pipeline
from superoptix.core import SuperOptixPipeline

# Model management
from superoptix.models import SuperOptiXModelManager

# Memory systems
from superoptix.memory import AgentMemory

# Tools
from superoptix.tools import BaseTool, get_default_tools

# SuperSpec DSL
from superoptix.superspec import SuperSpecXParser, SuperSpecXValidator

# Observability
from superoptix.observability import SuperOptixTracer, ObservabilityDashboard
```

## 📦 Package Structure

```
superoptix/
├── core/                 # Core pipeline and utilities
├── models/              # Model intelligence system
├── memory/              # Memory management
├── tools/               # Tool framework
├── superspec/          # DSL parser and generator
├── observability/       # Tracing and monitoring
├── runners/             # DSPy and orchestra runners
├── cli/                 # Command-line interface
├── validators/          # Validation utilities
├── ui/                  # User interface components
├── adapters/            # External system adapters
└── config/              # Configuration management
```

## 🔍 Detailed API Listing

### **🎯 Core Pipeline (`superoptix.core`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `SuperOptixPipeline` | Base pipeline class for all agents | Inherit to create custom agents |
| `BasePipeline` | Abstract base class for pipeline implementations | Base class for pipeline abstractions |
| `PipelineUtils` | Utility functions for pipeline management | Helper functions for pipeline operations |
| `RAGMixin` | RAG integration mixin for pipelines | Add RAG capabilities to pipelines |
| `Validation` | Pipeline validation utilities | Validate pipeline configurations |

### **🤖 Model Management (`superoptix.models`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `SuperOptiXModelManager` | Main model management class | Central model management interface |
| `ModelRegistry` | Model registration and discovery | Register and discover available models |
| `TierSystem` | Tier-based model selection | Select models based on tier requirements |
| `ModelConfig` | Model configuration management | Configure model parameters and settings |
| `ModelUtils` | Model utility functions | Helper functions for model operations |
| `BaseModels` | Base model classes | Base classes for model implementations |
| **Backends:** | | |
| `OllamaBackend` | Ollama integration | Local Ollama model inference |
| `MLXBackend` | Apple MLX integration | Apple Silicon optimized inference |
| `HuggingFaceBackend` | HuggingFace integration | HuggingFace model inference |
| `LMStudioBackend` | LM Studio integration | LM Studio model inference |

### **🧠 Memory Systems (`superoptix.memory`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `AgentMemory` | Main memory management class | Central memory management interface |
| `EpisodicMemory` | Episode-based memory storage | Store conversation episodes |
| `LongTermMemory` | Persistent memory storage | Store long-term knowledge |
| `ShortTermMemory` | Session-based memory | Store session-specific information |
| `ContextManager` | Context management utilities | Manage context retrieval and storage |
| `MemoryBackends` | Storage backend implementations | SQLite, Redis, file-based storage |

### **🛠️ Tools Framework (`superoptix.tools`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `BaseTool` | Base class for all tools | Inherit to create custom tools |
| `ToolRegistry` | Tool registration and discovery | Register and discover available tools |
| `ToolFactory` | Tool creation factory | Create tools dynamically |
| `BuiltinTools` | Built-in tool implementations | Pre-built tool collection |
| **Categories:** | | |
| `CoreTools` | Basic utilities | Web search, calculator, file operations |
| `DevelopmentTools` | Development-related tools | Git, API testing, code review |
| `FinanceTools` | Financial calculations | Currency conversion, tax calculation |
| `HealthcareTools` | Health-related tools | BMI calculator, medical lookups |
| `MarketingTools` | Marketing and analytics | SEO analysis, email validation |
| `LegalTools` | Legal research and analysis | Legal lookups, contract analysis |
| `EducationTools` | Educational tools | Grade calculation, study scheduling |

### **📝 SuperSpec DSL (`superoptix.superspec`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `SuperSpecXParser` | DSL parser implementation | Parse SuperSpec specifications |
| `SuperSpecXValidator` | DSL validation utilities | Validate DSL specifications |
| `SuperSpecXGenerator` | Code generation from DSL | Generate code from DSL specs |
| `Schema` | DSL schema definitions | Define DSL structure and rules |
| `DSL` | DSL specification and grammar | DSL language specification |

### **📊 Observability (`superoptix.observability`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `SuperOptixTracer` | Main tracing implementation | Trace agent execution |
| `ObservabilityDashboard` | Web-based monitoring dashboard | Monitor agent performance |
| `Debugger` | Interactive debugging tools | Debug agent behavior |
| `Callbacks` | Tracing callbacks and hooks | Custom tracing callbacks |
| `EnhancedAdapter` | Enhanced DSPy adapter for tracing | Enhanced DSPy integration |

### **🏃 Runners (`superoptix.runners`)**
| Class/Function | Description | Usage |
|----------------|-------------|-------|
| `DSPyRunner` | DSPy pipeline execution | Execute DSPy pipelines |
| `OrchestraRunner` | Multi-agent orchestration | Orchestrate multiple agents |
| `PipelineRunner` | Pipeline execution utilities | Execute custom pipelines |

### **💻 CLI (`superoptix.cli`)**
| Command | Description | Usage |
|---------|-------------|-------|
| `main` | Main CLI entry point | Entry point for all CLI commands |
| `agent` | Agent management commands | Create, compile, evaluate agents |
| `model` | Model management commands | Install, list, configure models |
| `marketplace` | Marketplace commands | Browse and install from marketplace |
| `observability` | Observability commands | Start dashboard, view traces |
| `orchestra` | Orchestra management commands | Create and run orchestras |
| `superspec` | SuperSpec DSL commands | Generate and validate specs |

### **🔧 Additional Modules**
| Module | Description | Usage |
|--------|-------------|-------|
| `validators` | Validation utilities and frameworks | Validate configurations and data |
| `ui` | User interface components | Web-based UI components |
| `adapters` | External system adapters | Integrate with external systems |
| `config` | Configuration management | Manage application configuration |

## 🎯 Core Concepts

### **Pipeline Architecture**
SuperOptiX uses a pipeline-based architecture where agents inherit from `SuperOptixPipeline` and implement DSPy signatures and forward logic.

### **Model Intelligence**
The model management system provides unified access to multiple backends (Ollama, MLX, HuggingFace, LM Studio) with automatic discovery and configuration.

### **Memory Systems**
Multi-layered memory architecture supporting episodic, semantic, and working memory with various backend storage options.

### **Tool Framework**
Modular tool system organized by industry categories with factory patterns for easy tool creation and management.

### **SuperSpec DSL**
Declarative specification language for defining agent behavior, capabilities, and evaluation criteria.

### **Observability**
Comprehensive tracing, debugging, and monitoring capabilities for production deployment.

---

*This API reference provides detailed documentation for all SuperOptiX components. Use the navigation above to explore specific modules.* 🚀 