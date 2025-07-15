# 📊 Observability API

The observability system provides comprehensive monitoring, tracing, and debugging capabilities for SuperOptiX agents and pipelines.

## SuperOptixTracer

The main tracing component that tracks agent execution and performance.

### Constructor

```python
class SuperOptixTracer:
    def __init__(
        self,
        agent_id: str,
        enable_external_tracing: bool = False,
        traces_dir: str = "traces"
    )
```

**Parameters:**
- `agent_id` (str): Unique identifier for the agent
- `enable_external_tracing` (bool): Enable external tracing systems - defaults to False
- `traces_dir` (str): Directory for storing traces - defaults to "traces"

### Core Methods

#### trace_operation()
```python
def trace_operation(self, operation_name: str, category: str) -> TraceContext:
    """Start tracing an operation."""
```

**Parameters:**
- `operation_name` (str): Name of the operation
- `category` (str): Operation category

**Returns:** TraceContext for managing the trace

#### add_event()
```python
def add_event(
    self,
    event_type: str,
    data: Dict[str, Any],
    timestamp: Optional[datetime] = None
) -> str:
    """Add an event to the current trace."""
```

**Parameters:**
- `event_type` (str): Type of event
- `data` (Dict[str, Any]): Event data
- `timestamp` (datetime, optional): Event timestamp

**Returns:** Event identifier

#### add_metric()
```python
def add_metric(
    self,
    metric_name: str,
    value: float,
    unit: str = "count",
    tags: Optional[Dict[str, str]] = None
) -> None:
    """Add a metric to the current trace."""
```

**Parameters:**
- `metric_name` (str): Name of the metric
- `value` (float): Metric value
- `unit` (str): Metric unit - defaults to "count"
- `tags` (Dict[str, str], optional): Metric tags

#### save_trace()
```python
def save_trace(self, trace_id: Optional[str] = None) -> str:
    """Save the current trace to storage."""
```

**Parameters:**
- `trace_id` (str, optional): Custom trace identifier

**Returns:** Trace identifier

#### get_trace()
```python
def get_trace(self, trace_id: str) -> Optional[Dict[str, Any]]:
    """Retrieve a saved trace."""
```

**Parameters:**
- `trace_id` (str): Trace identifier

**Returns:** Trace data or None if not found

#### list_traces()
```python
def list_traces(
    self,
    agent_id: Optional[str] = None,
    start_time: Optional[datetime] = None,
    end_time: Optional[datetime] = None,
    limit: int = 100
) -> List[Dict[str, Any]]:
    """List available traces with optional filtering."""
```

**Parameters:**
- `agent_id` (str, optional): Filter by agent ID
- `start_time` (datetime, optional): Filter by start time
- `end_time` (datetime, optional): Filter by end time
- `limit` (int): Maximum results - defaults to 100

**Returns:** List of trace summaries

## TraceEvent

Represents a single event in a trace.

```python
@dataclass
class TraceEvent:
    event_id: str
    event_type: str
    timestamp: datetime
    data: Dict[str, Any]
    trace_id: str
    operation_name: Optional[str] = None
    category: Optional[str] = None
```

## TraceContext

Context manager for tracing operations.

```python
class TraceContext:
    def __init__(self, tracer: SuperOptixTracer, operation_name: str, category: str)
    
    def __enter__(self) -> 'TraceContext'
    def __exit__(self, exc_type, exc_val, exc_tb) -> None
    
    def add_event(self, event_type: str, data: Dict[str, Any]) -> str
    def add_metric(self, metric_name: str, value: float, unit: str = "count") -> None
    def set_status(self, status: str) -> None
    def set_error(self, error: Exception) -> None
```

## SuperOptixCallback

DSPy callback for integrating with the tracing system.

### Constructor

```python
class SuperOptixCallback:
    def __init__(self, tracer: SuperOptixTracer)
```

**Parameters:**
- `tracer` (SuperOptixTracer): Tracer instance

### Core Methods

#### on_chain_start()
```python
def on_chain_start(self, serialized: Dict[str, Any], inputs: Dict[str, Any], **kwargs) -> None:
    """Called when a DSPy chain starts."""
```

