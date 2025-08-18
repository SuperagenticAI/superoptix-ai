# GEPA API Reference

This document provides the API reference for GEPA (Graph Enhanced Prompting Algorithm) optimization in SuperOptiX.

## Overview

GEPA is a reflective prompt optimizer that uses Large Language Models' ability to analyze and critique their own behavior. It's available as a DSPy optimizer through SuperOptiX's unified optimizer factory.

## Core API

### Configuration

GEPA is configured through the `DSPyOptimizerFactory` with optimizer-specific parameters:

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

gepa_optimizer = DSPyOptimizerFactory.create_optimizer(
    optimizer_name="GEPA",
    params={
        "metric": "advanced_math_feedback",
        "auto": "light",
        "reflection_lm": "qwen3:8b",
        "reflection_minibatch_size": 3
    }
)
```

## Parameters Reference

### Core Parameters

#### `metric` (required)
**Type:** `str` or `callable`
**Description:** Evaluation metric for optimization

**Built-in Options:**
- `"answer_exact_match"` - Basic exact string matching
- `"advanced_math_feedback"` - Mathematical reasoning evaluation
- `"multi_component_enterprise_feedback"` - Business document analysis
- `"vulnerability_detection_feedback"` - Security vulnerability assessment
- `"privacy_preservation_feedback"` - Privacy compliance evaluation
- `"medical_accuracy_feedback"` - Healthcare safety validation
- `"legal_analysis_feedback"` - Legal compliance verification

**Custom Metric:**
```python
def custom_metric(example, pred, trace=None):
    from dspy.primitives import Prediction
    score = evaluate_custom_logic(example, pred)
    feedback = generate_feedback(example, pred)
    return Prediction(score=score, feedback=feedback)

params = {"metric": custom_metric}
```

#### `auto` (recommended)
**Type:** `str`
**Default:** `"light"`
**Options:** `"minimal"`, `"light"`, `"medium"`, `"heavy"`
**Description:** Automatic budget control for optimization intensity

| Setting | Time | Metric Calls | Use Case |
|---------|------|--------------|----------|
| `minimal` | 1-2 min | ~50 | Quick testing |
| `light` | 3-5 min | ~400 | Development |
| `medium` | 8-12 min | ~800 | Production prep |
| `heavy` | 15-30 min | ~1600 | Critical applications |

### Reflection Parameters

#### `reflection_lm` (required)
**Type:** `str`
**Description:** Language model for reflection and analysis

**Recommended Models:**
- `"qwen3:8b"` - Diverse reasoning perspective
- `"llama3.1:8b"` - Consistent with main processing
- `"llama3.2:1b"` - Lightweight option for resource constraints

**Example:**
```python
params = {
    "reflection_lm": "qwen3:8b",  # Different from main LM for diversity
}
```

#### `reflection_minibatch_size`
**Type:** `int`
**Default:** `3`
**Range:** `1-10`
**Description:** Number of examples processed per reflection batch

**Guidelines:**
- Larger batches: More context for reflection but higher memory usage
- Smaller batches: More frequent feedback but potentially less coherent insights

### Optimization Control

#### `max_full_evals`
**Type:** `int`
**Default:** Set by `auto` parameter
**Description:** Maximum number of full dataset evaluations

**Manual Override:**
```python
params = {
    "auto": None,  # Disable auto settings
    "max_full_evals": 20  # Custom limit
}
```

#### `skip_perfect_score`
**Type:** `bool`
**Default:** `True`
**Description:** Skip further optimization if perfect score achieved

#### `add_format_failure_as_feedback`
**Type:** `bool`
**Default:** `True`
**Description:** Include format parsing failures in feedback generation

### Advanced Parameters

#### `predictor_level_feedback`
**Type:** `bool`
**Default:** `False`
**Description:** Enable component-level feedback for multi-step pipelines

**Use Case:** Complex pipelines with multiple reasoning steps

```python
params = {
    "predictor_level_feedback": True  # For multi-component agents
}
```

#### `format_failure_feedback`
**Type:** `bool`
**Default:** `False` 
**Description:** Specialized feedback for format parsing issues

## Usage Patterns

### Basic GEPA Optimization

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

# Create GEPA optimizer
optimizer = DSPyOptimizerFactory.create_optimizer(
    optimizer_name="GEPA",
    params={
        "metric": "answer_exact_match",
        "auto": "light",
        "reflection_lm": "qwen3:8b"
    }
)

# Optimize pipeline
optimized_pipeline = optimizer.compile(
    student=base_pipeline,
    trainset=training_examples
)
```

