# Optimization Guide

SuperOptiX provides DSPy-powered optimization capabilities that automatically improve agent performance by optimizing prompts and few-shot examples. This guide covers how to use optimization to enhance your agents.

## What is Optimization?

Optimization in SuperOptiX uses DSPy's **BootstrapFewShot** optimizer to automatically find the best prompts and few-shot examples for your agents. This process analyzes your BDD scenarios and generates optimized weights that improve agent performance.

### How DSPy Optimization Works

DSPy optimization works by:

1. **Learning from Examples**: The optimizer uses your BDD scenarios as training examples
2. **Trial and Error**: It tests different prompt variations to find the most effective ones
3. **Automatic Tuning**: Based on the results, it automatically adjusts prompts and reasoning chains
4. **Weight Saving**: Optimized configurations are saved as JSON files for future use

## How Optimization Works in SuperOptiX

### The Optimization Process

1. **Load Pipeline**: The agent's DSPy pipeline is loaded from the compiled Python file
2. **Convert Scenarios**: Each BDD scenario from your playbook is converted to a training example
3. **Run DSPy Optimizer**: The BootstrapFewShot optimizer is executed with your training data
4. **Save Weights**: Optimized weights are saved to `pipelines/<agent>_optimized.json`

### Optimization by Tier

#### Oracle Tier (Simple Agents)
- Uses **BootstrapFewShot** optimizer
- Optimizes prompts and few-shot examples
- Faster optimization process
- Uses up to 3 training examples

#### Genie Tier (Multi-step Agents)
- Uses **BootstrapFewShot** optimizer with enhanced reasoning
- Optimizes reasoning chains and tool usage
- Slower optimization due to ReAct complexity
- Uses up to 8 training examples
- Uses larger default model (`llama3.1:8b` vs `1b`)

## Running Optimization

### Basic Optimization Workflow

```bash
# 1. Compile your agent first
super agent compile your_agent

# 2. Evaluate baseline performance
super agent evaluate your_agent

# 3. Optimize the agent
super agent optimize your_agent

# 4. Re-evaluate to measure improvement
super agent evaluate your_agent
```

### Optimization Command

```bash
super agent optimize <agent_name>
```

**Purpose**: Pre-compute the best prompt / few-shot demos using the BDD scenarios in your playbook.

**Process**:
1. Load pipeline
2. Convert each BDD scenario to a training example
3. Run DSPy BootstrapFewShot optimizer
4. Save tuned weights to `pipelines/<agent>_optimized.json`

**Cost/Time**: Highest. Multiple LM calls per scenario. Genie-tier is slower because it uses ReAct & a larger model.

**When to run**: After you add/edit scenarios or change the playbook persona.

### Force Re-optimization

```bash
super agent optimize <agent_name> --force
```

Use the `--force` flag to re-optimize even if an optimized version already exists.

### Runtime Optimization

```bash
super agent run <agent_name> --goal "..." [--optimize / --force-optimize]
```

**Flags**:
- *none*: Use `*_optimized.json` if present; otherwise run the base prompts
- `--optimize`: If no saved optimization is found, performs on-the-fly optimization (slower & pricier). If a saved file exists, defaults to it and skips fresh optimization
- `--force-optimize`: Always re-optimize at run-time, overwriting existing weights

## Basic Configuration

### Optimization in Playbook

```yaml
spec:
  optimization:
    enabled: true
    strategy: bootstrap_fewshot
    max_examples: 8
    max_rounds: 1
```

### Supported Strategies

The current version of SuperOptiX supports these optimization strategies:

- **bootstrap_fewshot** (default) - Uses DSPy's BootstrapFewShot optimizer

- **knn_fewshot** - K-nearest neighbors few-shot optimization

- **labeled_fewshot** - Labeled few-shot optimization

## Best Practices

### 1. Proper BDD/TDD Workflow

```bash
# 1. Define scenarios and compile
super agent compile developer

# 2. Establish baseline (CRITICAL)
super agent evaluate developer

# 3. Optimize based on baseline results
super agent optimize developer

# 4. Validate improvement
super agent evaluate developer

# 5. Deploy only if quality gates pass
super agent run developer --goal "task"
```