#### on_chain_end()
```python
def on_chain_end(self, outputs: Dict[str, Any], **kwargs) -> None:
    """Called when a DSPy chain ends."""
```

#### on_chain_error()
```python
def on_chain_error(self, error: Exception, **kwargs) -> None:
    """Called when a DSPy chain encounters an error."""
```

#### on_llm_start()
```python
def on_llm_start(self, serialized: Dict[str, Any], prompts: List[str], **kwargs) -> None:
    """Called when an LLM call starts."""
```

#### on_llm_end()
```python
def on_llm_end(self, response: Any, **kwargs) -> None:
    """Called when an LLM call ends."""
```

#### on_llm_error()
```python
def on_llm_error(self, error: Exception, **kwargs) -> None:
    """Called when an LLM call encounters an error."""
```

## InteractiveDebugger

Interactive debugging interface for agents.

### Constructor

```python
class InteractiveDebugger:
    def __init__(
        self,
        agent: SuperOptixPipeline,
        debug_mode: str = "interactive",
        breakpoints: Optional[List[str]] = None
    )
```

**Parameters:**
- `agent` (SuperOptixPipeline): Agent to debug
- `debug_mode` (str): Debug mode ("interactive", "step", "auto") - defaults to "interactive"
- `breakpoints` (List[str], optional): List of breakpoint conditions

### Core Methods

#### debug_run()
```python
def debug_run(self, query: str, **kwargs) -> Dict[str, Any]:
    """Run the agent in debug mode."""
```

**Parameters:**
- `query` (str): Input query
- `**kwargs` (Any): Additional parameters

**Returns:** Debug execution results

#### set_breakpoint()
```python
def set_breakpoint(self, condition: str) -> None:
    """Set a breakpoint condition."""
```

**Parameters:**
- `condition` (str): Breakpoint condition

#### clear_breakpoints()
```python
def clear_breakpoints(self) -> None:
    """Clear all breakpoints."""
```

#### step_through()
```python
def step_through(self, query: str) -> Generator[Dict[str, Any], None, None]:
    """Step through agent execution."""
```

**Parameters:**
- `query` (str): Input query

**Returns:** Generator yielding execution steps

#### inspect_state()
```python
def inspect_state(self) -> Dict[str, Any]:
    """Inspect current agent state."""
```

**Returns:** Current state information

#### modify_state()
```python
def modify_state(self, key: str, value: Any) -> None:
    """Modify agent state during debugging."""
```

**Parameters:**
- `key` (str): State key to modify
- `value` (Any): New value

## ObservabilityDashboard

Web-based dashboard for monitoring agent performance.

### Constructor

```python
class ObservabilityDashboard:
    def __init__(
        self,
        traces_dir: str = "traces",
        port: int = 8080,
        host: str = "localhost"
    )
```

**Parameters:**
- `traces_dir` (str): Directory containing traces - defaults to "traces"
- `port` (int): Dashboard port - defaults to 8080
- `host` (str): Dashboard host - defaults to "localhost"

### Core Methods

#### start()
```python
def start(self) -> None:
    """Start the dashboard server."""
```

#### stop()
```python
def stop(self) -> None:
    """Stop the dashboard server."""
```

#### get_dashboard_url(self) -> str:
    """Get the dashboard URL."""
```

**Returns:** Dashboard URL

#### add_custom_metric()
```python
def add_custom_metric(
    self,
    metric_name: str,
    value: float,
    agent_id: str,
    timestamp: Optional[datetime] = None
) -> None:
    """Add a custom metric to the dashboard."""
```

**Parameters:**
- `metric_name` (str): Metric name
- `value` (float): Metric value
- `agent_id` (str): Agent identifier
- `timestamp` (datetime, optional): Metric timestamp

#### get_metrics()
```python
def get_metrics(
    self,
    agent_id: Optional[str] = None,
    metric_name: Optional[str] = None,
    start_time: Optional[datetime] = None,
    end_time: Optional[datetime] = None
) -> List[Dict[str, Any]]:
    """Get metrics with optional filtering."""
