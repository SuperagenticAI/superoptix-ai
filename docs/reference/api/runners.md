# 🏃 Runners API

The runners system provides execution engines for SuperOptiX agents and orchestras, handling DSPy pipeline execution and multi-agent coordination.

## DSPyRunner

Executes DSPy-based SuperOptiX agents with comprehensive monitoring and optimization.

### Constructor

```python
class DSPyRunner:
    def __init__(
        self,
        agent: SuperOptixPipeline,
        config: Optional[Dict[str, Any]] = None
    )
```

**Parameters:**
- `agent` (SuperOptixPipeline): Agent to run
- `config` (Dict[str, Any], optional): Runner configuration

### Core Methods

#### run()
```python
def run(
    self,
    query: str,
    **kwargs
) -> Dict[str, Any]:
    """Run the agent with a query."""
```

**Parameters:**
- `query` (str): Input query
- `**kwargs` (Any): Additional parameters

**Returns:** Execution results dictionary

#### run_batch()
```python
def run_batch(
    self,
    queries: List[str],
    max_concurrent: int = 1,
    **kwargs
) -> List[Dict[str, Any]]:
    """Run multiple queries in batch."""
```

**Parameters:**
- `queries` (List[str]): List of input queries
- `max_concurrent` (int): Maximum concurrent executions - defaults to 1
- `**kwargs` (Any): Additional parameters

**Returns:** List of execution results

#### run_with_tools()
```python
def run_with_tools(
    self,
    query: str,
    tools: List[BaseTool],
    max_tool_calls: int = 5,
    **kwargs
) -> Dict[str, Any]:
    """Run agent with specific tools."""
```

**Parameters:**
- `query` (str): Input query
- `tools` (List[BaseTool]): Tools to use
- `max_tool_calls` (int): Maximum tool calls - defaults to 5
- `**kwargs` (Any): Additional parameters

**Returns:** Execution results with tool usage

#### run_with_memory()
```python
def run_with_memory(
    self,
    query: str,
    memory: AgentMemory,
    include_context: bool = True,
    **kwargs
) -> Dict[str, Any]:
    """Run agent with memory integration."""
```

**Parameters:**
- `query` (str): Input query
- `memory` (AgentMemory): Memory system to use
- `include_context` (bool): Include memory context - defaults to True
- `**kwargs` (Any): Additional parameters

**Returns:** Execution results with memory context

#### optimize()
```python
def optimize(
    self,
    training_data: List[Dict[str, Any]],
    optimization_strategy: str = "BootstrapFewShot",
    **kwargs
) -> Dict[str, Any]:
    """Optimize the agent with training data."""
```

**Parameters:**
- `training_data` (List[Dict[str, Any]]): Training examples
- `optimization_strategy` (str): Optimization strategy - defaults to "BootstrapFewShot"
- `**kwargs` (Any): Optimization parameters

**Returns:** Optimization results

#### evaluate()
```python
def evaluate(
    self,
    test_data: List[Dict[str, Any]],
    metrics: Optional[List[str]] = None,
    **kwargs
) -> Dict[str, Any]:
    """Evaluate the agent with test data."""
```

**Parameters:**
- `test_data` (List[Dict[str, Any]]): Test examples
- `metrics` (List[str], optional): Metrics to compute
- `**kwargs` (Any): Evaluation parameters

**Returns:** Evaluation results

#### get_execution_stats()
```python
def get_execution_stats(self) -> Dict[str, Any]:
    """Get execution statistics."""
```

**Returns:** Execution statistics dictionary

#### reset_stats()
```python
def reset_stats(self) -> None:
    """Reset execution statistics."""
```

## OrchestraRunner

Executes multi-agent orchestras with coordination and workflow management.

### Constructor

```python
class OrchestraRunner:
    def __init__(
        self,
        orchestra_config: Dict[str, Any],
        agents: Dict[str, SuperOptixPipeline],
        config: Optional[Dict[str, Any]] = None
    )
```

**Parameters:**
- `orchestra_config` (Dict[str, Any]): Orchestra configuration
- `agents` (Dict[str, SuperOptixPipeline]): Dictionary of agents
- `config` (Dict[str, Any], optional): Runner configuration

