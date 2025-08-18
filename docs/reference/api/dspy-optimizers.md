# DSPy Optimizers API Reference

This document provides the API reference for using DSPy optimizers in SuperOptiX through the `DSPyOptimizerFactory` and related classes.

## DSPyOptimizerFactory

The `DSPyOptimizerFactory` provides a unified interface for creating and configuring all supported DSPy optimizers.

### Methods

#### `create_optimizer(optimizer_name, params=None, lm_config=None)`

Creates a DSPy optimizer instance with the specified configuration.

**Parameters:**
- `optimizer_name` (str): Name of the optimizer to create
- `params` (dict, optional): Optimizer-specific parameters
- `lm_config` (dict, optional): Language model configuration

**Returns:**
- Configured DSPy optimizer instance

**Example:**
```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

optimizer = DSPyOptimizerFactory.create_optimizer(
    optimizer_name="GEPA",
    params={
        "metric": "answer_exact_match",
        "auto": "light",
        "reflection_lm": "qwen3:8b"
    },
    lm_config={
        "model": "llama3.1:8b",
        "provider": "ollama"
    }
)
```

#### `create_tier_optimized_optimizer(tier, training_data_size, optimizer_config=None)`

Creates an optimizer with settings optimized for the specified agent tier and data size.

**Parameters:**
- `tier` (str): Agent tier ("oracles", "genies", "protocols", "superagents")
- `training_data_size` (int): Number of training examples
- `optimizer_config` (dict, optional): Override default configuration

**Returns:**
- Configured optimizer optimized for the tier

**Example:**
```python
optimizer = DSPyOptimizerFactory.create_tier_optimized_optimizer(
    tier="oracles",
    training_data_size=5
)
```

#### `get_supported_optimizers()`

Returns a list of all supported optimizer names.

**Returns:**
- `list`: Available optimizer names

**Example:**
```python
optimizers = DSPyOptimizerFactory.get_supported_optimizers()
# Returns: ['GEPA', 'SIMBA', 'MIPROv2', 'BootstrapFewShot', ...]
```

## Optimizer Configurations

### GEPA (Graph Enhanced Prompting Algorithm)

Reflective prompt evolution with advanced feedback mechanisms.

#### Configuration Parameters

```python
gepa_params = {
    # Core settings
    "metric": str,                    # Evaluation metric function name
    "auto": str,                      # Budget control: "minimal", "light", "medium", "heavy"
    
    # Reflection settings
    "reflection_lm": str,             # Model for reflection analysis
    "reflection_minibatch_size": int, # Examples per reflection batch
    
    # Optimization controls
    "max_full_evals": int,           # Maximum full evaluations
    "skip_perfect_score": bool,       # Skip if score is perfect
    "add_format_failure_as_feedback": bool,  # Include format errors in feedback
    
    # Advanced settings
    "predictor_level_feedback": bool, # Component-level feedback
    "format_failure_feedback": bool   # Format-specific feedback
}
```

#### Available Metrics

- `answer_exact_match`: Basic exact string matching
- `advanced_math_feedback`: Mathematical reasoning with step validation
- `multi_component_enterprise_feedback`: Business document multi-aspect analysis
- `vulnerability_detection_feedback`: Security analysis with remediation
- `privacy_preservation_feedback`: Data privacy compliance assessment
- `medical_accuracy_feedback`: Healthcare safety validation
- `legal_analysis_feedback`: Legal compliance verification

#### Budget Settings

| Budget | Description | Time | Evaluations | Use Case |
|--------|-------------|------|-------------|----------|
| `minimal` | Fastest optimization | 1-2 min | ~50 calls | Quick testing |
| `light` | Balanced speed/quality | 3-5 min | ~400 calls | Development |
| `medium` | Quality focused | 8-12 min | ~800 calls | Production prep |
| `heavy` | Maximum quality | 15-30 min | ~1600 calls | Critical applications |

#### Example Configuration

