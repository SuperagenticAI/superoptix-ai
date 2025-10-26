# 🧠 DeepAgents Framework Integration

**SuperOptiX now supports DeepAgents - a LangGraph-based framework for building "deep" agents with planning, filesystem access, and subagent spawning capabilities!**

---

## 🎯 What is DeepAgents?

DeepAgents is a framework for creating sophisticated agents that go beyond simple tool-calling loops. It provides:

- 📋 **Planning Tools**: Break down complex tasks with `write_todos`
- 📁 **Filesystem Access**: Offload context with `read_file`, `write_file`, `ls`, `edit_file`
- 👥 **Subagent Spawning**: Delegate specialized tasks to focused subagents
- 💾 **Long-term Memory**: Persist information across conversations

Perfect for complex research, code generation, and multi-step workflows!

---

## 📦 Installation

```bash
pip install superoptix[frameworks-deepagents]==0.2.0b1 --pre
```

**Includes:**
- deepagents (latest)
- SuperOptiX core with GEPA 0.0.17

**Requirements:**
- Python 3.11+
- Git (for DSPy dependency)
- API keys for Claude or GPT-4 (function-calling models)

---

## 🚀 Quick Start

### 1. Pull the Demo Agent

```bash
cd your_project
super agent pull research_agent_deepagents
```

### 2. Configure Model

**⚠️ Important: DeepAgents requires function-calling models**

Edit `agents/research_agent_deepagents/playbook/research_agent_deepagents_playbook.yaml`:

```yaml
language_model:
  provider: anthropic
  model: anthropic:claude-sonnet-4-20250514
  temperature: 0.7
  max_tokens: 4000
```

**Supported Models:**
- ✅ **Claude**: `anthropic:claude-sonnet-4-20250514` (recommended)
- ✅ **OpenAI**: `openai:gpt-4-turbo`, `openai:gpt-4`
- ✅ **Google**: `google-genai:gemini-2.0-flash`

