# 🎯 SuperSpec DSL Reference

<div style="text-align: center; margin: 2rem 0; padding: 1.5rem; background: linear-gradient(135deg, var(--md-primary-fg-color--light) 0%, var(--md-accent-fg-color--light) 50%, var(--md-primary-fg-color--lighter) 100%); border-radius: var(--border-radius); color: var(--md-default-fg-color); border: 2px solid var(--md-primary-fg-color--light);">
    <h2 style="color: var(--md-default-fg-color);">🎯 SuperSpec DSL Reference</h2>
    <p style="font-size: 1.1rem; margin-bottom: 1rem; color: var(--md-default-fg-color);">
        <strong>Complete reference for the SuperSpec Agent Playbook Definition Language</strong><br>
        Based on the actual SuperOptiX library implementation
    </p>
</div>

## 📋 **Overview**

SuperSpec is the declarative DSL (Domain Specific Language) for defining AI agent playbooks in SuperOptiX. It provides a structured, validated way to specify agent behavior, capabilities, and configuration.

### **Core Components**

- **Parser** - Parses YAML/JSON playbook files into structured objects
- **Validator** - Validates playbooks against schema and tier constraints
- **Generator** - Creates playbook templates for different tiers and namespaces
- **Schema** - Defines the structure and validation rules

## 🔧 **API Reference**

### **SuperSpecParser**

Parses agent playbook files according to the SuperSpec DSL specification.

```python
from superoptix.superspec import SuperSpecParser

parser = SuperSpecParser()
```

#### **Methods**

##### `parse_file(file_path: Union[str, Path]) -> Optional[AgentSpec]`

Parse a playbook file from disk.

```python
# Parse a YAML playbook file
spec = parser.parse_file("agents/my-agent/playbook/my-agent_playbook.yaml")

# Parse a JSON playbook file
spec = parser.parse_file("agents/my-agent/playbook/my-agent_playbook.json")
```

**Parameters:**
- `file_path` - Path to the playbook file (YAML or JSON)

**Returns:**
- `AgentSpec` object or `None` if parsing failed

##### `parse_dict(data: Dict[str, Any], source: str = "dict") -> Optional[AgentSpec]`

Parse a dictionary containing playbook data.

```python
playbook_data = {
    "apiVersion": "agent/v1",
    "kind": "AgentSpec",
    "metadata": {...},
    "spec": {...}
}

spec = parser.parse_dict(playbook_data, "my_playbook")
```

**Parameters:**
- `data` - Dictionary with playbook configuration
- `source` - Source identifier for error reporting

**Returns:**
- `AgentSpec` object or `None` if parsing failed

##### `parse_directory(directory_path: Union[str, Path], pattern: str = "*.yaml") -> List[AgentSpec]`

Parse all playbook files in a directory.

```python
# Parse all YAML files in agents directory
specs = parser.parse_directory("./agents/", "*.yaml")

# Parse all JSON files
specs = parser.parse_directory("./agents/", "*.json")
```

**Parameters:**
- `directory_path` - Directory containing playbook files
- `pattern` - File pattern to match (default: "*.yaml")

**Returns:**
- List of `AgentSpec` objects

##### `get_tier_distribution() -> Dict[str, int]`

Get distribution of agent tiers across parsed specs.

```python
distribution = parser.get_tier_distribution()
# Returns: {"oracles": 5, "genies": 3}
```

##### `find_specs_by_tier(tier: str) -> List[AgentSpec]`

Find all specs of a specific tier.

```python
oracle_specs = parser.find_specs_by_tier("oracles")
genie_specs = parser.find_specs_by_tier("genies")
```

##### `export_to_json(spec: AgentSpec, file_path: Union[str, Path]) -> bool`

Export a parsed spec to JSON format.

```python
success = parser.export_to_json(spec, "exported_playbook.json")
```

### **SuperSpecValidator**

Validates agent playbooks against the SuperSpec DSL specification.

```python
from superoptix.superspec import SuperSpecValidator

validator = SuperSpecValidator()
```

#### **Methods**

##### `validate(playbook_data: Dict[str, Any]) -> Dict[str, Any]`

Validate a playbook against SuperSpec DSL specification.

```python
result = validator.validate(playbook_data)

if result["valid"]:
    print("✅ Playbook is valid")
else:
    print("❌ Validation errors:")
    for error in result["errors"]:
        print(f"  - {error}")
```

**Returns:**
```python
{
    "valid": bool,
    "errors": List[str],
    "warnings": List[str],
    "tier": str
}
```

##### `validate_file(file_path: str) -> Dict[str, Any]`

Validate a playbook file directly.