### Core Methods

#### run_orchestra()
```python
def run_orchestra(
    self,
    input_data: Dict[str, Any],
    workflow_type: str = "pipeline",
    **kwargs
) -> Dict[str, Any]:
    """Run the complete orchestra workflow."""
```

**Parameters:**
- `input_data` (Dict[str, Any]): Input data for the orchestra
- `workflow_type` (str): Workflow type ("pipeline", "broadcast", "conditional") - defaults to "pipeline"
- `**kwargs` (Any): Additional parameters

**Returns:** Orchestra execution results

#### run_pipeline_workflow()
```python
def run_pipeline_workflow(
    self,
    input_data: Dict[str, Any],
    pipeline_steps: List[str],
    **kwargs
) -> Dict[str, Any]:
    """Run a pipeline workflow."""
```

**Parameters:**
- `input_data` (Dict[str, Any]): Input data
- `pipeline_steps` (List[str]): Ordered list of agent steps
- `**kwargs` (Any): Additional parameters

**Returns:** Pipeline execution results

#### run_broadcast_workflow()
```python
def run_broadcast_workflow(
    self,
    input_data: Dict[str, Any],
    target_agents: List[str],
    aggregation_strategy: str = "consensus",
    **kwargs
) -> Dict[str, Any]:
    """Run a broadcast workflow."""
```

**Parameters:**
- `input_data` (Dict[str, Any]): Input data
- `target_agents` (List[str]): Target agents for broadcast
- `aggregation_strategy` (str): Result aggregation strategy - defaults to "consensus"
- `**kwargs` (Any): Additional parameters

**Returns:** Broadcast execution results

#### run_conditional_workflow()
```python
def run_conditional_workflow(
    self,
    input_data: Dict[str, Any],
    conditions: List[Dict[str, Any]],
    **kwargs
) -> Dict[str, Any]:
    """Run a conditional workflow."""
```

**Parameters:**
- `input_data` (Dict[str, Any]): Input data
- `conditions` (List[Dict[str, Any]]): Conditional workflow rules
- `**kwargs` (Any): Additional parameters

**Returns:** Conditional execution results

#### run_parallel_workflow()
```python
def run_parallel_workflow(
    self,
    input_data: Dict[str, Any],
    parallel_tasks: List[Dict[str, Any]],
    max_concurrent: int = 4,
    **kwargs
) -> Dict[str, Any]:
    """Run a parallel workflow."""
```

**Parameters:**
- `input_data` (Dict[str, Any]): Input data
- `parallel_tasks` (List[Dict[str, Any]]): Parallel task definitions
- `max_concurrent` (int): Maximum concurrent executions - defaults to 4
- `**kwargs` (Any): Additional parameters

**Returns:** Parallel execution results

#### add_agent()
```python
def add_agent(
    self,
    agent_id: str,
    agent: SuperOptixPipeline
) -> None:
    """Add an agent to the orchestra."""
```

**Parameters:**
- `agent_id` (str): Agent identifier
- `agent` (SuperOptixPipeline): Agent instance

#### remove_agent()
```python
def remove_agent(self, agent_id: str) -> None:
    """Remove an agent from the orchestra."""
```

**Parameters:**
- `agent_id` (str): Agent identifier

#### get_agent_status()
```python
def get_agent_status(self, agent_id: str) -> Dict[str, Any]:
    """Get status of a specific agent."""
```

**Parameters:**
- `agent_id` (str): Agent identifier

**Returns:** Agent status information

#### get_orchestra_status()
```python
def get_orchestra_status(self) -> Dict[str, Any]:
    """Get overall orchestra status."""
```

**Returns:** Orchestra status information

#### pause_orchestra()
```python
def pause_orchestra(self) -> None:
    """Pause orchestra execution."""
```

#### resume_orchestra()
```python
def resume_orchestra(self) -> None:
    """Resume orchestra execution."""
```

#### stop_orchestra()
```python
def stop_orchestra(self) -> None:
    """Stop orchestra execution."""
```

## Workflow Types

### Pipeline Workflow

Sequential execution of agents where output of one becomes input to the next.

