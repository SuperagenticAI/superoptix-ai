# 💻 CLI Commands API

The SuperOptiX CLI provides a comprehensive command-line interface for managing agents, models, and orchestras. This API documents all available commands and their usage.

## Main CLI Entry Point

### super

The main CLI command that provides access to all SuperOptiX functionality.

```bash
super [OPTIONS] COMMAND [ARGS]...
```

**Global Options:**
- `--version`: Show version and exit
- `--help`: Show help message and exit
- `--verbose`: Enable verbose output
- `--config`: Path to configuration file
- `--log-level`: Set logging level (DEBUG, INFO, WARNING, ERROR)

## Agent Commands

### super agent

Manage SuperOptiX agents and their lifecycle.

#### super agent init

Initialize a new SuperOptiX project.

```bash
super agent init [OPTIONS] PROJECT_NAME
```

**Arguments:**
- `PROJECT_NAME`: Name of the project to create

**Options:**
- `--template`: Template to use (basic, advanced, custom)
- `--tier`: Agent tier (oracles, genies, sage)
- `--model`: Default model to use
- `--backend`: Model backend (ollama, mlx, huggingface, lmstudio)
- `--tools`: Comma-separated list of tools to include
- `--memory`: Enable memory system
- `--rag`: Enable RAG integration
- `--output-dir`: Output directory for project files

**Example:**
```bash
super agent init my_project --tier genies --model llama3.2:8b --tools web_search,calculator
```

#### super agent create

Create a new agent from specification.

```bash
super agent create [OPTIONS] AGENT_NAME
```

**Arguments:**
- `AGENT_NAME`: Name of the agent to create

**Options:**
- `--spec`: Path to agent specification file
- `--template`: Template to use
- `--tier`: Agent tier
- `--model`: Model to use
- `--tools`: Tools to include
- `--output`: Output file path

**Example:**
```bash
super agent create my_agent --spec agent_spec.yaml --output my_agent.py
```

#### super agent compile

Compile an agent specification to executable code.

```bash
super agent compile [OPTIONS] SPEC_FILE
```

**Arguments:**
- `SPEC_FILE`: Path to agent specification file

**Options:**
- `--output`: Output file path
- `--format`: Output format (python, yaml, json)
- `--validate`: Validate specification before compilation
- `--optimize`: Enable optimization during compilation

**Example:**
```bash
super agent compile agent.yaml --output compiled_agent.py --validate
```

#### super agent run

Run an agent with a query.

```bash
super agent run [OPTIONS] AGENT_PATH QUERY
```

**Arguments:**
- `AGENT_PATH`: Path to agent file or specification
- `QUERY`: Query to run

**Options:**
- `--config`: Agent configuration file
- `--model`: Override model
- `--tools`: Override tools
- `--memory`: Enable memory
- `--tracing`: Enable tracing
- `--output`: Output file for results

**Example:**
```bash
super agent run my_agent.py "What is the weather like?" --tracing --output results.json
```

#### super agent evaluate

Evaluate an agent with test data.

```bash
super agent evaluate [OPTIONS] AGENT_PATH
```

**Arguments:**
- `AGENT_PATH`: Path to agent file or specification

**Options:**
- `--test-data`: Path to test data file
- `--metrics`: Comma-separated list of metrics
- `--scenarios`: Path to BDD scenarios file
- `--output`: Output file for evaluation results
- `--format`: Output format (json, csv, html)
- `--threshold`: Pass/fail threshold
- `--ci`: CI/CD mode with exit codes

**Example:**
```bash
super agent evaluate my_agent.py --test-data test_data.json --metrics semantic_f1,exact_match --ci
```

#### super agent optimize

Optimize an agent with training data.

```bash
super agent optimize [OPTIONS] AGENT_PATH
```

**Arguments:**
- `AGENT_PATH`: Path to agent file or specification

**Options:**
- `--training-data`: Path to training data file
- `--strategy`: Optimization strategy (BootstrapFewShot, ReAct)
- `--iterations`: Number of optimization iterations
- `--output`: Output file for optimized agent
- `--metrics`: Metrics to optimize for
- `--validate`: Validate after optimization

**Example:**
```bash
super agent optimize my_agent.py --training-data train_data.json --strategy BootstrapFewShot --iterations 10
```

#### super agent list

List available agents.

```bash
super agent list [OPTIONS]
```

**Options:**
- `--format`: Output format (table, json, yaml)
- `--filter`: Filter agents by criteria
- `--sort`: Sort by field
- `--limit`: Maximum number of agents to show

**Example:**
```bash
super agent list --format json --filter tier=genies
```

#### super agent info