```python
result = validator.validate_file("my-agent_playbook.yaml")
```

##### `get_validation_summary(results: List[Dict[str, Any]]) -> Dict[str, Any]`

Get summary statistics for multiple validation results.

```python
summary = validator.get_validation_summary(validation_results)
# Returns: {"total": 10, "valid": 8, "invalid": 2, "errors": [...], "warnings": [...]}
```

### **SuperSpecXGenerator**

Generates agent playbook templates based on the SuperSpec DSL specification.

```python
from superoptix.superspec import SuperSpecXGenerator

generator = SuperSpecXGenerator()
```

#### **Methods**

##### `generate_oracles_template(name: str, namespace: str = "software", description: str = None, role: str = "Assistant", task_name: str = "main_task") -> Dict[str, Any]`

Generate an Oracles tier agent template.

```python
template = generator.generate_oracles_template(
    name="Data Analyst",
    namespace="finance",
    description="Financial data analysis agent",
    role="Data Analyst",
    task_name="analyze_data"
)
```

##### `generate_genies_template(name: str, namespace: str = "software", description: str = None, role: str = "Intelligent Assistant", task_name: str = "solve_problem", enable_memory: bool = True, enable_tools: bool = True, enable_rag: bool = False) -> Dict[str, Any]`

Generate a Genies tier agent template.

```python
template = generator.generate_genies_template(
    name="Advanced Assistant",
    namespace="healthcare",
    description="Healthcare assistant with tools and memory",
    role="Healthcare Assistant",
    task_name="patient_analysis",
    enable_memory=True,
    enable_tools=True,
    enable_rag=True
)
```

##### `generate_playbook(tier: str, role: str, namespace: str = "software") -> Dict`

Generate a complete playbook for a specific tier, role, and namespace.

```python
playbook = generator.generate_playbook(
    tier="genies",
    role="Customer Support",
    namespace="retail"
)
```

##### `save_template(template: Dict[str, Any], file_path: str, format: str = "yaml") -> bool`

Save a generated template to file.

```python
success = generator.save_template(
    template,
    "agents/customer-support/playbook/customer-support_playbook.yaml",
    "yaml"
)
```

##### `generate_namespace_templates(namespace: str, output_dir: str = ".", tiers: List[str] = None) -> List[str]`

Generate templates for all tiers in a namespace.

```python
files = generator.generate_namespace_templates(
    namespace="finance",
    output_dir="./generated_agents",
    tiers=["oracles", "genies"]
)
```

##### `validate_template(template: Dict[str, Any]) -> List[str]`

Validate a generated template.

```python
errors = generator.validate_template(template)
if not errors:
    print("✅ Template is valid")
else:
    print("❌ Template errors:", errors)
```

##### `get_template_info(template: Dict[str, Any]) -> Dict[str, Any]`

Get information about a generated template.

```python
info = generator.get_template_info(template)
# Returns: {"name": "...", "tier": "...", "namespace": "...", "features": [...]}
```

### **SuperSpecXSchema**

Defines the schema and validation rules for SuperSpec DSL.

```python
from superoptix.superspec import SuperSpecXSchema

schema = SuperSpecXSchema()
```

#### **Class Attributes**

##### **Valid Enumerations**

```python
# API versions
VALID_API_VERSIONS = ["agent/v1"]

# Object types
VALID_KINDS = ["AgentSpec"]

# Agent tiers
VALID_TIERS = ["oracles", "genies"]

# Development stages
VALID_STAGES = ["alpha", "beta", "stable"]

# Agent types
VALID_AGENT_TYPES = ["Autonomous", "Supervised", "Interactive", "Reactive", "Deliberative", "Hybrid"]

# Namespaces
VALID_NAMESPACES = [
    "software", "education", "healthcare", "finance", "marketing",
    "legal", "consulting", "retail", "manufacturing", "transportation", 
    "agriculture_food", "energy_utilities", "gaming_sports",
    "government_public", "hospitality_tourism", "human_resources",
    "media_entertainment", "real_estate", "testing"
]

# Language model locations
VALID_LM_LOCATIONS = ["local", "self-hosted", "cloud"]

# Language model providers
VALID_LM_PROVIDERS = [
    "ollama", "vllm", "sglang", "mlx", "lm_studio",
    "openai", "anthropic", "google", "azure", "mistral", 
    "cohere", "groq", "deepseek"
]

# Input/Output types
VALID_INPUT_TYPES = ["str", "int", "bool", "float", "list[str]", "dict[str,Any]"]
VALID_OUTPUT_TYPES = ["str", "int", "bool", "float", "list[str]", "dict[str,Any]"]

# Agent flow step types by tier
VALID_AGENTFLOW_TYPES = {
    "oracles": ["Generate", "Think", "Compare", "Route"],
    "genies": ["Generate", "Think", "ActWithTools", "Search", "Compare", "Route"]
}

# Built-in metrics
VALID_BUILTIN_METRICS = [
    "answer_exact_match", "answer_passage_match", "semantic_f1", 
    "rouge_l", "bleu", "meteor", "answer_correctness", 
    "faithfulness", "context_relevance"
]

# Optimization strategies (current version only)
VALID_OPTIMIZATION_STRATEGIES = ["few_shot_bootstrapping"]

# Genies-only features
GENIES_ONLY_FEATURES = [
    "memory", "tool_calling", "retrieval", "streaming", "react_config"
]
```