### 2. Optimization Guidelines

- **Always evaluate first**: Run `super agent evaluate <n>` to establish baseline performance

- **Optimize based on evaluation**: Run `super agent optimize <n>` after changing the playbook or scenarios

- **Re-evaluate to measure improvement**: Run `super agent evaluate <n>` again to validate optimization effectiveness

- **Commit optimized weights**: Commit the generated `*_optimized.json` so CI & colleagues don't need to re-optimize

- **Use evaluation in CI/CD**: Use `super agent evaluate <n>` during PRs to ensure quality gates pass

- **Reserve runtime optimization**: Use `--optimize` flag during `run` only for quick experiments

### 3. Cost Management

- Monitor your provider dashboard during optimization
- Cancel with **CTRL-C** if it's taking too long; your base pipeline remains intact
- You can abort CI/CD build if you are performing optimization on CI/CD or GPU servers
- Use appropriate model sizes for optimization (smaller models for oracle, larger for genie)

### 4. Performance Considerations

- Oracle tier optimization is faster and cheaper
- Genie tier optimization is slower due to ReAct complexity
- Once optimized weights are saved, testing and running use the same speed for both tiers
- Only the initial optimization is slower for higher tiers

## Troubleshooting

### Common Issues

#### Optimization Taking Too Long
```bash
# Cancel optimization
CTRL-C

# Check if base pipeline is intact
super agent run your_agent --goal "test"
```

#### Poor Optimization Results
```yaml
# Improve BDD scenarios
spec:
  scenarios:
    - name: "comprehensive_test"
      given: "detailed context"
      when: "specific action"
      then: "expected outcome"
```

#### Memory Issues During Optimization
```yaml
# Reduce optimization load
spec:
  optimization:
    max_examples: 3  # Reduce from 8
    max_rounds: 1    # Single round
```

## Cost Management

### ⚠️ **IMPORTANT: Optimization Can Be Expensive!**

Optimization makes **hundreds to thousands of API calls** to improve your agent's performance. With cloud LLMs, this can quickly become very expensive.

### Real Cost Examples (Approx)

| Model | Optimization Iterations | API Calls | Estimated Cost |
|-------|------------------------|-----------|----------------|
| GPT-4o | 50 | 500 | $2.50 |
| GPT-4o | 200 | 2,000 | $10.00 |
| GPT-4 | 50 | 500 | $15.00 |
| GPT-4 | 200 | 2,000 | $60.00 |

### Cost Control Strategies

#### 1. Use Local Models for Optimization

```yaml
# Switch to local model for optimization
spec:
  language_model:
    location: local
    provider: ollama
    model: llama3.1:8b  # Free local model
    temperature: 0.7
    max_tokens: 2000
```

```bash
# Optimize with local model (FREE)
super agent optimize your_agent

# Then switch back to cloud model for production
# Edit playbook to use cloud provider
super agent compile your_agent
```

#### 2. Conservative Optimization Settings

```yaml
# Conservative optimization settings
spec:
  optimization:
    strategy: bootstrap_fewshot
    max_examples: 3      # Limit demonstrations
    max_rounds: 1        # Single optimization round
```

### Safe Optimization Workflow

```bash
# Safe optimization workflow
super agent compile your_agent   # Use local model
super agent evaluate your_agent               # Establish baseline
super agent optimize your_agent               # Free optimization
super agent evaluate your_agent               # Measure improvement

# Switch to cloud for final testing
# Edit playbook to use cloud provider
super agent compile your_agent
super agent evaluate your_agent   # Minimal cloud usage
```

## 📚 Related Documentation

- [Agent Development Guide](agent-development.md) - Complete agent development workflow
- [Evaluation & Testing Guide](evaluation-testing.md) - Testing methodologies
- [BDD Guide](bdd.md) - Behavior-driven development
- [Quick Start Guide](../quick-start.md) - Getting started with SuperOptiX 