```python
gepa_config = {
    "name": "GEPA",
    "params": {
        "metric": "advanced_math_feedback",
        "auto": "light",
        "reflection_lm": "qwen3:8b",
        "reflection_minibatch_size": 3,
        "skip_perfect_score": True,
        "add_format_failure_as_feedback": True
    }
}
```

### SIMBA (Stochastic Introspective Mini-Batch Ascent)

Advanced optimization with mini-batch processing and introspective analysis.

#### Configuration Parameters

```python
simba_params = {
    "metric": str,           # Evaluation metric
    "bsize": int,           # Batch size for optimization
    "num_candidates": int,   # Number of candidates to generate
    "max_steps": int,       # Maximum optimization steps
    "verbose": bool         # Enable detailed logging
}
```

#### Example Configuration

```python
simba_config = {
    "name": "SIMBA", 
    "params": {
        "metric": "answer_exact_match",
        "bsize": 8,
        "num_candidates": 5,
        "max_steps": 10
    }
}
```

### MIPROv2 (Multi-step Instruction Prompt Optimization)

Sophisticated prompt engineering with multi-step instruction refinement.

#### Configuration Parameters

```python
miprov2_params = {
    "metric": str,                 # Evaluation metric
    "num_candidates": int,         # Candidates per iteration  
    "init_temperature": float,     # Initial sampling temperature
    "verbose": bool               # Enable detailed logging
}
```

### BootstrapFewShot

Creates few-shot examples through bootstrapping with self-generated demonstrations.

#### Configuration Parameters

```python
bootstrap_params = {
    "metric": str,                    # Evaluation metric
    "max_bootstrapped_demos": int,    # Maximum bootstrapped examples
    "max_rounds": int,               # Bootstrap rounds
    "max_errors": int               # Error tolerance
}
```

### BetterTogether

Ensemble approach combining multiple few-shot strategies.

#### Configuration Parameters

```python
better_together_params = {
    "metric": str,                 # Evaluation metric
    "max_bootstrapped_demos": int, # Bootstrapped examples
    "max_labeled_demos": int,      # Labeled examples
    "max_rounds": int             # Optimization rounds
}
```

## Usage Patterns

### Basic Optimization Workflow

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

# 1. Create optimizer
optimizer = DSPyOptimizerFactory.create_optimizer(
    optimizer_name="GEPA",
    params={"metric": "answer_exact_match", "auto": "light"}
)

# 2. Compile with training data
optimized_pipeline = optimizer.compile(
    student=base_pipeline,
    trainset=training_examples
)

# 3. Use optimized pipeline
result = optimized_pipeline(input_data)
```

### Tier-Based Optimization

```python
# Automatic tier optimization
optimizer = DSPyOptimizerFactory.create_tier_optimized_optimizer(
    tier="oracles",           # Oracle-tier agent
    training_data_size=10,    # Small training set
    optimizer_config={        # Optional overrides
        "auto": "medium"
    }
)
```

### Custom Metric Integration

```python
def custom_domain_feedback(example, pred, trace=None):
    """Custom feedback metric for domain-specific evaluation."""
    from dspy.primitives import Prediction
    
    # Implement domain-specific scoring logic
    score = evaluate_prediction(example, pred)
    feedback = generate_improvement_feedback(example, pred)
    
    return Prediction(score=score, feedback=feedback)

# Register and use custom metric
optimizer = DSPyOptimizerFactory.create_optimizer(
    optimizer_name="GEPA",
    params={
        "metric": custom_domain_feedback,  # Pass function directly
        "auto": "light"
    }
)
```

## Error Handling

### Common Exceptions

#### `OptimizerNotSupportedError`

Raised when requesting an unsupported optimizer.

```python
try:
    optimizer = DSPyOptimizerFactory.create_optimizer("InvalidOptimizer")
except OptimizerNotSupportedError as e:
    print(f"Optimizer not supported: {e}")