### Domain-Specific Configuration

#### Mathematical Problem Solving
```python
math_params = {
    "metric": "advanced_math_feedback",
    "auto": "light",
    "reflection_lm": "qwen3:8b",
    "reflection_minibatch_size": 3,
    "skip_perfect_score": True
}
```

#### Security Analysis
```python
security_params = {
    "metric": "vulnerability_detection_feedback",
    "auto": "medium",  # More thorough for security
    "reflection_lm": "qwen3:8b",
    "reflection_minibatch_size": 5,
    "format_failure_feedback": True  # Handle code format issues
}
```

#### Healthcare Applications
```python
medical_params = {
    "metric": "medical_accuracy_feedback",
    "auto": "heavy",  # Maximum safety for medical
    "reflection_lm": "qwen3:8b",
    "reflection_minibatch_size": 2,  # Conservative batch size
    "skip_perfect_score": False  # Always complete full optimization
}
```

### Resource-Optimized Configurations

#### Low Memory (8GB+ RAM)
```python
lightweight_params = {
    "metric": "answer_exact_match",
    "auto": "minimal",
    "reflection_lm": "llama3.2:1b",  # Smaller model
    "reflection_minibatch_size": 2,
    "max_full_evals": 3
}
```

#### Standard Setup (16GB+ RAM)
```python
standard_params = {
    "metric": "advanced_math_feedback",
    "auto": "light",
    "reflection_lm": "qwen3:8b",
    "reflection_minibatch_size": 3
}
```

#### High-Performance (32GB+ RAM)
```python
performance_params = {
    "metric": "advanced_math_feedback",
    "auto": "heavy",
    "reflection_lm": "qwen3:8b",
    "reflection_minibatch_size": 5,
    "max_full_evals": 50
}
```

## Custom Feedback Metrics

### Implementing Custom Metrics

```python
def domain_specific_feedback(example, pred, trace=None):
    """
    Custom feedback metric for domain-specific evaluation.
    
    Args:
        example: Training example with input/expected output
        pred: Model prediction to evaluate
        trace: Optional execution trace (for debugging)
        
    Returns:
        dspy.Prediction with score and feedback
    """
    from dspy.primitives import Prediction
    
    # Domain-specific evaluation logic
    accuracy_score = evaluate_accuracy(example, pred)
    safety_score = evaluate_safety(example, pred)
    compliance_score = evaluate_compliance(example, pred)
    
    # Combine scores
    overall_score = (accuracy_score + safety_score + compliance_score) / 3
    
    # Generate improvement feedback
    feedback = []
    if accuracy_score < 0.8:
        feedback.append("Improve factual accuracy by cross-referencing authoritative sources")
    if safety_score < 0.9:
        feedback.append("Add safety disclaimers and risk assessments")
    if compliance_score < 0.95:
        feedback.append("Ensure full regulatory compliance with industry standards")
    
    feedback_text = ". ".join(feedback) if feedback else "Excellent performance across all criteria"
    
    return Prediction(score=overall_score, feedback=feedback_text)

# Use custom metric
optimizer = DSPyOptimizerFactory.create_optimizer(
    optimizer_name="GEPA",
    params={
        "metric": domain_specific_feedback,
        "auto": "light",
        "reflection_lm": "qwen3:8b"
    }
)
```

### Multi-Criteria Evaluation

```python
def multi_criteria_feedback(example, pred, trace=None):
    """Multi-aspect evaluation with weighted scoring."""
    from dspy.primitives import Prediction
    
    # Multiple evaluation criteria
    criteria = {
        "accuracy": (evaluate_accuracy(example, pred), 0.4),
        "clarity": (evaluate_clarity(pred), 0.3),
        "completeness": (evaluate_completeness(example, pred), 0.2),
        "efficiency": (evaluate_efficiency(pred), 0.1)
    }
    
    # Weighted score calculation
    total_score = sum(score * weight for score, weight in criteria.values())
    
    # Detailed feedback generation
    feedback_parts = []
    for criterion, (score, weight) in criteria.items():
        if score < 0.7:
            feedback_parts.append(f"Improve {criterion} (current: {score:.2f})")
    
    feedback = "; ".join(feedback_parts) if feedback_parts else "Strong performance across all criteria"
    
    return Prediction(score=total_score, feedback=feedback)
```

## Compatibility and Limitations

### Supported Agent Types