**Not Yet Supported:**
- ❌ **Ollama models**: LangChain's ChatOllama doesn't implement `bind_tools()` yet
  - Tracking: [LangChain Issue](https://github.com/langchain-ai/langchain/issues)

### 3. Set API Key

```bash
export ANTHROPIC_API_KEY=your_key
# OR
export OPENAI_API_KEY=your_key
```

### 4. Run the Workflow

```bash
# Compile (generate DeepAgents pipeline code)
super agent compile research_agent_deepagents --framework deepagents

# Evaluate (run BDD scenarios)
super agent evaluate research_agent_deepagents

# Optimize with GEPA (optimize system prompt)
super agent optimize research_agent_deepagents --auto medium

# Run agent
super agent run research_agent_deepagents --query "Research the state of AI in 2025"
```

---

## 📋 Creating Your Own DeepAgents Playbook

### Basic Structure

```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: My Research Agent
  id: my_research_agent
  namespace: demo
  version: 1.0.0
  level: genies
  description: Custom research agent built with DeepAgents

spec:
  target_framework: deepagents
  
  language_model:
    provider: anthropic
    model: anthropic:claude-sonnet-4-20250514
    temperature: 0.7
    max_tokens: 4000
  
  input_fields:
    - name: query
      type: str
      description: Research question
      required: true
  
  output_fields:
    - name: report
      type: str
      description: Research report
      required: true
  
  persona:
    name: Research Agent
    role: Expert AI Researcher
    goal: Conduct thorough research and produce comprehensive reports
    traits:
      - analytical
      - thorough
  
  reasoning:
    method: planning
    steps:
      - Break down research into subtasks using write_todos
      - Search for authoritative sources
      - Save findings to files
      - Synthesize information
      - Write comprehensive report
  
  tools:
    enabled: true
    specific_tools:
      - internet_search
      - file_system
      - write_todos
  
  # BDD Scenarios for testing
  feature_specifications:
    scenarios:
      - name: Simple research
        description: Answer basic question
        input:
          query: "What is LangGraph?"
        expected_output:
          report: "Research report"
          expected_keywords:
            - LangGraph
            - framework
  
  optimization:
    optimizer:
      name: GEPA
      params:
        metric: response_accuracy
        auto: medium
```

---

## 🔄 Complete Workflow

### Step 1: Initialize Project

```bash
super init my_project
cd my_project
```

### Step 2: Create or Pull Agent

```bash
# Option A: Pull prebuilt agent
super agent pull research_agent_deepagents

# Option B: Create custom playbook
# (Create your_agent_playbook.yaml in agents/your_agent/playbook/)
```

### Step 3: Compile

```bash
super agent compile research_agent_deepagents --framework deepagents
```

**What happens:**
- Reads playbook YAML
- Generates Python pipeline using `deepagents_pipeline.py.jinja2` template
- Creates `BaseComponent` wrapper for GEPA optimization
- Adds BDD test loading
- Creates evaluation methods

**Output:** `agents/research_agent_deepagents/pipelines/research_agent_deepagents_deepagents_pipeline.py`

### Step 4: Evaluate

```bash
super agent evaluate research_agent_deepagents
```

**What happens:**
- Loads compiled pipeline
- Initializes DeepAgents agent
- Runs BDD scenarios from playbook
- Tests against expected outputs
- Shows pass/fail rate

**Example Output:**
```
✅ Simple research query: PASS
✅ Technical comparison: PASS
❌ Complex research: FAIL

Overall: 2/3 PASS (66.7%)
```

### Step 5: Optimize with GEPA

```bash
super agent optimize research_agent_deepagents --auto medium
```

**What happens:**
- Universal GEPA optimizer analyzes agent performance
- Optimizes the `system_prompt` (the optimizable variable)
- Runs multiple iterations with different prompts
- Selects best performing version
- Saves optimized weights

**Key Innovation:** GEPA optimizes DeepAgents agents even though they're not DSPy!

### Step 6: Re-evaluate

```bash
super agent evaluate research_agent_deepagents
```

**What happens:**
- Loads optimized system prompt
- Re-runs BDD scenarios
- Shows improvement

**Expected:** Higher pass rate after optimization!

### Step 7: Run

```bash
super agent run research_agent_deepagents --query "Research AI trends in 2025"
```

---

## 🔧 How It Works Under the Hood

### BaseComponent Wrapper

DeepAgents agents are wrapped in `BaseComponent` to make them GEPA-optimizable:

```python
class ResearchAgentDeepAgentsComponent(BaseComponent):
    def __init__(self, system_prompt=None, ...):
        super().__init__(
            name="research_agent_deepagents",
            variable=system_prompt,  # GEPA optimizes this!
            variable_type="system_prompt",
            framework="deepagents",
            ...
        )
    
    def forward(self, **inputs):
        # Execute DeepAgents agent
        result = self._agent.invoke({"messages": messages})
        return {"response": result["messages"][-1]["content"]}
    
    def update(self, new_variable):
        # GEPA calls this during optimization
        self.variable = new_variable
        # Reinitialize agent with new prompt
        self._agent = None
```

### Pipeline Class

The generated pipeline includes:

```python
class ResearchAgentDeepAgentsPipeline:
    def __init__(self, playbook_path=None):
        # Load playbook and BDD scenarios
        self.component = create_research_agent_deep_agents_agent()
        self.test_scenarios = self._load_bdd_scenarios()
    
    def run(self, **inputs):
        # Execute agent
        return self.component.forward(**inputs)
    
    def evaluate(self):
        # Run BDD scenarios
        for scenario in self.test_scenarios:
            result = self.run(**scenario["input"])
            # Compare with expected output
    
    def optimize_with_gepa(self, auto="medium"):
        # Universal GEPA optimization
        optimizer = UniversalGEPA(...)
        result = optimizer.compile(
            component=self.component,
            trainset=trainset,
            valset=valset
        )
    
    def run_bdd_test_suite(self):
        # CLI compatibility wrapper
        return self.evaluate()
```

---

## 📊 DeepAgents vs DSPy

| Feature | DeepAgents | DSPy |
|---------|-----------|------|
| **Framework** | LangGraph | DSPy |
| **Strength** | Complex multi-step tasks | Prompt optimization |
| **Planning** | Built-in `write_todos` | Manual implementation |
| **Filesystem** | Built-in tools | Manual implementation |
| **Subagents** | Native support | Manual composition |
| **SuperOptiX Support** | ✅ Full workflow | ✅ Full workflow |
| **GEPA Optimization** | ✅ system_prompt | ✅ All signatures |
| **Model Requirements** | Function-calling only | Any LLM |
| **Ollama Support** | ⚠️ Blocked (LangChain issue) | ✅ Full support |

**When to use DeepAgents:**
- Complex research tasks
- Multi-step workflows requiring planning
- Need filesystem for context management
- Want subagent delegation

**When to use DSPy:**
- Need Ollama/local model support
- Focus on prompt optimization
- Simpler task structures
- Want maximum flexibility

---

## 🎓 Example Use Cases

### Research Agent
```yaml
persona:
  role: Expert AI Researcher
  goal: Conduct thorough research and produce comprehensive reports
reasoning:
  method: planning
tools:
  specific_tools:
    - internet_search
    - file_system
    - write_todos
```

### Code Assistant
```yaml
persona:
  role: Senior Software Engineer
  goal: Write high-quality code with proper documentation
reasoning:
  method: planning
tools:
  specific_tools:
    - file_system  # Read/write code files
    - write_todos  # Plan implementation
    - code_executor  # Test code
```

### Data Analyst
```yaml
persona:
  role: Data Science Expert
  goal: Analyze datasets and provide insights
reasoning:
  method: planning
tools:
  specific_tools:
    - file_system
    - write_todos
subagents:
  - name: visualization-specialist
    description: Create charts and graphs
  - name: statistics-expert
    description: Run statistical analysis
```

---

## ⚙️ Advanced Configuration

### Custom Subagents

```yaml
subagents:
  - name: research-specialist
    description: Deep dive into specific topics
    system_prompt: You are an expert researcher focused on academic papers
    tools:
      - academic_search
      - citation_checker
    model: anthropic:claude-sonnet-4-20250514
```

### Custom Tools

Define tools in the `tools` section:

```yaml
tools:
  enabled: true
  specific_tools:
    - name: database_query
      description: Query production database
      implementation: custom
    - name: api_call
      description: Call external API
      implementation: custom
```

Implement in the generated pipeline or provide as functions.

---

## 🐛 Troubleshooting

### NotImplementedError in bind_tools()

**Symptom:**
```
NotImplementedError
  at langchain_core.language_models.chat_models.py line 1491
```

**Cause:** Using Ollama model with DeepAgents

**Solution:** Use function-calling capable models:
```yaml
language_model:
  provider: anthropic
  model: anthropic:claude-sonnet-4-20250514
```

### Agent Initialization Failed

**Symptom:** "Failed to initialize DeepAgents"

**Checklist:**
1. ✅ API key set? (`ANTHROPIC_API_KEY`, `OPENAI_API_KEY`)
2. ✅ Model string correct? (e.g., `anthropic:claude-sonnet-4-20250514`)
3. ✅ LangChain dependencies installed? (`pip install langchain langchain-anthropic`)

### No BDD Specifications Found

**Symptom:** "❌ No BDD specifications found!"

**Solution:** Add scenarios to playbook:
```yaml
feature_specifications:
  scenarios:
    - name: Basic test
      input:
        query: "Test query"
      expected_output:
        report: "Expected result"
```

Then recompile:
```bash
super agent compile your_agent --framework deepagents
```

---

## 🎯 GEPA Optimization Details

### What Gets Optimized

DeepAgents agents have one optimizable variable:
- **`system_prompt`**: The main instruction to the agent

GEPA automatically:
1. Analyzes agent performance on BDD scenarios
2. Generates variations of the system prompt
3. Tests each variation
4. Selects the best performing prompt
5. Saves optimized version

### Optimization Example

**Before (Baseline):**
```
System Prompt: "You are an expert researcher."
Pass Rate: 33.3%
```

**After GEPA Optimization:**
```
System Prompt: "You are an expert researcher. When answering questions:
1. Use write_todos to plan your research steps
2. Save findings to research_notes.md
3. Synthesize information before responding
..."
Pass Rate: 66.7%
```

---

## 🏗️ Architecture

```
SuperSpec YAML Playbook
        ↓
    Compiler (AgentCompiler)
        ↓
DeepAgents Pipeline Template (deepagents_pipeline.py.jinja2)
        ↓
Generated Python Pipeline
        ├─ ResearchAgentDeepAgentsComponent (BaseComponent wrapper)
        │   └─ create_deep_agent() ← Real DeepAgents implementation
        └─ ResearchAgentDeepAgentsPipeline
            ├─ run()
            ├─ evaluate()
            ├─ optimize_with_gepa() ← Universal GEPA
            └─ run_bdd_test_suite()
```

---

## 📚 Additional Resources

- **DeepAgents Docs**: https://github.com/langchain-ai/deepagents
- **LangGraph Docs**: https://langchain-ai.github.io/langgraph/
- **SuperOptiX Multi-Framework Guide**: `/docs/guides/multi-framework.md`
- **Universal GEPA**: `/docs/guides/universal-gepa.md`

---

## 💡 Tips & Best Practices

### 1. Use Detailed System Prompts
DeepAgents shine with detailed instructions:
```yaml
persona:
  role: Expert Researcher
  goal: |
    Conduct thorough research on AI topics, producing
    comprehensive, well-sourced reports
  backstory: |
    You have 10+ years of experience in AI research
```

### 2. Leverage Planning
Always include `write_todos` in tools:
```yaml
reasoning:
  steps:
    - Break down research into subtasks using write_todos
    - Execute each subtask systematically
```

### 3. Use Filesystem for Context
For long outputs, instruct agent to save to files:
```yaml
constraints:
  - Save research findings to research_notes.md
  - Keep main context clean
```

### 4. Start Simple, Then Optimize
1. Get baseline working (compile + evaluate)
2. Run optimization (GEPA improves the prompt)
3. Iterate on scenarios based on failures

---

## 🎓 Comparison with Other Frameworks

### DeepAgents + SuperOptiX Advantages
- ✅ Built-in planning and filesystem
- ✅ GEPA optimization works
- ✅ Standard SuperOptiX workflow
- ✅ Full LangGraph features (streaming, checkpointing, etc.)

### DSPy + SuperOptiX Advantages
- ✅ Works with Ollama (no function-calling requirement)
- ✅ More optimization targets (all signatures, not just system_prompt)
- ✅ Better for simple, focused tasks
- ✅ Native to SuperOptiX

### Use Both!
SuperOptiX lets you:
- Use **DSPy** for simple tasks with Ollama
- Use **DeepAgents** for complex tasks with Claude/GPT-4
- **Optimize both** with the same workflow!

---

## 🚀 Next Steps

1. **Try the demo agent**:
   ```bash
   super agent pull research_agent_deepagents
   super agent compile research_agent_deepagents --framework deepagents
   super agent evaluate research_agent_deepagents
   ```

2. **Create your own DeepAgents agent**:
   - Copy the demo playbook
   - Customize persona, tools, and scenarios
   - Compile and optimize!

3. **Explore other frameworks**:
   - CrewAI (coming soon)
   - Microsoft Agent Framework (coming soon)
   - OpenAI Agents SDK (coming soon)

---

## ❓ FAQ

**Q: Why can't I use Ollama with DeepAgents?**  
A: LangChain's ChatOllama doesn't implement `bind_tools()` yet. This is a LangChain limitation, not SuperOptiX or DeepAgents. We're tracking the issue.

**Q: Can I use local models at all?**  
A: Yes! Use DSPy agents which work perfectly with Ollama. The workflow is identical.

**Q: Does GEPA really optimize DeepAgents?**  
A: Yes! Universal GEPA optimizes the `system_prompt` through the BaseComponent interface. It's framework-agnostic.

**Q: Can I mix DSPy and DeepAgents agents?**  
A: Absolutely! Create orchestrations that use both. Each agent uses the best framework for its task.

**Q: What about other frameworks?**  
A: Coming soon! We're extending the same pattern to CrewAI, Microsoft, OpenAI SDK, and Google ADK.

---

## 🎉 Success Stories

**What Users Are Building:**
- Complex research agents with multi-step planning
- Code assistants with filesystem access
- Data analysis agents with specialized subagents
- All optimized with GEPA for better performance!

**The SuperOptiX Advantage:**
"Finally, one workflow to rule them all - whether you use DSPy, DeepAgents, or any other framework!"

---

*Need help? Check our [Discord](https://discord.gg/superoptix) or [open an issue](https://github.com/Shashikant86/SuperOptiX/issues)!*