```

#### `InvalidParameterError`

Raised when optimizer parameters are invalid.

```python
try:
    optimizer = DSPyOptimizerFactory.create_optimizer(
        "GEPA", 
        params={"invalid_param": "value"}
    )
except InvalidParameterError as e:
    print(f"Invalid parameter: {e}")
```

### Best Practices for Error Handling

```python
def safe_optimize(optimizer_config, pipeline, trainset):
    """Safely optimize with comprehensive error handling."""
    try:
        optimizer = DSPyOptimizerFactory.create_optimizer(**optimizer_config)
        return optimizer.compile(student=pipeline, trainset=trainset)
    except OptimizerNotSupportedError:
        # Fallback to default optimizer
        fallback = DSPyOptimizerFactory.create_optimizer("BootstrapFewShot")
        return fallback.compile(student=pipeline, trainset=trainset)
    except InvalidParameterError as e:
        # Log error and use default parameters
        logger.warning(f"Invalid parameters: {e}. Using defaults.")
        optimizer = DSPyOptimizerFactory.create_optimizer(
            optimizer_config["name"]
        )
        return optimizer.compile(student=pipeline, trainset=trainset)
```

## Performance Considerations

### Memory Usage Guidelines

| Optimizer | Memory Usage | Recommended RAM | Notes |
|-----------|--------------|-----------------|-------|
| GEPA | High (2 models) | 16GB+ | Uses reflection LM |
| SIMBA | Medium | 8GB+ | Single model optimization |
| MIPROv2 | Medium | 8GB+ | Instruction refinement |
| BootstrapFewShot | Low | 4GB+ | Lightweight bootstrapping |
| BetterTogether | Medium | 8GB+ | Ensemble approach |

### Optimization Time Estimates

| Optimizer | Light Config | Medium Config | Heavy Config |
|-----------|--------------|---------------|--------------|
| GEPA | 3-5 minutes | 8-12 minutes | 15-30 minutes |
| SIMBA | 1-2 minutes | 3-5 minutes | 5-10 minutes |
| MIPROv2 | 2-4 minutes | 5-8 minutes | 10-15 minutes |
| BootstrapFewShot | 30-60 seconds | 1-2 minutes | 2-5 minutes |

### Scaling Recommendations

```python
# For large training sets (>50 examples)
if len(trainset) > 50:
    optimizer_name = "BootstrapFewShot"  # More efficient for large data
else:
    optimizer_name = "GEPA"  # Better for small, high-quality data

# For resource-constrained environments
if available_memory_gb < 8:
    optimizer_config["auto"] = "minimal"
elif available_memory_gb < 16:
    optimizer_config["auto"] = "light"
else:
    optimizer_config["auto"] = "medium"
```

## Integration with SuperSpec

DSPy optimizers integrate seamlessly with SuperSpec agent playbooks:

```yaml
# agent_playbook.yaml
spec:
  optimization:
    optimizer:
      name: GEPA
      params:
        metric: advanced_math_feedback
        auto: light
        reflection_lm: qwen3:8b
        reflection_minibatch_size: 3
```

The factory automatically reads these configurations during agent compilation:

```python
# Automatic configuration from playbook
from superoptix.core.pipeline_utils import create_optimized_pipeline

# Reads optimization config from playbook
optimized_agent = create_optimized_pipeline(
    playbook_path="agent_playbook.yaml",
    trainset=training_data
)
```

## CLI Reference

### Agent Optimization Commands

#### `super agent optimize`

Optimizes an agent using the configured optimizer from its playbook.

**Syntax:**
```bash
super agent optimize <agent_name> [OPTIONS]
```

**Parameters:**
- `agent_name`: Name of the compiled agent to optimize

**Options:**
- `--timeout SECONDS`: Override default timeout (default: 300)
- `--output-dir PATH`: Directory to save optimized artifacts
- `--force`: Force re-optimization even if optimized version exists
- `--verbose`: Enable detailed optimization logs

**Examples:**
```bash
# Basic optimization with default settings
super agent optimize math_agent