Get information about an agent.

```bash
super agent info [OPTIONS] AGENT_PATH
```

**Arguments:**
- `AGENT_PATH`: Path to agent file or specification

**Options:**
- `--format`: Output format (table, json, yaml)
- `--detailed`: Show detailed information

**Example:**
```bash
super agent info my_agent.py --detailed
```

## Model Commands

### super model

Manage SuperOptiX models and their lifecycle.

#### super model list

List available models across all backends.

```bash
super model list [OPTIONS]
```

**Options:**
- `--backend`: Filter by backend (ollama, mlx, huggingface, lmstudio)
- `--size`: Filter by size (tiny, small, medium, large)
- `--task`: Filter by task (chat, code, reasoning, embedding)
- `--installed-only`: Show only installed models (default: True)
- `--all`: Show all available models
- `--verbose`: Show detailed information

**Example:**
```bash
super model list --backend ollama --size small
```

#### super model install

Install a model on a specific backend.

```bash
super model install [OPTIONS] MODEL_NAME
```

**Arguments:**
- `MODEL_NAME`: Name of the model to install

**Options:**
- `--backend`: Backend to install on (ollama, mlx, huggingface, lmstudio)


**Example:**
```bash
super model install llama3.2:3b --backend ollama
```

#### super model run

Run a prompt against a SuperOptiX model with automatic installation.

```bash
super model run [OPTIONS] MODEL_NAME PROMPT
```

**Arguments:**
- `MODEL_NAME`: Name of the model to run
- `PROMPT`: Prompt to send to the model

**Options:**
- `--backend`: Backend to use (ollama, mlx, huggingface) - auto-detected if not specified
- `--interactive`: Run in interactive mode
- `--max-tokens`: Maximum tokens to generate (default: 2048)
- `--temperature`: Temperature for generation 0.0-2.0 (default: 0.7)

**Features:**
- **Auto-installation:** Automatically installs models if not found
- **Backend auto-detection:** Finds the correct backend for the model
- **Interactive mode:** Supports conversation mode with history
- **Real-time execution:** Direct model execution without server setup

**Supported Backends:**
- **Ollama:** Uses `ollama run` command
- **MLX:** Downloads and uses MLX-LM directly
- **HuggingFace:** Downloads and uses transformers pipeline directly
- **LM Studio:** Not supported (designed for server mode)

**Examples:**
```bash
# Single prompt execution
super model run llama3.2:3b "Write a Python function to add two numbers" --backend ollama

# Interactive mode
super model run llama3.2:3b "" --backend ollama --interactive

# Auto-detection with auto-installation
super model run mlx-community/Llama-3.2-3B-Instruct-4bit "Write a hello world program" --backend mlx

# HuggingFace with auto-installation
super model run microsoft/phi-1_5 "Write a simple calculator" --backend huggingface
```

#### super model remove

Remove a model from a specific backend.

```bash
super model remove [OPTIONS] MODEL_NAME
```

**Arguments:**
- `MODEL_NAME`: Name of the model to remove

**Options:**
- `--backend`: Backend to remove from (auto-detected if not specified)

- `--all-backends`: Remove from all backends where it exists

**Example:**
```bash
super model remove llama3.2:3b --backend ollama
```

#### super model refresh

Refresh the SuperOptiX model cache.

```bash
super model refresh
```

**Example:**
```bash
super model refresh
```

#### super model info

Get detailed information about a model.

```bash
super model info MODEL_NAME
```

**Arguments:**
- `MODEL_NAME`: Name of the model to get info about

**Example:**
```bash
super model info llama3.2:3b
```

#### super model server

Start a model server for local inference.

```bash
super model server [OPTIONS] BACKEND MODEL_NAME
```

**Arguments:**
- `BACKEND`: Backend type (mlx, huggingface, lmstudio)
- `MODEL_NAME`: Name of the model to serve

**Options:**
- `--port`: Port to run server on

**Example:**
```bash
super model server mlx mlx-community/Llama-3.2-3B-Instruct-4bit --port 8000
```

#### super model dspy

Create a DSPy client for a model.

```bash
super model dspy [OPTIONS] MODEL_NAME
```

**Arguments:**
- `MODEL_NAME`: Name of the model for DSPy client

**Options:**
- `--temperature`: Temperature for generation (default: 0.7)
- `--max-tokens`: Maximum tokens (default: 2048)

**Example:**
```bash
super model dspy ollama/llama3.2:3b --temperature 0.8
```

#### super model convert

Convert HuggingFace model to MLX format (EXPERIMENTAL).

```bash
super model convert [OPTIONS] HF_MODEL
```

