# 🧠 Model Management API

The model management system provides unified access to multiple language model backends with automatic discovery, configuration, and DSPy integration.

## SuperOptiXModelManager

The main model manager class that handles model operations across different backends.

### Constructor

```python
class SuperOptiXModelManager:
    def __init__(self, config_dir: Optional[str] = None)
```

**Parameters:**
- `config_dir` (str, optional): Configuration directory path

### Core Methods

#### list_models()
```python
def list_models(
    self,
    backend: Optional[SuperOptiXBackendType] = None,
    size: Optional[SuperOptiXModelSize] = None,
    task: Optional[SuperOptiXModelTask] = None,
    installed_only: bool = True,
    verbose: bool = False
) -> List[SuperOptiXModelInfo]:
    """List models with optional filtering."""
```

**Parameters:**
- `backend` (SuperOptiXBackendType, optional): Filter by backend type
- `size` (SuperOptiXModelSize, optional): Filter by model size
- `task` (SuperOptiXModelTask, optional): Filter by model task
- `installed_only` (bool): Show only installed models - defaults to True
- `verbose` (bool): Show detailed information - defaults to False

**Returns:** List of model information objects

#### install_model()
```python
def install_model(
    self,
    model_name: str,
    backend: SuperOptiXBackendType = SuperOptiXBackendType.OLLAMA,
    force: bool = False,
    **kwargs
) -> SuperOptiXModelInfo:
    """Install a model on the specified backend."""
```

**Parameters:**
- `model_name` (str): Name of the model to install
- `backend` (SuperOptiXBackendType): Target backend - defaults to OLLAMA
- `force` (bool): Force reinstall if already installed - defaults to False
- `**kwargs` (Any): Additional installation parameters

**Returns:** Model information object

#### get_model_info()
```python
def get_model_info(
    self,
    model_name: str,
    backend: SuperOptiXBackendType = SuperOptiXBackendType.OLLAMA
) -> SuperOptiXModelInfo:
    """Get detailed information about a model."""
```

**Parameters:**
- `model_name` (str): Name of the model
- `backend` (SuperOptiXBackendType): Backend type - defaults to OLLAMA

**Returns:** Detailed model information object

#### start_server()
```python
def start_server(
    self,
    model_name: str,
    backend: SuperOptiXBackendType = SuperOptiXBackendType.OLLAMA,
    port: int = None,
    **kwargs
) -> Dict[str, Any]:
    """Start a model server for the specified model."""
```

**Parameters:**
- `model_name` (str): Name of the model to serve
- `backend` (SuperOptiXBackendType): Backend type - defaults to OLLAMA
- `port` (int, optional): Port number for the server
- `**kwargs` (Any): Additional server configuration

**Returns:** Server information dictionary

#### create_dspy_client()
```python
def create_dspy_client(
    self,
    model_name: str,
    backend: SuperOptiXBackendType = SuperOptiXBackendType.OLLAMA,
    **kwargs
) -> dspy.LM:
    """Create a DSPy language model client."""
```

**Parameters:**
- `model_name` (str): Name of the model
- `backend` (SuperOptiXBackendType): Backend type - defaults to OLLAMA
- `**kwargs` (Any): Additional client configuration

**Returns:** DSPy language model client

#### check_backend_status()
```python
def check_backend_status(
    self,
    backend: SuperOptiXBackendType
) -> SuperOptiXBackendInfo:
    """Check the status of a backend."""
```

**Parameters:**
- `backend` (SuperOptiXBackendType): Backend to check

**Returns:** Backend status information

## Data Classes

### SuperOptiXModelInfo

```python
@dataclass
class SuperOptiXModelInfo:
    name: str
    backend: SuperOptiXBackendType
    size: SuperOptiXModelSize
    task: SuperOptiXModelTask
    status: SuperOptiXModelStatus
    installed: bool
    file_size: Optional[int]
    download_url: Optional[str]
    description: Optional[str]
    tags: List[str]
    parameters: Optional[int]
    context_length: Optional[int]
    last_updated: Optional[datetime]
```

### SuperOptiXBackendInfo

```python
@dataclass
class SuperOptiXBackendInfo:
    backend: SuperOptiXBackendType
    available: bool
    version: Optional[str]
    models_count: int
    server_running: bool
    server_url: Optional[str]
    error_message: Optional[str]
```

### SuperOptiXModelConfig

```python
@dataclass
class SuperOptiXModelConfig:
    name: str
    backend: SuperOptiXBackendType
    temperature: float = 0.1
    max_tokens: int = 2000
    top_p: float = 1.0
    frequency_penalty: float = 0.0
    presence_penalty: float = 0.0
    stop_sequences: List[str] = None
    api_base: Optional[str] = None
    api_key: Optional[str] = None
```

## Enums

### SuperOptiXBackendType

```python
class SuperOptiXBackendType(Enum):
    OLLAMA = "ollama"
    MLX = "mlx"
    HUGGINGFACE = "huggingface"
    LMSTUDIO = "lmstudio"
```

### SuperOptiXModelSize

```python
class SuperOptiXModelSize(Enum):
    TINY = "tiny"      # < 1B parameters
    SMALL = "small"    # 1B - 7B parameters
    MEDIUM = "medium"  # 7B - 30B parameters
    LARGE = "large"    # > 30B parameters
```