# Optimization with extended timeout (10 minutes)
super agent optimize math_agent --timeout 600

# Verbose optimization with custom output directory
super agent optimize math_agent --verbose --output-dir ./optimized_agents

# Force re-optimization of previously optimized agent
super agent optimize math_agent --force
```

#### `super agent compile`

Compiles an agent from its playbook, preparing it for optimization.

**Syntax:**
```bash
super agent compile <agent_name> [OPTIONS]
```

**Options:**
- `--playbook PATH`: Path to playbook file (auto-detected if not specified)
- `--output-dir PATH`: Directory to save compiled pipeline
- `--validate`: Validate playbook before compilation

**Example:**
```bash
# Compile agent with validation
super agent compile math_agent --validate
```

#### `super agent evaluate`

Evaluates agent performance using configured metrics.

**Syntax:**
```bash
super agent evaluate <agent_name> [OPTIONS]
```

**Options:**
- `--dataset PATH`: Custom evaluation dataset
- `--metrics LIST`: Comma-separated list of metrics to use
- `--output FORMAT`: Output format (json, csv, table)

**Example:**
```bash
# Evaluate with custom metrics
super agent evaluate math_agent --metrics answer_exact_match,advanced_math_feedback
```

#### `super model install`

Installs required models for optimization.

**Syntax:**
```bash
super model install <model_name> [OPTIONS]
```

**Options:**
- `--provider PROVIDER`: Model provider (ollama, huggingface, etc.)
- `--backend BACKEND`: Compute backend (cpu, gpu, mps)

**Examples:**
```bash
# Install models for GEPA optimization
super model install llama3.1:8b --provider ollama
super model install qwen3:8b --provider ollama

# Install lightweight model for resource-constrained systems
super model install llama3.2:1b --provider ollama
```

### Configuration Commands

#### `super optimizer list`

Lists available optimizers and their parameters.

**Syntax:**
```bash
super optimizer list [OPTIMIZER_NAME]
```

**Example:**
```bash
# List all optimizers
super optimizer list

# Get details for specific optimizer
super optimizer list GEPA
```

**Sample Output:**
```
Available DSPy Optimizers:
==========================

GEPA - Graph Enhanced Prompting Algorithm
  Description: Reflective prompt evolution with advanced feedback
  Parameters:
    - metric (required): Evaluation metric function
    - auto: Budget control (minimal, light, medium, heavy)
    - reflection_lm (required): Reflection model name
    - reflection_minibatch_size: Examples per reflection batch
    - max_full_evals: Maximum full evaluations
    - skip_perfect_score: Skip if perfect score achieved

SIMBA - Stochastic Introspective Mini-Batch Ascent
  Description: Advanced optimization with mini-batch processing
  Parameters:
    - metric (required): Evaluation metric function
    - bsize: Batch size for optimization
    - num_candidates: Number of candidates to generate
    - max_steps: Maximum optimization steps
```

#### `super agent status`

Shows optimization status and performance metrics.

**Syntax:**
```bash
super agent status <agent_name>
```

**Example Output:**
```
Agent: math_agent
Status: Optimized
Optimizer: GEPA
Last Optimization: 2024-01-15 14:30:22
Performance Metrics:
  - Baseline Accuracy: 60.0%
  - Optimized Accuracy: 95.0%
  - Improvement: +35.0%
  - Optimization Time: 4m 32s
```

### Troubleshooting Commands

#### `super logs optimizer`

Shows optimization logs for debugging.

**Syntax:**
```bash
super logs optimizer <agent_name> [OPTIONS]
```

**Options:**
- `--lines N`: Number of log lines to show (default: 50)
- `--level LEVEL`: Log level filter (debug, info, warning, error)
- `--follow`: Follow log output in real-time

**Examples:**
```bash
# Show recent optimization logs
super logs optimizer math_agent --lines 100

# Follow optimization in real-time
super logs optimizer math_agent --follow

