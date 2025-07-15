# 🏗️ Project Structure Guide

This guide shows you how to create and explore a real SuperOptiX Agentic System project using the CLI, and explains the meaning of each directory and file.

---

## 🚀 Step 1: Initialize Your Agentic System

To start, create a new Agentic System project using the `super init` command. For example, to create a software engineering system called `swe`:

```bash
super init swe
```

You’ll see a message confirming your project is ready.

---

## 📂 Step 2: Explore the Project Structure

Change into your new project directory:

```bash
cd swe
ls -la
```

You’ll see output like:

```
total 48
drwxr-xr-x@ 10 user  staff   320 ... ./
drwxr-xr-x  ... ../
-rw-r--r--@  1 user  staff   ... .env
-rw-r--r--@  1 user  staff   ... .gitignore
-rw-r--r--@  1 user  staff   ... .pre-commit-config.yaml
-rw-r--r--@  1 user  staff   ... .super
-rw-r--r--@  1 user  staff   ... README.md
-rw-r--r--@  1 user  staff   ... pyproject.toml
drwxr-xr-x@ 12 user  staff   ... swe/
drwxr-xr-x@  5 user  staff   ... tests/
```

**Key files and folders:**

- **📄 `.super`** — This file marks the root of your Agentic System. Always run `super` commands from this directory.

- **⚙️ `pyproject.toml`** — Python package configuration for your agentic system.

- **📖 `README.md`** — Project overview and documentation.

- **📦 `swe/`** — Main Python package for your agentic modules and logic.

- **🧪 `tests/`** — Place your tests here.

---

## 🧩 Step 3: Explore the Agentic Modules

List the contents of the main package directory:

```bash
ls -la swe/
```

You’ll see subdirectories for each agentic module:

```
agents/     guardrails/ memory/     protocols/  teams/
evals/      knowledge/  optimizers/ servers/    tools/
```

**Directory meanings:**

- **🤖 `agents/`** — Each agent lives in its own subdirectory here. Agent playbooks, pipelines, and optimized pipelines are stored here.

- **🛡️ `guardrails/`** — Guardrails for safety, validation, and compliance.

- **🧠 `memory/`** — Memory modules for your agents.

- **📡 `protocols/`** — Communication and orchestration protocols.

- **👥 `teams/`** — Multi-agent team configurations.

- **✅ `evals/`** — Evaluation scenarios and test cases.

- **📚 `knowledge/`** — Knowledge bases and data sources.

- **⚡ `optimizers/`** — Optimization strategies and modules.

- **🌐 `servers/`** — Server and API integration code.

- **🔧 `tools/`** — Custom tools and utilities for your agents.

---

## 🏷️ Step 4: Pull and Compile an Agent

Let’s add a pre-built agent and see what files are created.

```bash
super agent pull developer
```

This creates a new agent directory structure:

**📁 `swe/agents/developer/`**
- **📋 `playbook/`** — Contains the agent's configuration files
  - **📄 `developer_playbook.yaml`** — Agent definition and configuration

---

Now compile the agent:

```bash
super agent compile developer
```

This generates a pipeline structure:

**📁 `swe/agents/developer/`**
- **📋 `playbook/`** — Agent configuration files
  - **📄 `developer_playbook.yaml`** — Agent definition
- **⚙️ `pipelines/`** — Generated pipeline files
  - **🐍 `developer_pipeline.py`** — Executable agent pipeline

---

## 📜 Step 5: Explore Agent Files

**Agent Playbook:**  
`swe/agents/developer/playbook/developer_playbook.yaml`  
This YAML file defines the agent’s persona, tasks, evaluation scenarios, and optimization strategy.

**Agent Pipeline:**  
`swe/agents/developer/pipelines/developer_pipeline.py`  
This Python file is an auto-generated, executable pipeline for the agent, ready for further customization.

---

## 📝 Example: Playbook and Pipeline

**Playbook (YAML):**
```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: Developer Assistant
  id: developer
  ...
spec:
  language_model:
    provider: ollama
    model: llama3.2:1b
    api_base: http://localhost:11434
  persona:
    name: DevBot
    role: Software Developer
    goal: Write clean, efficient, and maintainable code
  ...
```

**Pipeline (Python):**
```python
class DeveloperPipeline(
    TracingMixin,
    ModelSetupMixin, 
    ToolsMixin,
    BDDTestMixin,
    UsageTrackingMixin,
    EvaluationMixin
):
    ...
    def __init__(self):
        ...
        self.module = DeveloperModule()
        ...
```

---

## 💡 Tips

- All `super` CLI commands (e.g., `super agent`, `super orchestra`, `super spec`) must be run from the root directory containing the `.super` file.
- Each agent’s logic, playbooks, and pipelines are isolated in their own subdirectories under `agents/`.
- The project is a standard Python package — you can ship and reuse it in other Agentic Systems. 