| Agent Tier | Tool Support | GEPA Compatible | Recommended Alternative |
|------------|--------------|-----------------|------------------------|
| **Oracles** | No tools | ✅ Yes | GEPA (excellent fit) |
| **Genies** | ReAct + Tools | ❌ No | BootstrapFewShot, SIMBA |
| **Protocols** | Advanced tools | ❌ No | BetterTogether, MIPROv2 |
| **Superagents** | Complex tools | ❌ No | SIMBA, MIPROv2 |

### GEPA Limitations

#### Tool-Calling Agents
GEPA currently doesn't support ReAct agents with tool calling due to:
- Complex output format parsing requirements
- Multi-step trajectory analysis challenges
- Tool response integration complexity

**Error Symptoms:**
```
WARNING: Failed to unpack prediction and trace
INFO: No trajectories captured. Skipping.
Average Metric: 0.0 / 5 (0.0%)
```

**Solution:** Use alternative optimizers for tool-enabled agents:
```python
# For Genies tier with tools
tool_agent_params = {
    "name": "BootstrapFewShot",
    "params": {
        "metric": "answer_exact_match",
        "max_bootstrapped_demos": 4,
        "max_rounds": 1
    }
}
```

### System Requirements

#### Minimum Requirements
- **RAM:** 8GB+ (with lightweight configuration)
- **Models:** Primary LM + Reflection LM
- **Time:** 1-2 minutes minimum for optimization

#### Recommended Setup
- **RAM:** 16GB+
- **Models:** `llama3.1:8b` + `qwen3:8b`
- **Storage:** 20GB+ for model storage

#### Production Setup
- **RAM:** 32GB+
- **CPU:** 8+ cores
- **Models:** Full model suite for optimal reflection

## Monitoring and Debugging

### Optimization Progress Indicators

**Normal GEPA Logs:**
```
INFO dspy.teleprompt.gepa.gepa: Running GEPA for approx 400 metric calls
INFO dspy.evaluate.evaluate: Average Metric: 2.0 / 5 (40.0%)
INFO dspy.teleprompt.gepa.gepa: Iteration 0: Base program full valset score: 0.4
INFO dspy.teleprompt.gepa.gepa: Iteration 1: Selected program 0 score: 0.4
INFO dspy.evaluate.evaluate: Average Metric: 3.0 / 3 (100.0%)
INFO dspy.teleprompt.gepa.gepa: Iteration 2: Proposed new text for predictor
```

**Success Indicators:**
- ✅ Allocated metric calls (e.g., "approx 400 metric calls")
- ✅ Baseline performance measurement
- ✅ Iterative improvements ("Selected program X score")
- ✅ Score improvements over iterations
- ✅ New prompt candidate generation

### Common Issues and Solutions

#### Timeout Behavior
**Issue:** GEPA optimization exceeds timeout limits
**Solution:** Normal behavior - GEPA prioritizes quality over speed
```python
# Allow longer timeout in agent optimization
# This is handled automatically by SuperOptiX CLI
```

#### Memory Issues
**Issue:** Out of memory errors during optimization
**Solution:** Reduce resource usage
```python
memory_efficient_params = {
    "auto": "minimal",
    "reflection_minibatch_size": 2,
    "reflection_lm": "llama3.2:1b"
}
```

#### Low Scores
**Issue:** Optimization produces 0% scores
**Solution:** Check metric configuration and data quality
```python
# Verify metric function
def debug_metric(example, pred, trace=None):
    print(f"Example: {example}")
    print(f"Prediction: {pred}")
    # Add debug logic
    return original_metric(example, pred, trace)
```

## Performance Optimization

### Model Selection Strategy

```python
def select_reflection_model(main_model, available_memory_gb):
    """Select optimal reflection model based on main model and resources."""
    
    if available_memory_gb < 12:
        return "llama3.2:1b"  # Lightweight option
    elif main_model.startswith("llama"):
        return "qwen3:8b"     # Diverse perspective
    else:
        return "llama3.1:8b"  # Consistent architecture
```

### Budget Optimization

```python
def optimize_gepa_budget(training_size, time_constraint_minutes):
    """Select optimal GEPA budget based on constraints."""
    
    if time_constraint_minutes < 3:
        return "minimal"
    elif time_constraint_minutes < 8:
        return "light"
    elif training_size < 10 and time_constraint_minutes < 15:
        return "medium"
    else:
        return "heavy"
```

## Integration Examples

### SuperSpec Integration

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
        skip_perfect_score: true
        add_format_failure_as_feedback: true