#### **Class Methods**

##### `get_tier_features(tier: str) -> Dict[str, Any]`

Get allowed features for a specific tier.

```python
oracle_features = SuperSpecXSchema.get_tier_features("oracles")
genie_features = SuperSpecXSchema.get_tier_features("genies")
```

##### `validate_tier_compatibility(tier: str, features: List[str]) -> List[str]`

Validate tier compatibility with features.

```python
issues = SuperSpecXSchema.validate_tier_compatibility("oracles", ["memory", "tools"])
# Returns: ["Feature 'memory' requires Genies tier", "Feature 'tools' requires Genies tier"]
```

##### `get_metadata_schema() -> Dict[str, Any]`

Get the metadata section schema.

```python
metadata_schema = SuperSpecXSchema.get_metadata_schema()
```

##### `get_language_model_schema() -> Dict[str, Any]`

Get the language model configuration schema.

```python
lm_schema = SuperSpecXSchema.get_language_model_schema()
```

##### `get_full_schema(tier: str = "oracles") -> Dict[str, Any]`

Get the complete schema for a specific tier.

```python
oracle_schema = SuperSpecXSchema.get_full_schema("oracles")
genie_schema = SuperSpecXSchema.get_full_schema("genies")
```

## 🎯 **Data Structures**

### **AgentMetadata**

```python
@dataclass
class AgentMetadata:
    name: str                    # Human-readable agent name
    id: str                      # Unique agent identifier
    version: str                 # Agent version (e.g., "1.0.0")
    namespace: Optional[str]     # Logical grouping namespace
    level: str = "oracles"       # Agent tier level
    stage: str = "alpha"         # Development stage
    agent_type: str = "Autonomous"  # Agent operational mode
    description: Optional[str]   # Brief agent description
    tags: Optional[List[str]]    # Categorization tags
    created_at: Optional[str]    # ISO timestamp of creation
    updated_at: Optional[str]    # ISO timestamp of last update
```

### **TaskDefinition**

```python
@dataclass
class TaskDefinition:
    name: str                                    # Unique task name
    instruction: str                             # Core LLM instruction
    description: Optional[str]                   # Task description
    inputs: Optional[List[Dict[str, Any]]]       # Input field definitions
    outputs: Optional[List[Dict[str, Any]]]      # Output field definitions
    schema: Optional[Dict[str, Any]]             # Task schema configuration
    reasoning_steps: Optional[List[str]]         # Reasoning step definitions
    training_examples: Optional[List[Dict[str, Any]]]  # Training examples
    assertions: Optional[List[Dict[str, Any]]]   # Task assertions
```

### **AgentFlowStep**

```python
@dataclass
class AgentFlowStep:
    name: str                        # Step name
    type: str                        # Step type (Generate, Think, etc.)
    task: str                        # Task name to execute
    depends_on: Optional[List[str]]  # Dependencies
    config: Optional[Dict[str, Any]] # Step configuration
    retry_policy: Optional[Dict[str, Any]]  # Retry policy
```

### **AgentSpec**

```python
@dataclass
class AgentSpec:
    api_version: str                           # API version (e.g., "agent/v1")
    kind: str                                  # Object type (e.g., "AgentSpec")
    metadata: AgentMetadata                    # Agent metadata
    language_model: Dict[str, Any]             # Language model configuration
    tasks: List[TaskDefinition]                # Task definitions
    persona: Optional[Dict[str, Any]]          # Agent persona
    agentflow: Optional[List[AgentFlowStep]]   # Execution flow
    retrieval: Optional[Dict[str, Any]]        # RAG configuration (Genies only)
    memory: Optional[Dict[str, Any]]           # Memory configuration (Genies only)
    tool_calling: Optional[Dict[str, Any]]     # Tool configuration (Genies only)
    evaluation: Optional[Dict[str, Any]]       # Evaluation configuration
    optimization: Optional[Dict[str, Any]]     # Optimization configuration
    training: Optional[Dict[str, Any]]         # Training configuration
    runtime: Optional[Dict[str, Any]]          # Runtime configuration
    observability: Optional[Dict[str, Any]]    # Observability configuration
    security: Optional[Dict[str, Any]]         # Security configuration
    feature_specifications: Optional[Dict[str, Any]]  # BDD scenarios
```