### SuperOptiXModelTask

```python
class SuperOptiXModelTask(Enum):
    CHAT = "chat"
    CODE = "code"
    REASONING = "reasoning"
    EMBEDDING = "embedding"
    MULTIMODAL = "multimodal"
```

### SuperOptiXModelStatus

```python
class SuperOptiXModelStatus(Enum):
    AVAILABLE = "available"
    INSTALLED = "installed"
    DOWNLOADING = "downloading"
    ERROR = "error"
    NOT_FOUND = "not_found"
```

## Utility Functions

### get_superoptix_system_info()
```python
def get_superoptix_system_info() -> Dict[str, Any]:
    """Get comprehensive system information."""
```

**Returns:** Dictionary with system information including OS, Python version, available backends, etc.

### format_size()
```python
def format_size(size_bytes: int) -> str:
    """Format file size in human-readable format."""
```

**Parameters:**
- `size_bytes` (int): Size in bytes

**Returns:** Formatted size string (e.g., "1.5 GB")

### parse_superoptix_model_name()
```python
def parse_superoptix_model_name(model_name: str) -> Dict[str, Any]:
    """Parse a SuperOptiX model name into components."""
```

**Parameters:**
- `model_name` (str): Model name to parse

**Returns:** Dictionary with parsed components

### get_superoptix_model_discovery_guide()
```python
def get_superoptix_model_discovery_guide() -> str:
    """Get a comprehensive guide for model discovery."""
```

**Returns:** Formatted guide text

### validate_superoptix_model_compatibility()
```python
def validate_superoptix_model_compatibility(
    model_name: str,
    backend: SuperOptiXBackendType
) -> bool:
    """Validate if a model is compatible with a backend."""
```

**Parameters:**
- `model_name` (str): Model name to validate
- `backend` (SuperOptiXBackendType): Backend to check compatibility with

**Returns:** True if compatible, False otherwise

## Configuration Functions

### get_superoptix_global_config()
```python
def get_superoptix_global_config() -> Dict[str, Any]:
    """Get global SuperOptiX configuration."""
```

**Returns:** Global configuration dictionary

### save_superoptix_global_config()
```python
def save_superoptix_global_config(config: Dict[str, Any]) -> None:
    """Save global SuperOptiX configuration."""
```

**Parameters:**
- `config` (Dict[str, Any]): Configuration to save

### get_superoptix_project_config()
```python
def get_superoptix_project_config(project_path: str) -> Dict[str, Any]:
    """Get project-specific configuration."""
```

**Parameters:**
- `project_path` (str): Path to the project

**Returns:** Project configuration dictionary

### save_superoptix_project_config()
```python
def save_superoptix_project_config(
    project_path: str,
    config: Dict[str, Any]
) -> None:
    """Save project-specific configuration."""
```

**Parameters:**
- `project_path` (str): Path to the project
- `config` (Dict[str, Any]): Configuration to save

## Example Usage

```python
from superoptix.models import (
    SuperOptiXModelManager,
    SuperOptiXBackendType,
    SuperOptiXModelSize,
    SuperOptiXModelTask
)

# Initialize model manager
manager = SuperOptiXModelManager()

# List installed models
models = manager.list_models(installed_only=True)
for model in models:
    print(f"{model.name} ({model.backend.value}) - {model.size.value}")

# List all available models
all_models = manager.list_models(installed_only=False, verbose=True)

# Filter by backend and size
ollama_models = manager.list_models(
    backend=SuperOptiXBackendType.OLLAMA,
    size=SuperOptiXModelSize.SMALL
)

# Install a model
model_info = manager.install_model(
    "llama3.2:3b",
    backend=SuperOptiXBackendType.OLLAMA
)

# Get model information
info = manager.get_model_info("llama3.2:3b")

# Start a model server
server_info = manager.start_server(
    "llama3.2:3b",
    port=8000
)

# Create DSPy client
lm = manager.create_dspy_client(
    "llama3.2:3b",
    temperature=0.2,
    max_tokens=1000
)

# Check backend status
status = manager.check_backend_status(SuperOptiXBackendType.OLLAMA)
print(f"Ollama available: {status.available}")
print(f"Models installed: {status.models_count}")

# Get system information
system_info = get_superoptix_system_info()
print(f"OS: {system_info['os']}")
print(f"Python: {system_info['python_version']}")

# Get discovery guide
guide = get_superoptix_model_discovery_guide()
print(guide)
```

## Backend-Specific Configuration

### Ollama Configuration

```python
ollama_config = {
    "api_base": "http://localhost:11434",
    "timeout": 30,
    "retry_attempts": 3
}
```

### MLX Configuration

```python
mlx_config = {
    "api_base": "http://localhost:8000",
    "model_path": "/path/to/models",
    "device": "cpu"  # or "gpu"
}
```

### HuggingFace Configuration

```python
huggingface_config = {
    "api_base": "http://localhost:8001",
    "trust_remote_code": True,
    "device_map": "auto"
}
```

### LM Studio Configuration

```python
lmstudio_config = {
    "api_base": "http://localhost:1234",
    "timeout": 60,
    "stream": False
}
``` 