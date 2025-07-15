# 🛠️ Tools Framework API

The tools framework provides a modular system for creating and managing tools that SuperOptiX agents can use. Tools are organized by industry categories and can be easily created using factory patterns.

## BaseTool

The base class for all tools in SuperOptiX.

### Constructor

```python
class BaseTool:
    def __init__(
        self,
        name: str,
        description: str,
        category: str = "general",
        version: str = "1.0.0",
        **kwargs
    )
```

**Parameters:**
- `name` (str): Tool name
- `description` (str): Tool description
- `category` (str): Tool category - defaults to "general"
- `version` (str): Tool version - defaults to "1.0.0"
- `**kwargs` (Any): Additional tool configuration

### Core Methods

#### execute()
```python
def execute(self, **kwargs) -> Dict[str, Any]:
    """Execute the tool with given parameters."""
```

**Parameters:** `**kwargs` - Tool-specific parameters
**Returns:** Dictionary with execution results

#### validate_input()
```python
def validate_input(self, **kwargs) -> bool:
    """Validate input parameters."""
```

**Parameters:** `**kwargs` - Input parameters to validate
**Returns:** True if valid, False otherwise

#### get_schema()
```python
def get_schema(self) -> Dict[str, Any]:
    """Get tool schema for parameter validation."""
```

**Returns:** Dictionary describing tool parameters and types

## Tool Categories

### Core Tools

Essential tools for basic agent functionality.

#### WebSearchTool
```python
class WebSearchTool(BaseTool):
    def __init__(self, api_key: Optional[str] = None, search_engine: str = "google")
    
    def execute(self, query: str, max_results: int = 5) -> Dict[str, Any]
```

**Parameters:**
- `query` (str): Search query
- `max_results` (int): Maximum results to return - defaults to 5

#### CalculatorTool
```python
class CalculatorTool(BaseTool):
    def execute(self, expression: str) -> Dict[str, Any]
```

**Parameters:**
- `expression` (str): Mathematical expression to evaluate

#### FileReaderTool
```python
class FileReaderTool(BaseTool):
    def execute(self, file_path: str, encoding: str = "utf-8") -> Dict[str, Any]
```

**Parameters:**
- `file_path` (str): Path to file to read
- `encoding` (str): File encoding - defaults to "utf-8"

#### DateTimeTool
```python
class DateTimeTool(BaseTool):
    def execute(self, operation: str, **kwargs) -> Dict[str, Any]
```

**Parameters:**
- `operation` (str): Operation type ("current", "parse", "format", "calculate")
- `**kwargs` (Any): Operation-specific parameters

#### TextAnalyzerTool
```python
class TextAnalyzerTool(BaseTool):
    def execute(self, text: str, analysis_type: str = "summary") -> Dict[str, Any]
```

**Parameters:**
- `text` (str): Text to analyze
- `analysis_type` (str): Type of analysis - defaults to "summary"

#### JSONProcessorTool
```python
class JSONProcessorTool(BaseTool):
    def execute(self, data: str, operation: str = "parse") -> Dict[str, Any]
```

**Parameters:**
- `data` (str): JSON data or string
- `operation` (str): Operation type - defaults to "parse"

### Development Tools

Tools for software development and engineering tasks.

#### GitTool
```python
class GitTool(BaseTool):
    def execute(self, command: str, repo_path: str = ".", **kwargs) -> Dict[str, Any]
```

**Parameters:**
- `command` (str): Git command to execute
- `repo_path` (str): Repository path - defaults to current directory

#### APITesterTool
```python
class APITesterTool(BaseTool):
    def execute(self, url: str, method: str = "GET", **kwargs) -> Dict[str, Any]
```

**Parameters:**
- `url` (str): API endpoint URL
- `method` (str): HTTP method - defaults to "GET"
- `**kwargs` (Any): Additional request parameters

#### DatabaseQueryTool
```python
class DatabaseQueryTool(BaseTool):
    def execute(self, query: str, connection_string: str, **kwargs) -> Dict[str, Any]
```

**Parameters:**
- `query` (str): SQL query to execute
- `connection_string` (str): Database connection string

#### CodeReviewerTool
```python
class CodeReviewerTool(BaseTool):
    def execute(self, code: str, language: str = "python") -> Dict[str, Any]
```

**Parameters:**
- `code` (str): Code to review
- `language` (str): Programming language - defaults to "python"

### Finance Tools

Tools for financial calculations and analysis.

#### CurrencyConverterTool
```python
class CurrencyConverterTool(BaseTool):
    def execute(self, amount: float, from_currency: str, to_currency: str) -> Dict[str, Any]
```

