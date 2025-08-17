# DSPy Optimizers in SuperOptiX

SuperOptiX provides comprehensive support for all major [DSPy](https://dspy.ai/) optimizers through an integrated factory system. This guide covers how to use DSPy's powerful [optimization capabilities](https://dspy.ai/learn/optimization/overview/) within the SuperOptiX framework.

## Overview

DSPy optimizers automatically improve your agent's prompts and reasoning patterns through systematic optimization. SuperOptiX enhances this with:

- **Unified Factory System**: Single interface for all DSPy optimizers
- **Memory-Optimized Configurations**: Safe defaults for various system specs
- **Advanced Feedback Metrics**: Domain-specific evaluation functions
- **Smart Answer Extraction**: Handles various output formats automatically
- **Integration with SuperSpec**: Seamless YAML-based configuration

## Available Optimizers

### 🚀 **GEPA** - Graph Enhanced Prompting Algorithm
*Reflective prompt evolution with advanced feedback*

```yaml
optimization:
  optimizer:
    name: GEPA
    params:
      metric: answer_exact_match
      auto: light                    # light, medium, heavy
      reflection_lm: qwen3:8b
      reflection_minibatch_size: 3
      skip_perfect_score: true
      add_format_failure_as_feedback: true
```

**Key Features:**
- **Reflective Learning**: Self-improving prompts through feedback
- **Auto Modes**: `light` (fast), `medium` (balanced), `heavy` (thorough)
- **Advanced Metrics**: 7 domain-specific feedback functions
- **Memory Usage**: ~25GB peak

**Best For:** Complex reasoning tasks, mathematical problems, domain-specific optimization

---

### ⚡ **SIMBA** - Stochastic Introspective Mini-Batch Ascent
*Advanced optimization with mini-batch processing*

```yaml
optimization:
  optimizer:
    name: SIMBA
    params:
      metric: answer_exact_match
      bsize: 8                       # Mini-batch size
      num_candidates: 4              # Candidate prompts per step
      max_steps: 4                   # Optimization steps
      max_demos: 3                   # Few-shot examples
      temperature_for_sampling: 0.2
      temperature_for_candidates: 0.2
```

**Key Features:**
- **Mini-Batch Processing**: Efficient batch optimization
- **Candidate Generation**: Multiple prompt variations per step
- **Temperature Control**: Fine-tuned sampling parameters
- **Memory Usage**: ~28GB peak

**Best For:** Large datasets, performance-critical applications, systematic improvement

---

### 🔧 **MIPROv2** - Multi-step Instruction Prompt Optimization
*Sophisticated prompt engineering with multiple steps*

```yaml
optimization:
  optimizer:
    name: MIPROv2
    params:
      metric: answer_exact_match
      num_candidates: 8              # Reduced from default 20
      init_temperature: 1.0
```

**Key Features:**
- **Multi-Step Optimization**: Iterative prompt refinement
- **Instruction Engineering**: Focus on instruction clarity
- **Candidate Exploration**: Multiple prompt variations
- **Memory Usage**: ~20GB peak

**Best For:** Instruction-following tasks, complex workflows, detailed reasoning

---

### 📚 **BootstrapFewShot** - Traditional Few-Shot Learning
*Reliable bootstrapping with few-shot examples*

```yaml
optimization:
  optimizer:
    name: BootstrapFewShot
    params:
      metric: answer_exact_match
      max_bootstrapped_demos: 4      # Generated examples
      max_labeled_demos: 16          # Manual examples
      max_rounds: 1                  # Optimization rounds
```

**Key Features:**
- **Bootstrap Learning**: Generate examples from existing data
- **Labeled Examples**: Incorporate manual examples
- **Round Control**: Multi-round optimization
- **Memory Usage**: ~18GB peak

**Best For:** Getting started, reliable baselines, limited training data

---

### 🤝 **BetterTogether** - Ensemble Few-Shot Learning
*Collaborative optimization with ensemble methods*

```yaml
optimization:
  optimizer:
    name: BetterTogether
    params:
      metric: answer_exact_match
      max_bootstrapped_demos: 3      # Generated examples
      max_labeled_demos: 12          # Manual examples
```

**Key Features:**
- **Ensemble Learning**: Combine multiple approaches
- **Collaborative Optimization**: Synergistic improvements
- **Example Integration**: Bootstrap + labeled examples
- **Memory Usage**: ~20GB peak

**Best For:** Robust performance, ensemble methods, collaborative learning

---

### 🔍 **COPRO** - Collaborative Prompt Optimization
*Advanced collaborative optimization* ⚠️

```yaml
optimization:
  optimizer:
    name: COPRO
    params:
      metric: answer_exact_match
      breadth: 6                     # Search breadth
      depth: 2                       # Search depth
      init_temperature: 1.2
```

**Status:** ⚠️ Requires `LITELLM_DROP_PARAMS=true` environment variable

**Best For:** Collaborative optimization, search-based improvement

---

### 🎯 **KNNFewShot** - K-Nearest Neighbor Learning
*Pattern-based optimization* ⚠️

```yaml
optimization:
  optimizer:
    name: KNNFewShot
    params:
      k: 3                          # Nearest neighbors
```

**Status:** ⚠️ Requires vectorizer configuration (coming soon)

**Best For:** Pattern recognition, similarity-based learning

## Memory Optimization

SuperOptiX includes memory-optimized configurations for different system specifications:

### For 128GB Systems (M4 Max, High-End Workstations)
- **SIMBA**: `bsize: 8`, `candidates: 4`, `steps: 4`
- **MIPROv2**: `candidates: 8` (reduced from 20)
- **Peak Usage**: ~28GB (22% of available memory)

### For 64GB Systems
- **SIMBA**: `bsize: 4`, `candidates: 2`, `steps: 3`
- **MIPROv2**: `candidates: 4`
- **Peak Usage**: ~15GB (23% of available memory)

### For 32GB Systems
- **BootstrapFewShot**: Recommended default
- **BetterTogether**: `max_bootstrapped_demos: 2`
- **Peak Usage**: ~8GB (25% of available memory)

## Advanced Features

### Smart Answer Extraction

SuperOptiX automatically handles various answer formats:

```python
# LaTeX boxed format
"$\\boxed{345}$" → "345"

# Natural language
"The answer is 42." → "42"

# Algebraic format
"x = 3 or x = -1/2" → "3, -1/2"

# Numeric extraction
"The result is 25 square units" → "25"
```

### Domain-Specific Feedback Metrics

Advanced GEPA feedback functions for specialized domains:

- **`advanced_math_feedback`**: Mathematical accuracy with step validation
- **`medical_accuracy_feedback`**: Safety-focused medical information
- **`legal_analysis_feedback`**: Legal compliance and risk assessment
- **`vulnerability_detection_feedback`**: Security analysis
- **`privacy_preservation_feedback`**: Data privacy compliance
- **`data_science_methodology_feedback`**: Scientific rigor
- **`multi_component_enterprise_feedback`**: Enterprise information extraction

### Tier-Optimized Defaults

SuperOptiX automatically selects optimizers based on agent tier:

```python
# Oracles Tier (≤5 examples)
optimizer = "LabeledFewShot"

# Oracles Tier (>5 examples)  
optimizer = "BootstrapFewShot"

# Genies Tier
optimizer = "BetterTogether"

# Advanced Tiers (≥20 examples)
optimizer = "GEPA"
```

## Usage Patterns

### Basic Optimization

```yaml
# In your agent playbook
optimization:
  optimizer:
    name: BootstrapFewShot
    params:
      metric: answer_exact_match
```

```bash
# Command line
super agent optimize my_agent
```

### Advanced Configuration

```yaml
optimization:
  optimizer:
    name: GEPA
    params:
      metric: advanced_math_feedback
      auto: medium
      reflection_lm: qwen3:8b
      reflection_minibatch_size: 3
      skip_perfect_score: true
      add_format_failure_as_feedback: true
```

### Custom Metrics

```python
# In optimizer factory
def custom_domain_feedback(example, pred, trace=None, *args, **kwargs):
    """Custom domain-specific feedback function."""
    expected = getattr(example, "answer", "")
    actual = getattr(pred, "answer", "")
    
    # Your custom evaluation logic
    score = evaluate_domain_specific_accuracy(expected, actual)
    feedback = generate_improvement_suggestions(expected, actual)
    
    return Prediction(score=score, feedback=feedback)
```

## Best Practices

### 1. **Start Simple, Scale Up**
```yaml
# Begin with BootstrapFewShot
optimizer:
  name: BootstrapFewShot
  
# Then move to GEPA for advanced needs
optimizer:
  name: GEPA
  params:
    auto: light  # Start with light mode
```

### 2. **Monitor Memory Usage**
```bash
# Check system memory before optimization
htop

# Use memory-safe configurations
# SuperOptiX provides optimized defaults
```

### 3. **Leverage BDD Scenarios**
```yaml
feature_specifications:
  scenarios:
    - name: quadratic_equation
      input:
        problem: "Solve 2x² - 5x - 3 = 0"
      expected_output:
        answer: "x = 3 or x = -1/2"
```

### 4. **Domain-Specific Optimization**
```yaml
# For mathematical problems
optimization:
  optimizer:
    name: GEPA
    params:
      metric: advanced_math_feedback
      
# For enterprise applications
optimization:
  optimizer:
    name: GEPA
    params:
      metric: multi_component_enterprise_feedback
```

### 5. **Iterative Improvement**
```bash
# Test baseline performance
super agent evaluate my_agent

# Optimize with light settings
super agent optimize my_agent

# Evaluate improvement
super agent evaluate my_agent

# Scale up if needed
# Edit playbook: auto: light → medium → heavy
```

## Troubleshooting

### Common Issues

#### Memory Errors
```bash
# Reduce batch sizes in playbook
bsize: 4          # Instead of 8
num_candidates: 2 # Instead of 4
```

#### COPRO Parameter Issues
```bash
# Set environment variable
export LITELLM_DROP_PARAMS=true
super agent optimize my_agent
```

#### Zero Scores
- Check answer format compatibility
- Use smart answer extraction (enabled by default)
- Verify BDD scenario expected outputs

#### Timeout Issues
- GEPA optimization takes 3-5 minutes (normal)
- Use `auto: light` for faster optimization
- Monitor system resources

### Performance Tips

1. **Use Appropriate Optimizer**: Match optimizer complexity to task complexity
2. **Optimize Memory**: Use provided memory-safe configurations
3. **Start Local**: Test with local models before cloud deployment
4. **Monitor Resources**: Watch memory and CPU usage during optimization
5. **Incremental Improvement**: Use `auto: light` → `medium` → `heavy` progression

## Integration Examples

### With Different Model Backends

```yaml
# Ollama (Local)
language_model:
  provider: ollama
  model: llama3.1:8b
  
optimization:
  optimizer:
    name: GEPA
    params:
      reflection_lm: qwen3:8b
```

```yaml
# OpenAI (Cloud)
language_model:
  provider: openai
  model: gpt-4-turbo
  
optimization:
  optimizer:
    name: MIPROv2
    params:
      num_candidates: 12  # Can use more with cloud
```

### With RAG Systems

```yaml
# Vector store integration
tools:
  - vectorstore_search

optimization:
  optimizer:
    name: BetterTogether  # Good for RAG workflows
    params:
      max_bootstrapped_demos: 4
```

### With Multi-Agent Systems

```yaml
# Orchestra coordination
optimization:
  optimizer:
    name: SIMBA          # Efficient for coordination
    params:
      bsize: 6
      max_steps: 3
```

## Performance Benchmarks

Based on testing with llama3.1:8b on M4 Max (128GB):

| Optimizer | Training Time | Memory Peak | Accuracy Gain | Best Use Case |
|-----------|---------------|-------------|---------------|---------------|
| BootstrapFewShot | 2-3 min | 18GB | +15-25% | Getting started |
| BetterTogether | 3-4 min | 20GB | +20-30% | Robust baselines |
| MIPROv2 | 4-6 min | 20GB | +25-35% | Instruction tasks |
| SIMBA | 5-7 min | 28GB | +30-40% | Performance critical |
| GEPA | 3-5 min | 25GB | +35-50% | Complex reasoning |

## Related Documentation

- [DSPy Official Documentation](https://dspy.ai/)
- [DSPy Optimization Overview](https://dspy.ai/learn/optimization/overview/)
- [GEPA Optimization Guide](gepa-optimization.md)
- [Agent Development Guide](agent-development.md)
- [Evaluation & Testing](evaluation-testing.md)
- [Memory Management](memory.md)
- [Model Management](model-management.md)

## Examples

Explore working examples in `/superoptix/agents/dspy_optimizers/`:

- `gepa_playbook.yaml` - GEPA configuration
- `simba_math_playbook.yaml` - SIMBA for mathematics
- `miprov2_math_playbook.yaml` - MIPROv2 advanced prompting
- `bootstrap_math_playbook.yaml` - Traditional few-shot
- `bettertogether_math_playbook.yaml` - Ensemble learning

## Contributing

To add support for new DSPy optimizers:

1. **Update Factory Registry**:
```python
# In optimizer_factory.py
OPTIMIZER_REGISTRY = {
    "new_optimizer": NewOptimizer,
    # ...
}
```

2. **Add Default Parameters**:
```python
DEFAULT_PARAMS = {
    "new_optimizer": {
        "metric": "answer_exact_match",
        # optimizer-specific params
    }
}
```

3. **Create Configuration Method**:
```python
def _configure_new_optimizer(cls, optimizer_class, params):
    # Custom configuration logic
    return optimizer_class(**params)
```

4. **Add Documentation**: Update this guide with the new optimizer details.

5. **Create Test Agent**: Add example playbook in `/agents/dspy_optimizers/`.

---

SuperOptiX's DSPy integration provides a powerful, memory-efficient platform for prompt optimization that scales from simple few-shot learning to advanced graph-based optimization algorithms.