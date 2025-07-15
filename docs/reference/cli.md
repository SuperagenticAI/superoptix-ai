# SuperOptiX CLI Reference

Welcome to the comprehensive SuperOptiX CLI reference! This document covers all available commands, their options, and usage examples, reflecting the actual implementation.

## Table of Contents

- [Getting Started](#getting-started)
- [Core Commands](#core-commands)
  - [init](#init)
  - [docs](#docs)
- [Agent Management (`agent` or `ag`)](#agent-management-agent-or-ag)
  - [agent pull](#agent-pull)
  - [agent compile](#agent-compile)
  - [agent design](#agent-design)
  - [agent inspect](#agent-inspect)
  - [agent lint](#agent-lint)
  - [agent list](#agent-list)
  - [agent optimize](#agent-optimize)
  - [agent evaluate](#agent-evaluate)
  - [agent run](#agent-run)
  - [agent rm](#agent-rm)
  - [agent tier-status](#agent-tier-status)
- [Model Intelligence System (`model` or `md`)](#model-intelligence-system-model-or-md)
  - [model list](#model-list)
  - [model discover](#model-discover)
  - [model guide](#model-guide)
  - [model install](#model-install)
  - [model info](#model-info)
  - [model backends](#model-backends)
  - [model dspy](#model-dspy)
  - [model server](#model-server)
- [SuperSpec DSL (`spec`)](#superspec-dsl-spec)
  - [spec generate](#spec-generate)
  - [spec validate](#spec-validate)
  - [spec analyze](#spec-analyze)
  - [spec info](#spec-info)
  - [spec schema](#spec-schema)
  - [spec bootstrap](#spec-bootstrap)
- [Orchestra Management (`orchestra` or `orch`)](#orchestra-management-orchestra-or-orch)
  - [orchestra create](#orchestra-create)
  - [orchestra list](#orchestra-list)
  - [orchestra run](#orchestra-run)
- [Marketplace (`marketplace`, `market` or `mk`)](#marketplace-marketplace-market-or-mk)
  - [marketplace](#marketplace-1)
  - [marketplace browse](#marketplace-browse)
  - [marketplace search](#marketplace-search)
  - [marketplace show](#marketplace-show)
  - [marketplace featured](#marketplace-featured)
  - [marketplace install](#marketplace-install)
- [Observability (`observe` or `ob`)](#observability-observe-or-ob)
  - [observe dashboard](#observe-dashboard)
  - [observe traces](#observe-traces)
  - [observe check](#observe-check)
  - [observe analyze](#observe-analyze)
  - [observe list](#observe-list)
  - [observe debug](#observe-debug)

## Getting Started

### Basic Workflow

```bash
# 1. Initialize a new project
super init my_project
cd my_project

# 2. Generate an agent using SuperSpec DSL
super spec generate genies developer --namespace software

# 3. Compile the agent
super agent compile developer

# 4. Evaluate the agent
super agent evaluate developer

# 5. Run the agent
super agent run developer --goal "Implement a basic calculator"
```

### Quick Reference

```bash
# Project management
super init <project_name>           # Initialize new project
super docs                          # Show comprehensive guide

# Agent lifecycle
super agent pull <name>             # Add pre-built agent
super agent compile <name>          # Compile agent to Python
super agent evaluate <name>         # Test agent with BDD
super agent run <name> --goal <goal> # Execute agent
super agent list                    # List project agents

# Model management
super model list                    # List installed models
super model install <model>         # Install model
super model server <backend> <model> # Start local server

# DSL and development
super spec generate <tier> <name>   # Generate agent playbook
super spec validate <file>          # Validate playbook
super spec analyze <path>           # Analyze playbooks

# Multi-agent workflows
super orchestra create <name>       # Create orchestra
super orchestra run <name> --goal <goal> # Run orchestra

# Discovery and tools
super marketplace                   # Browse marketplace
super marketplace search <query>    # Search components
super marketplace install agent <name> # Install agent

# Monitoring and debugging
super observe dashboard             # Launch observability dashboard
super observe traces <agent_id>     # View execution traces
```

## Core Commands

### init

Initialize a new SuperOptiX project with the complete directory structure.

```bash
super init <project_name>
```

**Arguments:**
- `project_name` - Name of the agentic system (required)

**Example:**
```bash
super init my_ai_project
```

### docs

Display comprehensive SuperOptiX documentation with examples and getting started information.

```bash
super docs
```

## Agent Management (`agent` or `ag`)

### agent pull

Pull a pre-built agent into your project from the SuperOptiX library. This command has an alias `pl`.

```bash
super agent pull <name> [options]
```

**Arguments:**
- `name` - Name of the pre-built agent to add (required)

**Options:**
- `--tier {oracles,genies}` - Agent tier level (default: oracles)
- `--force` - Force overwrite if agent already exists

### agent compile

Compile an agent playbook into executable Python code. This command has an alias `co`.

```bash
super agent compile [name] [options]
```

**Arguments:**
- `name` - Name of the agent to compile (optional if using --all)

**Options:**
- `--tier {oracles,genies}` - Override playbook tier for compilation
- `--all` - Compile all agents in the project
- `--abstracted` - Use abstracted pipeline with SuperOptixPipeline base class

### agent design

Interactively design an agent. This command has an alias `de`.

```bash
super agent design <agent> [options]
```

**Arguments:**
- `agent` - Name of the agent to design (required)

**Options:**
- `--tier` - Specify the agent tier for the designer

### agent inspect

Show detailed information and metadata about an agent. This command has an alias `in`.

```bash
super agent inspect <name>
```

**Arguments:**
- `name` - Name of the agent to inspect (required)

### agent lint

Validate agent playbooks for syntax and best practices. This command has an alias `li`.

```bash
super agent lint [name] [options]
```

**Arguments:**
- `name` - Name of the agent to lint (optional if using --all)

**Options:**
- `--all` - Lint all agents in the project

### agent list

List all agents in the project or pre-built agents available. This command has aliases `ls` and `ps`.

```bash
super agent list [options]
```

**Options:**
- `--pre-built` - List all available pre-built agents from the library
- `--industry` - Filter pre-built agents by industry

### agent optimize

Optimize an agent pipeline using DSPy optimization techniques. This command has an alias `op`.

```bash
super agent optimize <name> [options]
```

**Arguments:**
- `name` - Name of the agent to optimize (required)

**Options:**
- `--force` - Force re-optimization even if an optimized version already exists.

### agent evaluate

Evaluate an agent using its BDD specification tests. This command has an alias `ev`.

```bash
super agent evaluate <name> [options]
```

**Arguments:**
- `name` - Name of the agent to evaluate (required)

**Options:**
- `--auto-tune` - Enable auto-tuning for evaluation metrics
- `--ignore-checks` - Ignore non-essential checks during testing
- `--verbose, -v` - Show detailed results for each BDD specification
- `--format {table,json,junit}` - Output format for test results (default: table)
- `--save-report FILE` - Save detailed test report to a file

### agent run

Execute an agent with a specific goal. This command has an alias `ru`.

```bash
super agent run <name> --goal <goal>
```

**Arguments:**
- `name` - Name of the agent to run (required)
- `--goal` - Goal description for the agent (required)

### agent rm

Remove an agent from your project.

```bash
super agent rm <name>
```

**Arguments:**
- `name` - Name of the agent to remove (required)

This command will prompt for confirmation before deleting the agent's playbook and compiled pipeline files.

### agent tier-status

Show tier status and capabilities of agents in the project. This command has an alias `ts`.

```bash
super agent tier-status
```

## Model Intelligence System (`model` or `md`)

### model list

List SuperOptiX models (installed by default). This command has an alias `ls`.

```bash
super model list [options]
```

**Options:**
- `--backend {ollama,mlx,huggingface,lmstudio}` - Filter by backend
- `--size {tiny,small,medium,large}` - Filter by size
- `--task {chat,code,reasoning,embedding}` - Filter by task
- `--installed-only` - Show only installed models (default)
- `--all` - Show all available models
- `--verbose, -v` - Show detailed information

### model discover

Show SuperOptiX Model Discovery Guide. This command has an alias `disc`.

```bash
super model discover
```

### model guide

Show SuperOptiX Model Installation Guide. This command has an alias `g`.

```bash
super model guide
```

### model install

Install a SuperOptiX model. This command has an alias `i`.

```bash
super model install <model_name> [options]
```

**Arguments:**
- `model_name` - Model name to install (required)

**Options:**
- `--backend, -b {ollama,mlx,huggingface,lmstudio}` - Specify backend
- `--force, -f` - Force reinstall if already exists

### model info

Get detailed information about a SuperOptiX model. This command has an alias `inf`.

```bash
super model info <model_name>
```

**Arguments:**
- `model_name` - Model name to get info about (required)

### model backends

Show SuperOptiX backend status. This command has an alias `b`.

```bash
super model backends
```

### model dspy

Create DSPy client for SuperOptiX model. This command has an alias `d`.

```bash
super model dspy <model_name> [options]
```

**Arguments:**
- `model_name` - Model name for DSPy client (required)

**Options:**
- `--temperature, -t` - Temperature for generation (default: 0.7)
- `--max-tokens, -m` - Maximum tokens (default: 2048)

### model server

Start local server for SuperOptiX models. This command has an alias `srv`.

```bash
super model server <backend> <model_name> [options]
```

**Arguments:**
- `backend` - Backend type: mlx, huggingface, lmstudio (required)
- `model_name` - Model name to start server for (required)

**Options:**
- `--port, -p` - Port to run server on

## SuperSpec DSL (`spec`)

### spec generate

Generate agent playbook templates with customizable features. This command has an alias `gen`.

```bash
super spec generate <tier> <name> [options]
```

**Arguments:**
- `tier` - Agent tier: oracles or genies (required)
- `name` - Agent name (required)

**Options:**
- `--namespace` - Agent namespace (default: software)
- `--role` - Agent role description (default: Assistant)
- `--description` - Detailed agent description
- `--output` - Output directory or file path
- `--format` - Output format: yaml or json (default: yaml)
- `--memory/--no-memory` - Enable/disable memory system (Genie only, default: true)
- `--tools/--no-tools` - Enable/disable tool integration (Genie only, default: true)
- `--rag` - Enable RAG/retrieval (Genie only, default: false)

### spec validate

Validate agent playbook files. This command has an alias `val`.

```bash
super spec validate <files> [options]
```

**Arguments:**
- `files` - One or more playbook files to validate (required)

**Options:**
- `--verbose, -v` - Show detailed validation output
- `--format {table,json}` - Output format (default: table)

### spec analyze

Get insights about your playbooks. This command has an alias `an`.

```bash
super spec analyze <path> [options]
```

**Arguments:**
- `path` - Directory or file path to analyze (required)

**Options:**
- `--pattern` - File pattern to match (default: *.yaml)
- `--format {table,json}` - Output format (default: table)

### spec info

Show detailed agent information. This command has an alias `inf`.

```bash
super spec info <file>
```

**Arguments:**
- `file` - Agent playbook file (required)

### spec schema

Show DSL schema information. This command has an alias `sch`.

```bash
super spec schema [options]
```

**Options:**
- `--tier {oracles,genies}` - Show features for specific tier

### spec bootstrap

Bootstrap agents for a namespace. This command has an alias `boot`.

```bash
super spec bootstrap <namespace> [options]
```

**Arguments:**
- `namespace` - Target namespace (required)

**Options:**
- `--output-dir` - Output directory (default: ./generated_agents)
- `--tiers` - Tiers to generate (default: both oracles and genies)

## Orchestra Management (`orchestra` or `orch`)

### orchestra create

Create a new orchestra definition file. This command has an alias `cr`.

```bash
super orchestra create <name>
```

**Arguments:**
- `name` - Name of the orchestra to create (required)

### orchestra list

List all orchestras in the project. This command has an alias `ls`.

```bash
super orchestra list
```

### orchestra run

Run an orchestra with a specific goal. This command has an alias `ru`.

```bash
super orchestra run <name> --goal <goal>
```

**Arguments:**
- `name` - Name of the orchestra to run (required)
- `--goal` - Goal description for the orchestra (required)

## Marketplace (`marketplace`, `market` or `mk`)

### marketplace

Show the main marketplace dashboard.

```bash
super marketplace
```

### marketplace browse

Browse marketplace by category. This command has an alias `br`.

```bash
super marketplace browse <type> [options]
```

**Arguments:**
- `type` - What to browse: agents, tools, industries, or categories (required)

**Options:**
- `--industry` - Filter agents by industry
- `--category` - Filter tools by category
- `--tier {oracles,genies}` - Filter by tier level

### marketplace search

Universal search across agents and tools. This command has an alias `se`.

```bash
super marketplace search <query>
```

**Arguments:**
- `query` - Search term or phrase (required)

### marketplace show

Show detailed information about a component. This command has an alias `sh`.

```bash
super marketplace show <name>
```

**Arguments:**
- `name` - Name of the component to show (required)

### marketplace featured

Show featured/popular components. This command has an alias `fe`.

```bash
super marketplace featured
```

### marketplace install

Install a component (convenience wrapper). This command has an alias `in`.

```bash
super marketplace install <type> <name>
```

**Arguments:**
- `type` - Type of component: agent or tool (required)
- `name` - Name of the component to install (required)

## Observability (`observe` or `ob`)

### observe dashboard

Launch the observability dashboard. This command has an alias `db`.

```bash
super observe dashboard [options]
```

**Options:**
- `--agent-id` - Agent ID to monitor (optional)
- `--port` - Dashboard port (default: 8501)
- `--host` - Dashboard host (default: localhost)
- `--auto-open` - Auto-open browser

### observe traces

View and export agent execution traces. This command has an alias `tr`.

```bash
super observe traces <agent_id> [options]
```

**Arguments:**
- `agent_id` - The agent ID to view traces for (required)

**Options:**
- `--component` - Filter by component
- `--status` - Filter by status
- `--limit` - Limit number of traces (default: 100)
- `--export {json,csv}` - Export format
- `--output` - Output file path
- `--detailed` - Show detailed trace analysis
- `--show-tools` - Show tool execution details
- `--show-llm` - Show LLM call details

### observe check

Check pipeline tracing configuration. This command has an alias `ch`.

```bash
super observe check [options]
```

**Options:**
- `--agent-id` - Agent ID to test (optional)
- `--run-test` - Run a test agent execution
- `--check-dspy` - Check DSPy configuration

### observe analyze

Analyze agent performance. This command has an alias `an`.

```bash
super observe analyze <agent_id> [options]
```

**Arguments:**
- `agent_id` - The agent ID to analyze (required)

**Options:**
- `--days` - Number of days to analyze (default: 7)

### observe list

List all agents with trace files. This command has an alias `ls`.

```bash
super observe list
```

### observe debug

Debug an agent.

```bash
super observe debug agent <agent_id> [options]
```

**Arguments:**
- `agent_id` - Agent ID to debug (required)

**Options:**
- `--enable-step-mode` - Enable step-by-step debugging
- `--break-on-error` - Break on error
- `--break-on-memory` - Break on memory operations 