**Parameters:**
- `amount` (float): Amount to convert
- `from_currency` (str): Source currency code
- `to_currency` (str): Target currency code

#### TaxCalculatorTool
```python
class TaxCalculatorTool(BaseTool):
    def execute(self, income: float, state: str, filing_status: str) -> Dict[str, Any]
```

**Parameters:**
- `income` (float): Annual income
- `state` (str): State for tax calculation
- `filing_status` (str): Filing status

#### LoanCalculatorTool
```python
class LoanCalculatorTool(BaseTool):
    def execute(self, principal: float, rate: float, term_years: int) -> Dict[str, Any]
```

**Parameters:**
- `principal` (float): Loan principal amount
- `rate` (float): Annual interest rate
- `term_years` (int): Loan term in years

### Healthcare Tools

Tools for healthcare-related calculations and lookups.

#### BMICalculatorTool
```python
class BMICalculatorTool(BaseTool):
    def execute(self, weight_kg: float, height_cm: float) -> Dict[str, Any]
```

**Parameters:**
- `weight_kg` (float): Weight in kilograms
- `height_cm` (float): Height in centimeters

#### MedicalTermLookupTool
```python
class MedicalTermLookupTool(BaseTool):
    def execute(self, term: str) -> Dict[str, Any]
```

**Parameters:**
- `term` (str): Medical term to look up

#### DrugInteractionTool
```python
class DrugInteractionTool(BaseTool):
    def execute(self, drug1: str, drug2: str) -> Dict[str, Any]
```

**Parameters:**
- `drug1` (str): First drug name
- `drug2` (str): Second drug name

### Marketing Tools

Tools for marketing and business analysis.

#### SEOAnalyzerTool
```python
class SEOAnalyzerTool(BaseTool):
    def execute(self, url: str) -> Dict[str, Any]
```

**Parameters:**
- `url` (str): URL to analyze

#### EmailValidatorTool
```python
class EmailValidatorTool(BaseTool):
    def execute(self, email: str) -> Dict[str, Any]
```

**Parameters:**
- `email` (str): Email address to validate

#### SocialMetricsTool
```python
class SocialMetricsTool(BaseTool):
    def execute(self, platform: str, account: str) -> Dict[str, Any]
```

**Parameters:**
- `platform` (str): Social media platform
- `account` (str): Account username

### Legal Tools

Tools for legal research and document analysis.

#### LegalTermLookupTool
```python
class LegalTermLookupTool(BaseTool):
    def execute(self, term: str, jurisdiction: str = "US") -> Dict[str, Any]
```

**Parameters:**
- `term` (str): Legal term to look up
- `jurisdiction` (str): Legal jurisdiction - defaults to "US"

#### ContractAnalyzerTool
```python
class ContractAnalyzerTool(BaseTool):
    def execute(self, contract_text: str) -> Dict[str, Any]
```

**Parameters:**
- `contract_text` (str): Contract text to analyze

#### CaseSearchTool
```python
class CaseSearchTool(BaseTool):
    def execute(self, case_name: str, jurisdiction: str = "US") -> Dict[str, Any]
```

**Parameters:**
- `case_name` (str): Case name to search
- `jurisdiction` (str): Legal jurisdiction - defaults to "US"

### Education Tools

Tools for educational content and assessment.

#### GradeCalculatorTool
```python
class GradeCalculatorTool(BaseTool):
    def execute(self, scores: List[float], weights: List[float] = None) -> Dict[str, Any]
```

**Parameters:**
- `scores` (List[float]): List of scores
- `weights` (List[float], optional): List of weights for each score

#### StudySchedulerTool
```python
class StudySchedulerTool(BaseTool):
    def execute(self, subjects: List[str], hours_available: int) -> Dict[str, Any]
```

**Parameters:**
- `subjects` (List[str]): List of subjects to study
- `hours_available` (int): Available study hours

#### QuizGeneratorTool
```python
class QuizGeneratorTool(BaseTool):
    def execute(self, topic: str, num_questions: int = 10) -> Dict[str, Any]
```

**Parameters:**
- `topic` (str): Topic for quiz generation
- `num_questions` (int): Number of questions - defaults to 10

## Tool Factory Functions

### create_tool_by_name()
```python
def create_tool_by_name(tool_name: str, **kwargs) -> BaseTool:
    """Create a tool instance by name."""
```

**Parameters:**
- `tool_name` (str): Name of the tool to create
- `**kwargs` (Any): Tool-specific configuration

**Returns:** Tool instance

### get_available_tools()
```python
def get_available_tools() -> List[str]:
    """Get list of all available tool names."""
```

**Returns:** List of available tool names

### get_default_tools()
```python
def get_default_tools() -> List[BaseTool]:
    """Get list of default tools for agents."""
```