```

**Parameters:**
- `agent_id` (str, optional): Filter by agent ID
- `metric_name` (str, optional): Filter by metric name
- `start_time` (datetime, optional): Filter by start time
- `end_time` (datetime, optional): Filter by end time

**Returns:** List of metrics

## MultiAgentObservabilityDashboard

Dashboard for monitoring multiple agents.

### Constructor

```python
class MultiAgentObservabilityDashboard:
    def __init__(
        self,
        agents: List[SuperOptixPipeline],
        traces_dir: str = "traces",
        port: int = 8080,
        host: str = "localhost"
    )
```

**Parameters:**
- `agents` (List[SuperOptixPipeline]): List of agents to monitor
- `traces_dir` (str): Directory containing traces - defaults to "traces"
- `port` (int): Dashboard port - defaults to 8080
- `host` (str): Dashboard host - defaults to "localhost"

### Core Methods

#### start()
```python
def start(self) -> None:
    """Start the multi-agent dashboard."""
```

#### stop()
```python
def stop(self) -> None:
    """Stop the multi-agent dashboard."""
```

#### add_agent()
```python
def add_agent(self, agent: SuperOptixPipeline) -> None:
    """Add an agent to the dashboard."""
```

**Parameters:**
- `agent` (SuperOptixPipeline): Agent to add

#### remove_agent()
```python
def remove_agent(self, agent_id: str) -> None:
    """Remove an agent from the dashboard."""
```

**Parameters:**
- `agent_id` (str): Agent identifier

#### get_agent_comparison()
```python
def get_agent_comparison(
    self,
    metric_name: str,
    start_time: Optional[datetime] = None,
    end_time: Optional[datetime] = None
) -> Dict[str, List[float]]:
    """Compare agents by metric."""
```

**Parameters:**
- `metric_name` (str): Metric to compare
- `start_time` (datetime, optional): Start time filter
- `end_time` (datetime, optional): End time filter

**Returns:** Dictionary mapping agent IDs to metric values

## ObservabilityEnhancedDSPyAdapter

Enhanced DSPy adapter with observability features.

### Constructor

```python
class ObservabilityEnhancedDSPyAdapter:
    def __init__(
        self,
        base_adapter: Any,
        tracer: SuperOptixTracer,
        enable_metrics: bool = True,
        enable_tracing: bool = True
    )
```

**Parameters:**
- `base_adapter` (Any): Base DSPy adapter
- `tracer` (SuperOptixTracer): Tracer instance
- `enable_metrics` (bool): Enable metrics collection - defaults to True
- `enable_tracing` (bool): Enable tracing - defaults to True

### Core Methods

#### forward()
```python
def forward(self, *args, **kwargs) -> Any:
    """Enhanced forward pass with observability."""
```

**Parameters:** `*args, **kwargs` - Forward pass arguments
**Returns:** Forward pass result

#### get_metrics()
```python
def get_metrics(self) -> Dict[str, Any]:
    """Get collected metrics."""
```

**Returns:** Dictionary of metrics

#### reset_metrics()
```python
def reset_metrics(self) -> None:
    """Reset collected metrics."""
```

## Example Usage

```python
from superoptix.observability import (
    SuperOptixTracer,
    SuperOptixCallback,
    InteractiveDebugger,
    ObservabilityDashboard,
    ObservabilityEnhancedDSPyAdapter
)

# Initialize tracer
tracer = SuperOptixTracer(
    agent_id="my_agent",
    enable_external_tracing=True,
    traces_dir="traces"
)

# Use tracer in agent pipeline
class MyAgent(SuperOptixPipeline):
    def __init__(self, config=None):
        super().__init__(config)
        self.tracer = tracer
    
    def forward(self, query: str) -> dspy.Prediction:
        with self.tracer.trace_operation("agent_forward", "pipeline"):
            # Add custom events
            self.tracer.add_event("query_received", {"query": query})
            
            # Your agent logic here
            result = self.lm(f"Process: {query}")
            
            # Add metrics
            self.tracer.add_metric("response_length", len(result))
            self.tracer.add_metric("processing_time", 0.5)
            
            return dspy.Prediction(answer=result)

# Use DSPy callback
callback = SuperOptixCallback(tracer)

# Initialize agent
agent = MyAgent()

# Use callback with DSPy
import dspy
dspy.settings.configure(lm=agent.lm, trace=[callback])