```yaml
workflow_type: "pipeline"
pipeline_steps:
  - "data_processor"
  - "analyzer"
  - "reporter"
```

### Broadcast Workflow

Send the same input to multiple agents and aggregate results.

```yaml
workflow_type: "broadcast"
target_agents:
  - "validator_1"
  - "validator_2"
  - "validator_3"
aggregation_strategy: "consensus"
```

### Conditional Workflow

Execute different agents based on conditions.

```yaml
workflow_type: "conditional"
conditions:
  - condition: "input.type == 'text'"
    agent: "text_processor"
  - condition: "input.type == 'image'"
    agent: "image_processor"
  - condition: "input.type == 'data'"
    agent: "data_processor"
```

### Parallel Workflow

Execute multiple agents simultaneously.

```yaml
workflow_type: "parallel"
parallel_tasks:
  - agent: "data_processor"
    input_key: "raw_data"
  - agent: "metadata_extractor"
    input_key: "raw_data"
  - agent: "quality_checker"
    input_key: "raw_data"
max_concurrent: 3
```

## Example Usage

```python
from superoptix.runners import DSPyRunner, OrchestraRunner
from superoptix.core import SuperOptixPipeline
from superoptix.memory import AgentMemory

# Create agents
class DataProcessor(SuperOptixPipeline):
    def get_signature(self):
        return dspy.Signature(
            "Process raw data into structured format",
            raw_data=dspy.InputField(desc="Raw input data"),
            processed_data=dspy.OutputField(desc="Processed structured data")
        )
    
    def forward(self, raw_data: str) -> dspy.Prediction:
        # Processing logic
        processed = f"Processed: {raw_data}"
        return dspy.Prediction(processed_data=processed)
    
    def get_agent_name(self) -> str:
        return "data_processor"

class Analyzer(SuperOptixPipeline):
    def get_signature(self):
        return dspy.Signature(
            "Analyze processed data",
            processed_data=dspy.InputField(desc="Processed data"),
            analysis=dspy.OutputField(desc="Analysis results")
        )
    
    def forward(self, processed_data: str) -> dspy.Prediction:
        # Analysis logic
        analysis = f"Analysis of: {processed_data}"
        return dspy.Prediction(analysis=analysis)
    
    def get_agent_name(self) -> str:
        return "analyzer"

class Reporter(SuperOptixPipeline):
    def get_signature(self):
        return dspy.Signature(
            "Generate report from analysis",
            analysis=dspy.InputField(desc="Analysis results"),
            report=dspy.OutputField(desc="Final report")
        )
    
    def forward(self, analysis: str) -> dspy.Prediction:
        # Report generation logic
        report = f"Report: {analysis}"
        return dspy.Prediction(report=report)
    
    def get_agent_name(self) -> str:
        return "reporter"

# Initialize agents
data_processor = DataProcessor()
analyzer = Analyzer()
reporter = Reporter()

# DSPy Runner usage
runner = DSPyRunner(data_processor)

# Run single query
result = runner.run("Sample raw data")
print(f"Result: {result}")

# Run batch
batch_results = runner.run_batch([
    "Data 1",
    "Data 2",
    "Data 3"
], max_concurrent=2)

# Run with tools
from superoptix.tools import CalculatorTool
tools = [CalculatorTool()]
tool_result = runner.run_with_tools(
    "Calculate 2 + 2",
    tools=tools
)

# Run with memory
memory = AgentMemory(agent_id="data_processor")
memory_result = runner.run_with_memory(
    "Remember this data",
    memory=memory
)

# Optimize agent
training_data = [
    {"raw_data": "input1", "processed_data": "output1"},
    {"raw_data": "input2", "processed_data": "output2"}
]
optimization_result = runner.optimize(
    training_data,
    optimization_strategy="BootstrapFewShot"
)

# Evaluate agent
test_data = [
    {"raw_data": "test1", "processed_data": "expected1"},
    {"raw_data": "test2", "processed_data": "expected2"}
]
evaluation_result = runner.evaluate(test_data)

# Get execution stats
stats = runner.get_execution_stats()
print(f"Total runs: {stats['total_runs']}")
print(f"Average response time: {stats['avg_response_time']}")

# Orchestra Runner usage
agents = {
    "data_processor": data_processor,
    "analyzer": analyzer,
    "reporter": reporter
}

orchestra_config = {
    "name": "data_analysis_orchestra",
    "description": "Complete data analysis pipeline",
    "workflow_type": "pipeline",
    "pipeline_steps": ["data_processor", "analyzer", "reporter"]
}

orchestra_runner = OrchestraRunner(orchestra_config, agents)

# Run pipeline workflow
pipeline_result = orchestra_runner.run_pipeline_workflow(
    input_data={"raw_data": "Sample data for analysis"},
    pipeline_steps=["data_processor", "analyzer", "reporter"]
)

# Run broadcast workflow
broadcast_result = orchestra_runner.run_broadcast_workflow(
    input_data={"data": "Data to validate"},
    target_agents=["validator_1", "validator_2", "validator_3"],
    aggregation_strategy="consensus"
)

# Run conditional workflow
conditional_result = orchestra_runner.run_conditional_workflow(
    input_data={"type": "text", "content": "Sample text"},
    conditions=[
        {"condition": "input.type == 'text'", "agent": "text_processor"},
        {"condition": "input.type == 'image'", "agent": "image_processor"},
        {"condition": "input.type == 'data'", "agent": "data_processor"}
    ]
)

# Run parallel workflow
parallel_result = orchestra_runner.run_parallel_workflow(
    input_data={"raw_data": "Data for parallel processing"},
    parallel_tasks=[
        {"agent": "data_processor", "input_key": "raw_data"},
        {"agent": "metadata_extractor", "input_key": "raw_data"},
        {"agent": "quality_checker", "input_key": "raw_data"}
    ],
    max_concurrent=3
)

# Get orchestra status
status = orchestra_runner.get_orchestra_status()
print(f"Orchestra status: {status['status']}")
print(f"Active agents: {status['active_agents']}")

# Get specific agent status
agent_status = orchestra_runner.get_agent_status("data_processor")
print(f"Data processor status: {agent_status}")

# Add new agent
class NewAgent(SuperOptixPipeline):
    def get_signature(self):
        return dspy.Signature(
            "New agent signature",
            input=dspy.InputField(desc="Input"),
            output=dspy.OutputField(desc="Output")
        )
    
    def forward(self, input: str) -> dspy.Prediction:
        return dspy.Prediction(output=f"Processed: {input}")
    
    def get_agent_name(self) -> str:
        return "new_agent"

new_agent = NewAgent()
orchestra_runner.add_agent("new_agent", new_agent)

# Remove agent
orchestra_runner.remove_agent("new_agent")

# Control orchestra
orchestra_runner.pause_orchestra()
orchestra_runner.resume_orchestra()
orchestra_runner.stop_orchestra()
```

## Configuration Options

### DSPyRunner Configuration

```python
dspy_runner_config = {
    "enable_tracing": True,
    "enable_metrics": True,
    "max_retries": 3,
    "timeout": 30,
    "optimization_enabled": True,
    "evaluation_enabled": True
}
```

### OrchestraRunner Configuration

```python
orchestra_runner_config = {
    "max_concurrent_agents": 4,
    "workflow_timeout": 300,
    "enable_monitoring": True,
    "retry_failed_steps": True,
    "max_retries": 3,
    "aggregation_timeout": 60
}
```

### Workflow Configuration

```python
pipeline_config = {
    "error_handling": "continue",  # continue, stop, retry
    "data_passing": "explicit",    # explicit, automatic
    "validation": True,
    "logging": True
}

broadcast_config = {
    "aggregation_strategy": "consensus",  # consensus, majority, weighted
    "timeout": 60,
    "min_responses": 2
}

conditional_config = {
    "default_agent": "fallback_agent",
    "condition_evaluation": "strict",  # strict, fuzzy
    "fallback_strategy": "use_default"
}

parallel_config = {
    "max_concurrent": 4,
    "resource_limits": {"cpu": 0.5, "memory": "1GB"},
    "synchronization": "barrier"  # barrier, async
}
``` 