```

### Programmatic Usage

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory
from superoptix.core.pipeline_utils import EnhancedPipelineMixin

class CustomAgent(EnhancedPipelineMixin):
    def __init__(self):
        super().__init__()
        self.gepa_optimizer = DSPyOptimizerFactory.create_optimizer(
            optimizer_name="GEPA",
            params={
                "metric": "advanced_math_feedback",
                "auto": "light",
                "reflection_lm": "qwen3:8b"
            }
        )
    
    def optimize(self, training_data):
        """Optimize the agent using GEPA."""
        return self.gepa_optimizer.compile(
            student=self.base_pipeline,
            trainset=training_data
        )
```

## CLI Reference

### GEPA-Specific Commands

#### `super agent optimize --optimizer gepa`

Explicitly use GEPA optimizer, overriding playbook configuration.

**Syntax:**
```bash
super agent optimize <agent_name> --optimizer gepa [GEPA_OPTIONS]
```

**GEPA Options:**
- `--auto BUDGET`: Set budget level (minimal, light, medium, heavy)
- `--reflection-lm MODEL`: Specify reflection model
- `--minibatch-size N`: Set reflection minibatch size
- `--max-evals N`: Maximum full evaluations
- `--metric METRIC`: Override evaluation metric

**Examples:**
```bash
# Use GEPA with light budget
super agent optimize math_agent --optimizer gepa --auto light

# GEPA with custom reflection model
super agent optimize math_agent --optimizer gepa --reflection-lm llama3.1:8b

# GEPA with specific metric and parameters
super agent optimize math_agent --optimizer gepa \
  --metric advanced_math_feedback \
  --auto medium \
  --minibatch-size 5
```

#### `super gepa status`

Shows GEPA-specific optimization status and progress.

**Syntax:**
```bash
super gepa status <agent_name>
```

**Example Output:**
```
GEPA Optimization Status
========================
Agent: advanced_math_gepa
Optimizer: GEPA
Configuration:
  - Budget: light (~400 metric calls)
  - Reflection LM: qwen3:8b
  - Minibatch Size: 3
  - Metric: advanced_math_feedback

Progress:
  - Current Iteration: 3/5
  - Metric Calls Used: 287/400
  - Best Score: 0.85 (iteration 2)
  - Current Score: 0.91

Reflection Insights:
  - Generated 12 prompt candidates
  - 8 improvements identified
  - 3 candidates selected for next iteration

Time Elapsed: 3m 42s
Estimated Remaining: 1m 18s
```

#### `super gepa configure`

Interactive configuration wizard for GEPA parameters.

**Syntax:**
```bash
super gepa configure <agent_name> [OPTIONS]
```

**Options:**
- `--hardware-tier TIER`: Auto-configure for hardware (lightweight, standard, production)
- `--domain DOMAIN`: Domain-specific configuration (math, medical, legal, security)
- `--save-template`: Save configuration as template

**Example:**
```bash
# Configure GEPA for mathematics domain on standard hardware
super gepa configure math_agent --hardware-tier standard --domain math

# Interactive configuration with template saving
super gepa configure custom_agent --save-template
```

**Sample Interactive Session:**
```
GEPA Configuration Wizard
=========================

1. Hardware Configuration:
   [1] Lightweight (8GB+ RAM, faster optimization)
   [2] Standard (16GB+ RAM, balanced)
   [3] Production (32GB+ RAM, best quality)
   
   Choice [2]: 2

2. Domain Selection:
   [1] Mathematics (step-by-step reasoning)
   [2] Medical (safety-focused)
   [3] Legal (compliance-focused)
   [4] Security (vulnerability detection)
   [5] Custom domain
   
   Choice [1]: 1

3. Optimization Budget:
   [1] Minimal (1-2 min, quick testing)
   [2] Light (3-5 min, development)
   [3] Medium (8-12 min, production prep)
   [4] Heavy (15-30 min, best quality)
   
   Choice [2]: 2

Configuration Summary:
=====================
Reflection LM: qwen3:8b
Budget: light (~400 metric calls)
Metric: advanced_math_feedback
Minibatch Size: 3
Max Evaluations: 10

Apply this configuration? [y/N]: y
```

### Advanced CLI Commands

#### `super gepa benchmark`

Run GEPA benchmark against other optimizers.

**Syntax:**
```bash
super gepa benchmark <agent_name> [OPTIONS]
```

**Options:**
- `--compare-with LIST`: Comma-separated optimizer names
- `--iterations N`: Number of benchmark iterations
- `--output-format FORMAT`: Output format (table, json, csv)