**Arguments:**
- `HF_MODEL`: HuggingFace model to convert (e.g., 'microsoft/phi-2')

**Options:**
- `--output`: Output path for converted model (default: model name)
- `--quantize`: Generate a quantized model
- `--bits`: Bits per weight for quantization (default: 4)
- `--group-size`: Group size for quantization (default: 64)
- `--quant-recipe`: Mixed quantization recipe (mixed_2_6, mixed_3_4, mixed_3_6, mixed_4_6)
- `--dtype`: Data type (float16, bfloat16, float32)
- `--upload`: HuggingFace repo to upload converted model to
- `--dequantize`: Dequantize a quantized model
- `--trust-remote-code`: Trust remote code from HuggingFace

**Note:** This command is experimental and requires MLX backend to be available.

**Example:**
```bash
super model convert microsoft/phi-2 --quantize --bits 4
```

#### super model quantize

Quantize or dequantize an MLX model (EXPERIMENTAL).

```bash
super model quantize [OPTIONS] MODEL_NAME
```

**Arguments:**
- `MODEL_NAME`: MLX model to quantize

**Options:**
- `--output`: Output path for quantized model
- `--bits`: Bits per weight for quantization (default: 4)
- `--group-size`: Group size for quantization (default: 64)
- `--recipe`: Mixed quantization recipe (mixed_2_6, mixed_3_4, mixed_3_6, mixed_4_6)
- `--dequantize`: Dequantize instead of quantize

**Note:** This command is experimental and requires MLX backend to be available.

**Example:**
```bash
super model quantize my-model --bits 4 --output my-model-q4
```

#### super model discover

Discover available models across backends.

```bash
super model discover
```

**Example:**
```bash
super model discover
```

#### super model guide

Show installation guide for different backends.

```bash
super model guide
```

**Example:**
```bash
super model guide
```

#### super model backends

List available backends and their status.

```bash
super model backends
```

**Example:**
```bash
super model backends
```

## Marketplace Commands

### super market

Access the SuperOptiX marketplace for agents and tools.

#### super market browse

Browse marketplace items.

```bash
super market browse [OPTIONS] [CATEGORY]
```

**Arguments:**
- `CATEGORY`: Category to browse (agents, tools, templates)

**Options:**
- `--format`: Output format (table, json, yaml)
- `--limit`: Maximum items to show
- `--sort`: Sort by field
- `--filter`: Filter by criteria

**Example:**
```bash
super market browse agents --format json --limit 10
```

#### super market search

Search marketplace items.

```bash
super market search [OPTIONS] QUERY
```

**Arguments:**
- `QUERY`: Search query

**Options:**
- `--category`: Search category
- `--format`: Output format
- `--limit`: Maximum results
- `--sort`: Sort by relevance or date

**Example:**
```bash
super market search "customer service" --category agents --limit 5
```

#### super market install

Install marketplace item.

```bash
super market install [OPTIONS] ITEM_NAME
```

**Arguments:**
- `ITEM_NAME`: Name of the item to install

**Options:**
- `--version`: Item version
- `--output-dir`: Output directory
- `--verify`: Verify installation
- `--dependencies`: Install dependencies

**Example:**
```bash
super market install customer-service-agent --version 1.0.0 --output-dir ./agents
```

#### super market info

Get information about marketplace item.

```bash
super market info [OPTIONS] ITEM_NAME
```

**Arguments:**
- `ITEM_NAME`: Name of the item

**Options:**
- `--version`: Item version
- `--format`: Output format

**Example:**
```bash
super market info customer-service-agent --format json
```

## SuperSpec Commands

### super spec

Manage SuperSpec specifications and DSL.

#### super spec validate

Validate a SuperSpec specification.

```bash
super spec validate [OPTIONS] SPEC_FILE
```

**Arguments:**
- `SPEC_FILE`: Path to specification file

**Options:**
- `--schema`: Custom schema file
- `--strict`: Strict validation mode
- `--output`: Output file for validation results

**Example:**
```bash
super spec validate agent.yaml --strict --output validation.json
```

#### super spec generate

Generate code from SuperSpec specification.

```bash
super spec generate [OPTIONS] SPEC_FILE
```

**Arguments:**
- `SPEC_FILE`: Path to specification file

**Options:**
- `--output`: Output file path
- `--template`: Template to use
- `--format`: Output format (python, yaml, json)
- `--validate`: Validate before generation

**Example:**
```bash
super spec generate agent.yaml --output generated_agent.py --template advanced
```

#### super spec lint

Lint a SuperSpec specification.

```bash
super spec lint [OPTIONS] SPEC_FILE
```

