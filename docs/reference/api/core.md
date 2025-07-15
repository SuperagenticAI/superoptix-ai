# 🔧 Core Pipeline API

The core pipeline module provides the foundation for building SuperOptiX agents with automatic setup of tracing, tools, memory, and evaluation.

## SuperOptixPipeline

The main base class for all SuperOptiX agents. Inherits from `dspy.Module` and provides automatic framework setup.

### Constructor

```python
class SuperOptixPipeline(dspy.Module, ABC, metaclass=SuperOptixMeta):
    def __init__(self, config: Optional[Dict[str, Any]] = None)
```

**Parameters:**
- `config` (Dict[str, Any], optional): Configuration dictionary with pipeline settings

**Configuration Options:**
- `tier_level` (str): Agent tier ("oracles", "genies", "sage") - defaults to "oracles"
- `model` (str): Model name for the tier - auto-configured based on tier
- `provider` (str): Model provider ("ollama", "mlx", "huggingface", "lmstudio") - defaults to "ollama"
- `api_base` (str): API base URL for model provider
- `temperature` (float): Model temperature - defaults to 0.1
- `max_tokens` (int): Maximum tokens for responses - defaults to 2000
- `enable_memory` (bool): Enable memory system - defaults to False
- `memory_config` (dict): Memory system configuration
- `enable_external_tracing` (bool): Enable external tracing - defaults to False
- `traces_dir` (str): Directory for trace storage - defaults to "traces"

### Abstract Methods

#### get_signature()
```python
@abstractmethod
def get_signature(self) -> dspy.Signature:
    """Return the DSPy signature for this agent."""
```

**Returns:** DSPy signature defining the agent's input/output structure

#### forward()
```python
@abstractmethod
def forward(self, **kwargs) -> dspy.Prediction:
    """Implement the core reasoning logic."""
```

**Parameters:** `**kwargs` - Input parameters as defined by the signature
**Returns:** DSPy prediction with the agent's response

#### get_agent_name()
```python
@abstractmethod
def get_agent_name(self) -> str:
    """Return the agent name for tracing/logging."""
```

**Returns:** String identifier for the agent

### Optional Customization Methods

#### setup()
```python
def setup(self) -> None:
    """Override for custom initialization."""
```

Called after automatic framework setup. Override for custom initialization logic.

#### get_custom_tools()
```python
def get_custom_tools(self) -> List[Any]:
    """Override to add custom tools beyond built-ins."""
    return []
```

**Returns:** List of custom tools to add to the agent

#### get_custom_evaluation_metric()
```python
def get_custom_evaluation_metric(self) -> Optional[callable]:
    """Override to provide custom evaluation beyond semantic F1."""
    return None
```

**Returns:** Custom evaluation function or None for default semantic F1

#### get_bdd_scenarios()
```python
def get_bdd_scenarios(self) -> List[Dict[str, Any]]:
    """Override to provide custom BDD scenarios."""
    return self._load_default_bdd_scenarios()
```

**Returns:** List of BDD scenario dictionaries

### Execution Methods

#### run()
```python
def run(self, query: str = None, **kwargs) -> Dict[str, Any]:
    """Execute the agent with comprehensive tracking."""
```

**Parameters:**
- `query` (str, optional): Input query string
- `**kwargs` (Any): Additional input parameters

**Returns:** Dictionary with execution results, metrics, and traces

#### run_executable_specs()
```python
def run_executable_specs(self, auto_tune: bool = False) -> Dict[str, Any]:
    """Execute BDD specifications as executable specs with auto-tuning."""
```

**Parameters:**
- `auto_tune` (bool): Enable automatic tuning based on failures

**Returns:** Dictionary with specification execution results

#### train()
```python
def train(self, training_data: List[Dict[str, Any]], **kwargs) -> Dict[str, Any]:
    """Train the agent with provided data."""
```

**Parameters:**
- `training_data` (List[Dict[str, Any]]): Training examples
- `**kwargs` (Any): Training configuration

**Returns:** Dictionary with training results and metrics

### Usage Tracking

#### track_usage()
```python
@contextmanager
def track_usage(self):
    """Context manager for tracking usage statistics."""
```

**Usage:**
```python
with self.track_usage():
    result = self.forward(input_data)
```

#### get_usage_summary()
```python
def get_usage_summary(self) -> Dict[str, Any]:
    """Get comprehensive usage statistics."""
```

**Returns:** Dictionary with usage metrics and statistics

## Pipeline Utilities

### TracingMixin

Provides tracing capabilities for pipeline components.

```python
class TracingMixin:
    def trace_operation(self, operation_name: str, category: str):
        """Trace an operation with the observability system."""
```

### ModelSetupMixin

Handles model configuration and setup.

```python
class ModelSetupMixin:
    def setup_model(self, model_name: str, provider: str, **kwargs):
        """Setup language model with specified configuration."""
```

### ToolsMixin

Manages tool registration and execution.

```python
class ToolsMixin:
    def register_tool(self, tool: BaseTool):
        """Register a tool with the pipeline."""
    
    def get_available_tools(self) -> List[BaseTool]:
        """Get list of available tools."""
```

### BDDTestMixin

Provides BDD testing capabilities.

```python
class BDDTestMixin:
    def run_bdd_tests(self, scenarios: List[Dict[str, Any]]) -> Dict[str, Any]:
        """Run BDD test scenarios."""
```

### EvaluationMixin

Handles evaluation and metrics.

```python
class EvaluationMixin:
    def evaluate_prediction(self, prediction: dspy.Prediction, expected: Any) -> float:
        """Evaluate a prediction against expected output."""
```

### UsageTrackingMixin

Tracks usage statistics and performance.

```python
class UsageTrackingMixin:
    def track_usage(self, operation: str, duration: float, **kwargs):
        """Track usage of an operation."""
```

## Example Usage

```python
from superoptix.core import SuperOptixPipeline
import dspy

class MyAgent(SuperOptixPipeline):
    def get_signature(self):
        return dspy.Signature(
            "Given a question, provide a detailed answer",
            question=dspy.InputField(desc="The question to answer"),
            answer=dspy.OutputField(desc="Detailed answer to the question")
        )
    
    def forward(self, question: str) -> dspy.Prediction:
        # Your custom reasoning logic here
        reasoning = self.lm(f"Think step by step about: {question}")
        answer = self.lm(f"Based on the reasoning: {reasoning}, answer: {question}")
        return dspy.Prediction(answer=answer)
    
    def get_agent_name(self) -> str:
        return "my_custom_agent"

# Usage
agent = MyAgent(config={
    "tier_level": "genies",
    "enable_memory": True,
    "temperature": 0.2
})

# Run the agent
result = agent.run(query="What is the capital of France?")

# Run BDD tests
test_results = agent.run_executable_specs()

# Get usage summary
usage = agent.get_usage_summary()
```

## Configuration Reference

### Tier Configuration

| Tier | Default Model | Capabilities |
|------|---------------|--------------|
| oracles | llama3.2:1b | Basic Q&A, simple evaluation |
| genies | llama3.1:8b | Tools, RAG, memory, streaming |
| sage | llama3.1:70b | Advanced features, parallel execution |

### Model Provider Configuration

| Provider | API Base | Auto-Start |
|----------|----------|------------|
| ollama | http://localhost:11434 | Yes |
| mlx | http://localhost:8000 | No |
| huggingface | http://localhost:8001 | No |
| lmstudio | http://localhost:1234 | No |

### Memory Configuration

```python
memory_config = {
    "backend": "sqlite",  # sqlite, redis, file
    "max_episodes": 1000,
    "max_context_length": 4096,
    "retention_days": 30
}
``` 