**Example:**
```bash
# Benchmark GEPA against SIMBA and BootstrapFewShot
super gepa benchmark math_agent \
  --compare-with SIMBA,BootstrapFewShot \
  --iterations 3 \
  --output-format table
```

**Sample Output:**
```
GEPA Benchmark Results
=====================

Agent: math_agent
Iterations: 3
Dataset: 50 examples

Optimizer Performance:
┌─────────────────┬──────────┬─────────┬──────────────┬──────────────┐
│ Optimizer       │ Avg Score│ Best    │ Avg Time     │ Consistency  │
├─────────────────┼──────────┼─────────┼──────────────┼──────────────┤
│ GEPA           │ 0.924    │ 0.956   │ 4m 12s       │ 0.87         │
│ SIMBA          │ 0.843    │ 0.891   │ 1m 34s       │ 0.92         │
│ BootstrapFewShot│ 0.756    │ 0.798   │ 0m 45s       │ 0.95         │
└─────────────────┴──────────┴─────────┴──────────────┴──────────────┘

GEPA Advantages:
✓ Highest average and peak performance
✓ Best handling of complex reasoning tasks
✓ Superior prompt evolution quality

Trade-offs:
- Longer optimization time
- Higher memory requirements
```

#### `super gepa debug`

Debug GEPA optimization issues.

**Syntax:**
```bash
super gepa debug <agent_name> [OPTIONS]
```

**Options:**
- `--show-reflections`: Display reflection analysis
- `--trace-evolution`: Show prompt evolution tree
- `--analyze-failures`: Analyze failed optimization attempts

**Example:**
```bash
# Debug with full reflection analysis
super gepa debug math_agent --show-reflections --trace-evolution
```

## API Reference Extensions

### GEPA-Specific Configuration

#### GepaConfig Class

```python
from superoptix.optimizers.gepa import GepaConfig

# Type-safe GEPA configuration
config = GepaConfig(
    metric="advanced_math_feedback",
    auto="light",
    reflection_lm="qwen3:8b",
    reflection_minibatch_size=3,
    skip_perfect_score=True,
    add_format_failure_as_feedback=True
)

# Validate configuration
config.validate()

# Hardware-specific presets
lightweight_config = GepaConfig.lightweight_preset()
production_config = GepaConfig.production_preset()
```

#### GEPA Factory with Presets

```python
from superoptix.core.optimizer_factory import DSPyOptimizerFactory

# Domain-specific GEPA configurations
math_optimizer = DSPyOptimizerFactory.create_gepa_optimizer(
    domain="mathematics",
    hardware_tier="standard"
)

medical_optimizer = DSPyOptimizerFactory.create_gepa_optimizer(
    domain="healthcare",
    hardware_tier="production",  # Higher safety requirements
    custom_params={
        "skip_perfect_score": False,  # Always complete full optimization
        "reflection_minibatch_size": 2  # Conservative batch size
    }
)
```

### Advanced GEPA Usage

#### Custom Reflection Prompts

```python
from superoptix.optimizers.gepa import GepaOptimizer

class CustomGepaOptimizer(GepaOptimizer):
    def get_reflection_prompt(self, examples, predictions):
        """Override reflection prompt for domain-specific analysis."""
        base_prompt = super().get_reflection_prompt(examples, predictions)
        
        domain_prompt = f"""
        {base_prompt}
        
        Additional domain considerations:
        - Focus on mathematical accuracy and step-by-step reasoning
        - Ensure all algebraic manipulations are clearly explained
        - Verify solutions through substitution when applicable
        - Consider multiple solution methods when relevant
        """
        
        return domain_prompt

# Use custom optimizer
optimizer = CustomGepaOptimizer(
    metric="advanced_math_feedback",
    auto="light",
    reflection_lm="qwen3:8b"
)
```

#### Real-time Optimization Monitoring

```python
from superoptix.optimizers.gepa import GepaOptimizer, GepaCallback

class ProgressCallback(GepaCallback):
    def on_iteration_start(self, iteration, context):
        print(f"Starting iteration {iteration}")
        
    def on_reflection_complete(self, reflection_result, context):
        print(f"Reflection insights: {len(reflection_result.suggestions)} suggestions")
        
    def on_candidates_generated(self, candidates, context):
        print(f"Generated {len(candidates)} new prompt candidates")
        
    def on_evaluation_complete(self, scores, context):
        best_score = max(scores)
        print(f"Best score this iteration: {best_score:.3f}")

# Use callback for monitoring
optimizer = GepaOptimizer(
    metric="advanced_math_feedback",
    auto="light",
    reflection_lm="qwen3:8b",
    callbacks=[ProgressCallback()]
)

optimized_pipeline = optimizer.compile(base_pipeline, trainset)
```