**Arguments:**
- `SPEC_FILE`: Path to specification file

**Options:**
- `--rules`: Custom linting rules file
- `--output`: Output file for linting results
- `--fix`: Auto-fix issues where possible

**Example:**
```bash
super spec lint agent.yaml --fix --output linting.json
```

## Orchestra Commands

### super orchestra

Manage multi-agent orchestras.

#### super orchestra create

Create a new orchestra.

```bash
super orchestra create [OPTIONS] ORCHESTRA_NAME
```

**Arguments:**
- `ORCHESTRA_NAME`: Name of the orchestra

**Options:**
- `--config`: Orchestra configuration file
- `--agents`: Comma-separated list of agent paths
- `--workflow`: Workflow type (pipeline, broadcast, conditional)
- `--output`: Output file path

**Example:**
```bash
super orchestra create data_pipeline --agents agent1.py,agent2.py,agent3.py --workflow pipeline
```

#### super orchestra run

Run an orchestra.

```bash
super orchestra run [OPTIONS] ORCHESTRA_PATH
```

**Arguments:**
- `ORCHESTRA_PATH`: Path to orchestra file

**Options:**
- `--input`: Input data file
- `--config`: Orchestra configuration
- `--workflow`: Override workflow type
- `--output`: Output file for results
- `--monitor`: Enable monitoring

**Example:**
```bash
super orchestra run data_pipeline.yaml --input data.json --monitor --output results.json
```

#### super orchestra list

List available orchestras.

```bash
super orchestra list [OPTIONS]
```

**Options:**
- `--format`: Output format
- `--filter`: Filter orchestras
- `--sort`: Sort by field

**Example:**
```bash
super orchestra list --format json --filter status=active
```

## Observability Commands

### super observability

Manage observability and monitoring.

#### super observability dashboard

Start observability dashboard.

```bash
super observability dashboard [OPTIONS]
```

**Options:**
- `--port`: Dashboard port
- `--host`: Dashboard host
- `--traces-dir`: Traces directory
- `--config`: Dashboard configuration

**Example:**
```bash
super observability dashboard --port 8080 --host 0.0.0.0
```

#### super observability traces

Manage trace data.

```bash
super observability traces [OPTIONS] COMMAND [ARGS]...
```

**Commands:**
- `list`: List available traces
- `show`: Show trace details
- `export`: Export traces
- `clear`: Clear traces

**Example:**
```bash
super observability traces list --agent-id my_agent --limit 10
```

#### super observability metrics

Manage metrics.

```bash
super observability metrics [OPTIONS] COMMAND [ARGS]...
```

**Commands:**
- `list`: List available metrics
- `show`: Show metric values
- `export`: Export metrics
- `reset`: Reset metrics

**Example:**
```bash
super observability metrics show --metric response_time --agent-id my_agent
```

## Configuration Commands

### super config

Manage SuperOptiX configuration.

#### super config show

Show current configuration.

```bash
super config show [OPTIONS]
```

**Options:**
- `--format`: Output format
- `--section`: Show specific section

**Example:**
```bash
super config show --format json --section models
```

#### super config set

Set configuration value.

```bash
super config set [OPTIONS] KEY VALUE
```

**Arguments:**
- `KEY`: Configuration key
- `VALUE`: Configuration value

**Options:**
- `--global`: Set global configuration
- `--project`: Set project configuration

**Example:**
```bash
super config set models.default_backend ollama --global
```

#### super config get

Get configuration value.

```bash
super config get [OPTIONS] KEY
```

**Arguments:**
- `KEY`: Configuration key

**Options:**
- `--global`: Get global configuration
- `--project`: Get project configuration

**Example:**
```bash
super config get models.default_backend --global
```

#### super config reset

Reset configuration to defaults.

```bash
super config reset [OPTIONS]
```

**Options:**
- `--global`: Reset global configuration
- `--project`: Reset project configuration
- `--confirm`: Skip confirmation prompt

**Example:**
```bash
super config reset --global --confirm
```

## Utility Commands

### super utils

Utility commands for common tasks.

#### super utils validate

Validate SuperOptiX installation.

```bash
super utils validate [OPTIONS]
```

**Options:**
- `--check-models`: Check model availability
- `--check-backends`: Check backend availability
- `--check-tools`: Check tool availability
- `--output`: Output file for validation results

**Example:**
```bash
super utils validate --check-models --check-backends --output validation.json
```

#### super utils cleanup

Clean up temporary files and caches.

```bash
super utils cleanup [OPTIONS]
```

**Options:**
- `--traces`: Clean up trace files
- `--models`: Clean up model caches
- `--logs`: Clean up log files
- `--all`: Clean up everything
- `--confirm`: Skip confirmation prompt