# Show only error logs
super logs optimizer math_agent --level error
```

## API Reference Extensions

### Environment Variables

Configure DSPy optimizers using environment variables:

```bash
# Default optimizer settings
export SUPEROPTIX_DEFAULT_OPTIMIZER="GEPA"
export SUPEROPTIX_OPTIMIZER_TIMEOUT="300"

# GEPA-specific settings
export GEPA_AUTO_BUDGET="light"
export GEPA_REFLECTION_LM="qwen3:8b"
export GEPA_MINIBATCH_SIZE="3"

# Model configuration
export OLLAMA_HOST="localhost:11434"
export SUPEROPTIX_MODEL_CACHE_DIR="~/.superoptix/models"
```

### Programmatic Configuration

#### Agent Factory with Optimizer

```python
from superoptix.core.agent_factory import AgentFactory
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

# Create agent with pre-configured optimizer
agent_config = {
    "name": "math_solver",
    "optimizer": {
        "name": "GEPA",
        "params": {
            "metric": "advanced_math_feedback",
            "auto": "light",
            "reflection_lm": "qwen3:8b"
        }
    }
}

agent = AgentFactory.create_from_config(agent_config)
optimized_agent = agent.optimize(training_data)
```

#### Optimizer Comparison

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory
from superoptix.evaluation.benchmarks import OptimizationBenchmark

# Compare multiple optimizers
optimizers = {
    "gepa": DSPyOptimizerFactory.create_optimizer("GEPA", {"auto": "light"}),
    "simba": DSPyOptimizerFactory.create_optimizer("SIMBA", {"bsize": 8}),
    "bootstrap": DSPyOptimizerFactory.create_optimizer("BootstrapFewShot")
}

benchmark = OptimizationBenchmark(
    pipeline=base_pipeline,
    trainset=training_data,
    testset=test_data,
    optimizers=optimizers
)

results = benchmark.run()
print(benchmark.comparison_report(results))
```

#### Custom Metric Registration

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

# Register custom metric globally
def custom_domain_metric(example, pred, trace=None):
    # Implementation here
    pass

DSPyOptimizerFactory.register_metric("custom_domain_feedback", custom_domain_metric)

# Use in optimizer creation
optimizer = DSPyOptimizerFactory.create_optimizer(
    "GEPA",
    params={"metric": "custom_domain_feedback"}
)
```

### Batch Operations

#### Bulk Agent Optimization

```python
from superoptix.core.batch_optimizer import BatchOptimizer

# Optimize multiple agents
agents = ["math_agent", "legal_agent", "security_agent"]
optimizer_configs = {
    "math_agent": {"name": "GEPA", "params": {"auto": "medium"}},
    "legal_agent": {"name": "GEPA", "params": {"auto": "heavy"}},
    "security_agent": {"name": "SIMBA", "params": {"bsize": 4}}
}

batch_optimizer = BatchOptimizer(
    agents=agents,
    optimizer_configs=optimizer_configs,
    parallel_workers=2
)

results = batch_optimizer.optimize_all()
```

#### Performance Monitoring

```python
from superoptix.monitoring.optimizer_monitor import OptimizerMonitor

# Monitor optimization performance
monitor = OptimizerMonitor()

with monitor.track_optimization("math_agent") as tracker:
    optimizer = DSPyOptimizerFactory.create_optimizer("GEPA")
    optimized_pipeline = optimizer.compile(base_pipeline, trainset)
    
    # Get real-time metrics
    metrics = tracker.get_current_metrics()
    print(f"Progress: {metrics['progress']:.1%}")
    print(f"Current Score: {metrics['score']:.3f}")
```

## See Also

- [GEPA API Reference](gepa.md)
- [GEPA Optimization Guide](../../guides/gepa-optimization.md)
- [SuperSpec Configuration Reference](superspec.md) 
- [Agent Development Workflow](../../guides/agent-development.md)
- [CLI Command Reference](../cli/commands.md)