## 🚀 **CLI Commands**

### **Generate Playbook**

```bash
# Generate an Oracles tier agent
super spec generate oracles my-agent --namespace software

# Generate a Genies tier agent with all features
super spec generate genies advanced-agent --namespace finance --memory --tools --rag

# Generate with custom role and description
super spec generate genies data-analyst --namespace finance --role "Data Analyst" --description "Financial data analysis specialist"
```

### **Validate Playbook**

```bash
# Validate a single playbook
super spec validate my-agent_playbook.yaml

# Validate multiple playbooks
super spec validate *.yaml --verbose

# Validate with JSON output
super spec validate my-agent_playbook.yaml --format json
```

### **Analyze Playbooks**

```bash
# Analyze all playbooks in a directory
super spec analyze ./agents/

# Analyze with custom pattern
super spec analyze ./agents/ --pattern "*.yaml"

# Analyze with JSON output
super spec analyze ./agents/ --format json
```

### **Show Playbook Info**

```bash
# Show detailed information about a playbook
super spec info my-agent_playbook.yaml
```

### **Explore Schema**

```bash
# Show schema for all tiers
super spec schema

# Show schema for specific tier
super spec schema --tier genies
```

### **Bootstrap Namespace**

```bash
# Generate agents for all tiers in a namespace
super spec bootstrap --namespace finance --output-dir ./generated_agents

# Generate only specific tiers
super spec bootstrap --namespace healthcare --tiers oracles genies
```

## 🎯 **Validation Rules**

### **Required Fields**

- `apiVersion` - Must be "agent/v1"
- `kind` - Must be "AgentSpec"
- `metadata.name` - Human-readable agent name
- `metadata.id` - Unique identifier (a-z, 0-9, -, _)
- `metadata.version` - Semantic versioning (e.g., "1.0.0")
- `spec.language_model` - Language model configuration
- `spec.tasks` - At least one task definition

### **Tier-Specific Constraints**

#### **Oracles Tier**
- **Allowed AgentFlow Types**: `Generate`, `Think`, `Compare`, `Route`
- **Forbidden Features**: `memory`, `tool_calling`, `retrieval`, `streaming`, `react_config`
- **Default Model**: `llama3.2:1b` (Ollama)

#### **Genies Tier**
- **Allowed AgentFlow Types**: `Generate`, `Think`, `ActWithTools`, `Search`, `Compare`, `Route`
- **Allowed Features**: `memory`, `tool_calling`, `retrieval`, `streaming`, `react_config`
- **Default Model**: `llama3.2:3b` (Ollama)

### **Validation Examples**

```python
from superoptix.superspec import SuperSpecValidator

validator = SuperSpecValidator()

# Validate a playbook
result = validator.validate(playbook_data)

if result["valid"]:
    print(f"✅ Valid {result['tier']} tier playbook")
else:
    print("❌ Validation errors:")
    for error in result["errors"]:
        print(f"  - {error}")
    
    print("⚠️  Warnings:")
    for warning in result["warnings"]:
        print(f"  - {warning}")
```

## 🎉 **Best Practices**

### **1. Use Proper Namespacing**

```yaml
metadata:
  namespace: "finance"  # Use standard namespaces
  tags: ["finance", "data-analysis", "oracles"]
```

### **2. Follow Tier Constraints**

```yaml
# ✅ Correct - Oracles tier without advanced features
metadata:
  level: "oracles"
spec:
  # No memory, tools, or RAG configuration
  tasks: [...]

# ✅ Correct - Genies tier with advanced features
metadata:
  level: "genies"
spec:
  memory:
    enabled: true
  tool_calling:
    enabled: true
  retrieval:
    enabled: true
```

### **3. Validate Early and Often**

```bash
# Validate during development
super spec validate my-agent_playbook.yaml

# Validate before committing
super spec validate *.yaml --verbose
```

### **4. Use Descriptive Names**

```yaml
metadata:
  name: "Financial Data Analyst"  # Clear, descriptive name
  id: "financial-data-analyst"    # URL-friendly identifier
  description: "Specialized agent for financial data analysis and reporting"
```

---

💡 **Pro Tip**: Use the `super spec schema --tier genies` command to explore all available features and constraints for each tier! 