**Example:**
```bash
super utils cleanup --traces --logs --confirm
```

#### super utils export

Export SuperOptiX data.

```bash
super utils export [OPTIONS] DATA_TYPE
```

**Arguments:**
- `DATA_TYPE`: Type of data to export (agents, models, traces, config)

**Options:**
- `--output`: Output file path
- `--format`: Export format (json, yaml, csv)
- `--filter`: Filter data

**Example:**
```bash
super utils export agents --output agents.json --format json
```

## Environment Variables

The SuperOptiX CLI supports various environment variables for configuration:

```bash
# Model configuration
SUPEROPTIX_DEFAULT_BACKEND=ollama
SUPEROPTIX_DEFAULT_MODEL=llama3.2:8b
SUPEROPTIX_MODEL_CACHE_DIR=/path/to/cache

# API keys
SUPEROPTIX_OPENAI_API_KEY=your_openai_key
SUPEROPTIX_ANTHROPIC_API_KEY=your_anthropic_key
SUPEROPTIX_WEB_SEARCH_API_KEY=your_search_key

# Logging
SUPEROPTIX_LOG_LEVEL=INFO
SUPEROPTIX_LOG_FILE=/path/to/logs

# Tracing
SUPEROPTIX_TRACES_DIR=/path/to/traces
SUPEROPTIX_ENABLE_TRACING=true

# Memory
SUPEROPTIX_MEMORY_BACKEND=sqlite
SUPEROPTIX_MEMORY_PATH=/path/to/memory

# Development
SUPEROPTIX_DEV_MODE=true
SUPEROPTIX_DEBUG=true
```

## Configuration Files

### Global Configuration

Located at `~/.superoptix/config.yaml`:

```yaml
models:
  default_backend: ollama
  default_model: llama3.2:8b
  cache_dir: ~/.superoptix/models

tools:
  default_tools:
    - WebSearchTool
    - CalculatorTool
  api_keys:
    web_search: ${WEB_SEARCH_API_KEY}

memory:
  default_backend: sqlite
  default_path: ~/.superoptix/memory

observability:
  traces_dir: ~/.superoptix/traces
  enable_tracing: true
  log_level: INFO

development:
  dev_mode: false
  debug: false
```

### Project Configuration

Located at `./superoptix.yaml`:

```yaml
project:
  name: my_project
  version: 1.0.0
  description: My SuperOptiX project

agents:
  - name: my_agent
    file: agents/my_agent.py
    tier: genies
    model: llama3.2:8b

orchestras:
  - name: my_orchestra
    file: orchestras/my_orchestra.yaml
    workflow: pipeline

tools:
  - name: custom_tool
    file: tools/custom_tool.py

memory:
  backend: sqlite
  path: ./memory

evaluation:
  test_data: ./test_data.json
  scenarios: ./scenarios.yaml
  metrics:
    - semantic_f1
    - exact_match
```

## Exit Codes

The SuperOptiX CLI uses the following exit codes:

- `0`: Success
- `1`: General error
- `2`: Configuration error
- `3`: Validation error
- `4`: Model error
- `5`: Agent error
- `6`: Evaluation failure
- `7`: Optimization error
- `8`: Network error
- `9`: Permission error
- `10`: Resource error

## Examples

### Complete Workflow

```bash
# Initialize project
super agent init my_project --tier genies --model llama3.2:8b

# Create agent
super agent create my_agent --spec agent_spec.yaml

# Compile agent
super agent compile agent_spec.yaml --output my_agent.py

# Run agent
super agent run my_agent.py "Hello, world!"

# Evaluate agent
super agent evaluate my_agent.py --test-data test_data.json --ci

# Optimize agent
super agent optimize my_agent.py --training-data train_data.json

# Create orchestra
super orchestra create my_orchestra --agents agent1.py,agent2.py --workflow pipeline

# Run orchestra
super orchestra run my_orchestra.yaml --input data.json

# Monitor with dashboard
super observability dashboard --port 8080
```

### CI/CD Integration

```bash
# Validate specification
super spec validate agent.yaml --strict

# Run evaluation with CI mode
super agent evaluate agent.py --test-data test_data.json --ci --threshold 0.8

# Check exit code
if [ $? -eq 6 ]; then
    echo "Evaluation failed"
    exit 1
fi
```

### Model Management

```bash
# List available models
super model list --backend ollama --installed-only

# Install model
super model install llama3.2:8b --backend ollama --progress

# Start model server
super model server llama3.2:8b --port 8000

# Get model info
super model info llama3.2:8b --backend ollama --format json
``` 