# Interactive debugging
debugger = InteractiveDebugger(agent, debug_mode="interactive")
debugger.set_breakpoint("query contains 'debug'")

# Debug a query
debug_result = debugger.debug_run("This is a debug query")

# Step through execution
for step in debugger.step_through("Step through this query"):
    print(f"Step: {step['operation']}")
    print(f"Data: {step['data']}")

# Inspect state
state = debugger.inspect_state()
print(f"Current state: {state}")

# Modify state during debugging
debugger.modify_state("custom_variable", "new_value")

# Dashboard
dashboard = ObservabilityDashboard(
    traces_dir="traces",
    port=8080
)

# Start dashboard
dashboard.start()
print(f"Dashboard available at: {dashboard.get_dashboard_url()}")

# Add custom metrics
dashboard.add_custom_metric(
    metric_name="user_satisfaction",
    value=4.5,
    agent_id="my_agent"
)

# Get metrics
metrics = dashboard.get_metrics(
    agent_id="my_agent",
    start_time=datetime.now() - timedelta(hours=1)
)

# Multi-agent dashboard
agents = [agent1, agent2, agent3]
multi_dashboard = MultiAgentObservabilityDashboard(agents)

# Start multi-agent dashboard
multi_dashboard.start()

# Compare agents
comparison = multi_dashboard.get_agent_comparison(
    metric_name="response_time",
    start_time=datetime.now() - timedelta(hours=1)
)

# Enhanced DSPy adapter
enhanced_adapter = ObservabilityEnhancedDSPyAdapter(
    base_adapter=original_adapter,
    tracer=tracer,
    enable_metrics=True,
    enable_tracing=True
)

# Use enhanced adapter
result = enhanced_adapter.forward(input_data)

# Get metrics from adapter
adapter_metrics = enhanced_adapter.get_metrics()
print(f"Adapter metrics: {adapter_metrics}")

# Save trace
trace_id = tracer.save_trace()
print(f"Saved trace: {trace_id}")

# Retrieve trace
trace_data = tracer.get_trace(trace_id)
print(f"Trace events: {len(trace_data['events'])}")

# List traces
traces = tracer.list_traces(
    agent_id="my_agent",
    start_time=datetime.now() - timedelta(days=1),
    limit=10
)

for trace in traces:
    print(f"Trace {trace['trace_id']}: {trace['operation_name']}")

# Stop dashboard
dashboard.stop()
multi_dashboard.stop()
```

## Configuration Options

### Tracer Configuration

```python
tracer_config = {
    "enable_external_tracing": True,
    "traces_dir": "traces",
    "max_traces": 1000,
    "retention_days": 30,
    "compression": True
}
```

### Dashboard Configuration

```python
dashboard_config = {
    "port": 8080,
    "host": "localhost",
    "auto_refresh": True,
    "refresh_interval": 30,
    "theme": "dark",
    "enable_websockets": True
}
```

### Debugger Configuration

```python
debugger_config = {
    "debug_mode": "interactive",  # interactive, step, auto
    "breakpoints": ["error", "slow_operation"],
    "step_delay": 1.0,
    "show_internals": True
}
```

## Metrics and Events

### Built-in Metrics

- `response_time`: Time to generate response
- `token_count`: Number of tokens processed
- `memory_usage`: Memory consumption
- `tool_calls`: Number of tool invocations
- `error_rate`: Error frequency
- `user_satisfaction`: User feedback scores

### Built-in Events

- `agent_start`: Agent initialization
- `query_received`: Query processing start
- `tool_called`: Tool invocation
- `response_generated`: Response completion
- `error_occurred`: Error handling
- `memory_accessed`: Memory operations
- `optimization_step`: Optimization progress

### Custom Metrics and Events

```python
# Add custom metric
tracer.add_metric(
    metric_name="custom_business_metric",
    value=42.0,
    unit="score",
    tags={"category": "business", "priority": "high"}
)

# Add custom event
tracer.add_event(
    event_type="business_decision",
    data={
        "decision": "approve_loan",
        "amount": 50000,
        "risk_score": 0.3,
        "reasoning": "Good credit history"
    }
)
``` 