#### Parallel GEPA Optimization

```python
from superoptix.optimizers.gepa import GepaEnsemble
from concurrent.futures import ThreadPoolExecutor

# Run multiple GEPA configurations in parallel
configs = [
    {"reflection_lm": "qwen3:8b", "minibatch_size": 3},
    {"reflection_lm": "llama3.1:8b", "minibatch_size": 5},
    {"reflection_lm": "qwen3:8b", "minibatch_size": 2, "auto": "medium"}
]

ensemble = GepaEnsemble(
    base_config={"metric": "advanced_math_feedback"},
    variant_configs=configs,
    selection_strategy="best_validation_score"
)

# Parallel optimization with resource management
optimized_pipeline = ensemble.optimize_parallel(
    base_pipeline=base_pipeline,
    trainset=trainset,
    max_workers=2  # Limit concurrent optimizations
)
```

### GEPA Introspection API

#### Optimization Analysis

```python
from superoptix.optimizers.gepa import GepaAnalyzer

# Analyze completed GEPA optimization
analyzer = GepaAnalyzer.from_optimized_agent("math_agent")

# Get optimization history
history = analyzer.get_optimization_history()
for iteration in history:
    print(f"Iteration {iteration.number}:")
    print(f"  Score: {iteration.score:.3f}")
    print(f"  Candidates: {len(iteration.candidates)}")
    print(f"  Insights: {iteration.reflection_summary}")

# Analyze prompt evolution
evolution_tree = analyzer.get_prompt_evolution_tree()
analyzer.visualize_evolution(evolution_tree, save_path="prompt_evolution.png")

# Get reflection insights
insights = analyzer.get_reflection_insights()
print("Key improvement areas identified:")
for insight in insights:
    print(f"- {insight.category}: {insight.description}")
```

#### Performance Profiling

```python
from superoptix.optimizers.gepa import GepaProfiler

# Profile GEPA performance
profiler = GepaProfiler()

with profiler.profile_optimization():
    optimizer = DSPyOptimizerFactory.create_optimizer("GEPA")
    optimized_pipeline = optimizer.compile(base_pipeline, trainset)

# Get detailed performance report
report = profiler.get_performance_report()
print("GEPA Performance Profile:")
print(f"Total Time: {report.total_time:.1f}s")
print(f"Reflection Time: {report.reflection_time:.1f}s ({report.reflection_percentage:.1%})")
print(f"Evaluation Time: {report.evaluation_time:.1f}s ({report.evaluation_percentage:.1%})")
print(f"Memory Peak: {report.memory_peak:.1f}GB")

# Bottleneck analysis
bottlenecks = profiler.identify_bottlenecks()
for bottleneck in bottlenecks:
    print(f"Bottleneck: {bottleneck.component} - {bottleneck.impact}")
```

### Integration with SuperSpec

#### Dynamic GEPA Configuration

```python
from superoptix.superspec.gepa_integration import GepaSpecBuilder

# Build GEPA configuration from agent requirements
spec_builder = GepaSpecBuilder()

# Analyze agent requirements
agent_analysis = spec_builder.analyze_agent("math_agent")
print(f"Recommended GEPA config for {agent_analysis.complexity} complexity:")

# Generate optimal configuration
gepa_spec = spec_builder.build_gepa_spec(
    agent_requirements=agent_analysis,
    resource_constraints={"max_memory_gb": 16, "max_time_minutes": 10},
    quality_priorities=["accuracy", "reasoning_quality"]
)

print(f"Auto-generated GEPA configuration:")
print(f"  Budget: {gepa_spec.auto}")
print(f"  Reflection Model: {gepa_spec.reflection_lm}")
print(f"  Estimated Time: {gepa_spec.estimated_time_minutes} minutes")
```

## See Also

- [DSPy Optimizers API Reference](dspy-optimizers.md)
- [GEPA Optimization Guide](../../guides/gepa-optimization.md)
- [Agent Development Workflow](../../guides/agent-development.md)
- [Custom Feedback Metrics Guide](../../guides/custom-metrics.md)
- [CLI Command Reference](../cli/commands.md)
- [SuperSpec GEPA Integration](../../guides/superspec-gepa.md)