**Returns:** List of default tool instances

### get_tools_by_category()
```python
def get_tools_by_category(category: str) -> List[str]:
    """Get all tools in a specific category."""
```

**Parameters:**
- `category` (str): Tool category

**Returns:** List of tool names in the category

## Tool Registry

### ToolRegistry

Manages tool registration and discovery.

```python
class ToolRegistry:
    def __init__(self)
    
    def register_tool(self, tool_class: Type[BaseTool]) -> None
    
    def get_tool(self, name: str) -> Optional[Type[BaseTool]]
    
    def list_tools(self, category: Optional[str] = None) -> List[str]
    
    def get_tool_schema(self, name: str) -> Optional[Dict[str, Any]]
```

## Example Usage

```python
from superoptix.tools import (
    BaseTool,
    WebSearchTool,
    CalculatorTool,
    create_tool_by_name,
    get_default_tools,
    get_available_tools
)

# Create tools using factory functions
web_search = create_tool_by_name("WebSearchTool", api_key="your_api_key")
calculator = create_tool_by_name("CalculatorTool")

# Execute tools
search_results = web_search.execute(
    query="SuperOptiX framework",
    max_results=5
)

calc_result = calculator.execute(expression="2 + 2 * 3")

# Get default tools for an agent
default_tools = get_default_tools()
print(f"Default tools: {[tool.name for tool in default_tools]}")

# Get all available tools
available_tools = get_available_tools()
print(f"Available tools: {len(available_tools)}")

# Create custom tool
class CustomTool(BaseTool):
    def __init__(self):
        super().__init__(
            name="custom_tool",
            description="A custom tool for specific tasks",
            category="custom"
        )
    
    def execute(self, input_data: str) -> Dict[str, Any]:
        # Custom logic here
        return {
            "result": f"Processed: {input_data}",
            "status": "success"
        }
    
    def validate_input(self, input_data: str) -> bool:
        return isinstance(input_data, str) and len(input_data) > 0

# Use custom tool
custom_tool = CustomTool()
result = custom_tool.execute("test data")

# Tool categories
from superoptix.tools import get_tools_by_category

core_tools = get_tools_by_category("core")
dev_tools = get_tools_by_category("development")
finance_tools = get_tools_by_category("finance")

print(f"Core tools: {core_tools}")
print(f"Development tools: {dev_tools}")
print(f"Finance tools: {finance_tools}")

# Tool statistics
from superoptix.tools import get_tool_stats

stats = get_tool_stats()
print(f"Total tools: {stats['total_tools']}")
print(f"Categories: {stats['categories']}")
print(f"Version: {stats['version']}")

# Using tools in agent pipeline
class MyAgent(SuperOptixPipeline):
    def get_custom_tools(self):
        return [
            WebSearchTool(api_key="your_key"),
            CalculatorTool(),
            CustomTool()
        ]
    
    def forward(self, query: str) -> dspy.Prediction:
        # Use tools in reasoning
        if "calculate" in query.lower():
            result = self.tools[1].execute(expression=query)
            return dspy.Prediction(answer=f"Calculation result: {result}")
        
        # Use web search
        search_results = self.tools[0].execute(query=query)
        return dspy.Prediction(answer=f"Found: {search_results}")
```

## Tool Configuration

### Web Search Configuration

```python
web_search_config = {
    "api_key": "your_api_key",
    "search_engine": "google",  # google, bing, duckduckgo
    "max_results": 5,
    "timeout": 30
}
```

### Database Configuration

```python
db_config = {
    "connection_string": "postgresql://user:pass@localhost/db",
    "timeout": 30,
    "max_connections": 10
}
```

### API Configuration

```python
api_config = {
    "timeout": 30,
    "retry_attempts": 3,
    "headers": {"User-Agent": "SuperOptiX/1.0"}
}
```

## Error Handling

### ToolError

Base exception for tool-related errors.

```python
class ToolError(Exception):
    pass
```

### ToolExecutionError

Raised when tool execution fails.

```python
class ToolExecutionError(ToolError):
    pass
```

### ToolValidationError

Raised when tool input validation fails.

```python
class ToolValidationError(ToolError):
    pass
```

## Tool Schema

Tools can provide schemas for parameter validation:

```python
def get_schema(self) -> Dict[str, Any]:
    return {
        "name": "calculator",
        "description": "Performs mathematical calculations",
        "parameters": {
            "expression": {
                "type": "string",
                "description": "Mathematical expression to evaluate",
                "required": True
            }
        },
        "returns": {
            "type": "object",
            "properties": {
                "result": {"type": "number"},
                "status": {"type": "string"}
            }
        }
    }
``` 