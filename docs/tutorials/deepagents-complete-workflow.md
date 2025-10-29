# 🎯 DeepAgents Complete End-to-End Workflow

**A comprehensive, step-by-step guide to building, running, evaluating, and optimizing DeepAgents with SuperOptiX. Follow along and build production-ready agents with persistent memory, real file access, and GEPA optimization - all using FREE Gemini models!**

---

## 📖 Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Step-by-Step Workflow](#step-by-step-workflow)
4. [Backend Configuration](#backend-configuration)
5. [Advanced Examples](#advanced-examples)
6. [Troubleshooting](#troubleshooting)
7. [Production Deployment](#production-deployment)

**Time to Complete:** 30-45 minutes  
**Difficulty:** Intermediate  
**Cost:** $0.00 (FREE tier with Gemini!)

---

## 🎯 Introduction

### What You'll Build

By the end of this tutorial, you'll have:

- ✅ A fully functional DeepAgents research assistant
- ✅ Real Gemini API integration (FREE tier)
- ✅ Automated evaluation with BDD scenarios
- ✅ GEPA-optimized system prompts (+20-30% improvement)
- ✅ Production-ready agent deployment

### What is DeepAgents?

DeepAgents 0.2.0 is LangChain's framework for building **"deep agents"** - sophisticated, long-running agents that can:

- 📋 **Plan** complex tasks with `write_todos`
- 📁 **Manage files** with 6 filesystem tools
- 👥 **Spawn subagents** for specialized tasks
- 🗄️ **Persist memory** across conversations (NEW in 0.2.0!)
- 📂 **Access real files** on your computer (NEW in 0.2.0!)

**Source:** [LangChain Blog - Doubling Down on DeepAgents](https://blog.langchain.com/doubling-down-on-deepagents/)

---

## 📋 Prerequisites

### 1. System Requirements

- **Python 3.11+** (required)
- **SuperOptiX installed** (see below)
- **Internet connection** (for Gemini API)

### 2. Install SuperOptiX

```bash
# Install SuperOptiX with DeepAgents support
pip install superoptix[frameworks-deepagents]

# REQUIRED: Install Gemini integration for LangChain
pip install langchain-google-genai
```

**What gets installed:**
- SuperOptiX core
- DeepAgents 0.2.0+ with backend support
- LangChain, LangGraph integration
- GEPA optimizer
- Google Gemini integration for LangChain

### 3. Get FREE Gemini API Key

**Why Gemini?**
- ✅ FREE tier with generous quotas
- ✅ Function-calling support (required for DeepAgents)
- ✅ Fast (1-3 second responses)
- ✅ GPT-4 class quality

**Steps:**
1. Go to [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Sign in with your Google account
3. Click **"Create API Key"** or **"Get API Key"**
4. Copy the key (format: `AIzaSy...`)

**Free Tier Limits:**
- 15 requests per minute
- 1,500 requests per day  
- 1M tokens per minute
- ✅ **More than enough for development and testing!**

### 4. Set Environment Variable

=== "Fish Shell"
    ```bash
    # Add to ~/.config/fish/config.fish
    set -x GOOGLE_API_KEY "AIzaSy-your-actual-key-here"
    
    # Reload config
    source ~/.config/fish/config.fish
    
    # Verify
    echo $GOOGLE_API_KEY
    ```

=== "Bash/Zsh"
    ```bash
    # Add to ~/.bashrc or ~/.zshrc
    export GOOGLE_API_KEY="AIzaSy-your-actual-key-here"
    
    # Reload config
    source ~/.bashrc  # or source ~/.zshrc
    
    # Verify
    echo $GOOGLE_API_KEY
    ```

=== "Temporary (Current Session Only)"
    ```bash
    # Set for current terminal session
    export GOOGLE_API_KEY="AIzaSy-your-actual-key-here"
    
    # Verify
    echo $GOOGLE_API_KEY
    ```

### 5. Verify Installation

```bash
# Check SuperOptiX
super --version

# Check DeepAgents backends
python -c "from superoptix.vendor.deepagents.backends import StateBackend, StoreBackend, FilesystemBackend, CompositeBackend; print('✅ All backends available!')"

# Check Gemini integration
python -c "from langchain_google_genai import ChatGoogleGenerativeAI; print('✅ Gemini integration ready!')"
```

**Expected Output:**
```
SuperOptiX version 0.1.4
✅ All backends available!
✅ Gemini integration ready!
```

---

## 🚀 Step-by-Step Workflow

### Step 1: Initialize Project

Create a new SuperOptiX project:

```bash
# Create project
super init my_deepagents_project

# Navigate to project directory
cd my_deepagents_project

# Verify structure
ls -la
```

**Expected Output:**
```
╭──────────────────────────────────────────────────────────────────────────────╮
│ 🎉 SUCCESS! Your full-blown shippable Agentic System 'my_deepagents_project' │
│ is ready!                                                                    │
╰──────────────────────────────────────────────────────────────────────────────╯

Your project structure:
my_deepagents_project/
├── .super                 # Project metadata
├── .gitignore
├── README.md
├── pyproject.toml
└── my_deepagents_project/
    ├── agents/            # Your agents go here
    ├── guardrails/
    ├── memory/
    ├── protocols/
    ├── teams/
    ├── evals/
    ├── knowledge/
    ├── optimizers/
    ├── servers/
    └── tools/
```

**✅ Checkpoint:** You should have a `.super` file in your directory. All `super` commands must run from this directory.

---

### Step 2: Pull Demo Agent

Pull the DeepAgents research assistant demo:

```bash
super agent pull research_agent_deepagents
```

**Expected Output:**
```
╭──────────────────────────────────────────────────────────────────────────────╮
│ 🎉 AGENT ADDED SUCCESSFULLY! Pre-built Agent Ready                           │
╰──────────────────────────────────────────────────────────────────────────────╯
╭────────────────────────────── 📋 Agent Details ──────────────────────────────╮
│                                                                              │
│  🤖 Name: Research Agent (DeepAgents)                                        │
│  🏢 Industry: Demo | 🔮 Tier: Oracles                                        │
│  📁 Location: my_deepagents_project/agents/research_agent_deepagents/        │
│                                                                              │
╰──────────────────────────────────────────────────────────────────────────────╯
```

**What was created:**
```
my_deepagents_project/agents/research_agent_deepagents/
├── playbook/
│   └── research_agent_deepagents_playbook.yaml  # Agent configuration
└── pipelines/                                   # Will be created on compile
```

**✅ Checkpoint:** Check that the playbook file exists:
```bash
cat my_deepagents_project/agents/research_agent_deepagents/playbook/research_agent_deepagents_playbook.yaml | head -20
```

---

### Step 3: Inspect Agent Configuration

Let's look at what we just pulled:

```bash
cat my_deepagents_project/agents/research_agent_deepagents/playbook/research_agent_deepagents_playbook.yaml
```

**Key Configuration Sections:**

```yaml
metadata:
  name: Research Agent (DeepAgents)
  description: Research assistant built with DeepAgents

spec:
  target_framework: deepagents  # Uses DeepAgents framework
  
  language_model:
    provider: google-genai
    model: google-genai:gemini-2.5-flash  # Use latest model from provider
    temperature: 0.7
    max_tokens: 8192
    # Note: Model names may change as providers release new versions.
    # Check provider docs for latest models: https://ai.google.dev/models
  
  backend:
    type: state  # Default: ephemeral storage (can change to 'store' for persistence)
  
  persona:
    role: Expert AI Researcher
    goal: Conduct thorough research on AI and technology topics
  
  # BDD test scenarios
  feature_specifications:
    scenarios:
      - name: Simple research query
        input:
          query: "What is LangGraph?"
        expected_output:
          report: "LangGraph is a framework..."
  
  # GEPA optimization configuration
  optimization:
    optimizer:
      name: GEPA
      params:
        metric: response_accuracy
        auto: medium
        reflection_lm: google-genai:gemini-2.5-pro  # FREE Gemini Pro for reflection!
```

**✅ Checkpoint:** Note the `target_framework: deepagents` - this tells SuperOptiX to compile for DeepAgents.

---

### Step 4: Compile Agent

Transform the YAML playbook into executable Python code:

```bash
super agent compile research_agent_deepagents --framework deepagents
```

**Expected Output:**
```
================================================================================

🔨 Compiling agent 'research_agent_deepagents'...
╭─────────────────────────── ⚡ Compilation Details ───────────────────────────╮
│                                                                              │
│  🎯 Agent: Research Agent (DeepAgents)                                       │
│  🏗️ Framework: DeepAgents (LangGraph)                                        │
│  🔧 Process: YAML playbook → Executable Python pipeline                      │
│  📁 Output: my_deepagents_project/agents/research_agent_deepagents/          │
│            pipelines/research_agent_deepagents_deepagents_pipeline.py        │
│                                                                              │
╰──────────────────────────────────────────────────────────────────────────────╯

🐍 Converted field names to snake_case for DSPy compatibility
✅ Tools configuration detected for Genies tier
✅ Successfully compiled with DEEPAGENTS framework
╭──────────────────────────────────────────────────────────────────────────────╮
│ 🎉 COMPILATION SUCCESSFUL! Pipeline Generated                                │
╰──────────────────────────────────────────────────────────────────────────────╯
```

**What was created:**
- `research_agent_deepagents_deepagents_pipeline.py` (~28KB, 766 lines)
- Contains `ResearchAgentDeepAgentsComponent` (BaseComponent wrapper)
- Contains `ResearchAgentDeepAgentsPipeline` (executable pipeline)
- Includes `_create_backend()` method for backend support

**✅ Checkpoint:** Verify the pipeline file exists:
```bash
ls -lh my_deepagents_project/agents/research_agent_deepagents/pipelines/
# Should show: research_agent_deepagents_deepagents_pipeline.py (~28KB)
```

---

### Step 5: Run Agent (First Execution)

Execute the agent with a simple query:

```bash
super agent run research_agent_deepagents --goal "What is 2 + 2? Answer with just the number."
```

**Expected Output:**
```
📊 Observability: superoptix
🚀 Running agent 'research_agent_deepagents'...

Running with base model (not optimized)...

📝 Using base pipeline (no optimization available)

Looking for pipeline at: my_deepagents_project/agents/research_agent_deepagents/
pipelines/research_agent_deepagents_deepagents_pipeline.py

╭────────────────────────────── Agent Execution ───────────────────────────────╮
│ 🤖 Running Research_Agent_Deepagents Pipeline                                │
│                                                                              │
│ Executing Task: What is 2 + 2? Answer with just the number.                  │
│                                                                              │
╰──────────────────────────────────────────────────────────────────────────────╯

✅ DeepAgents agent initialized with model: google-genai:gemini-2.5-flash

                                Analysis Results                                
┏━━━━━━━━━━┳━━━━━━━┓
┃ Aspect   ┃ Value ┃
┡━━━━━━━━━━╇━━━━━━━┩
│ Response │ 4     │
└──────────┴───────┘

Pre-Optimized Pipeline: ⚪ NO
Runtime Optimization: ⚪ NO

Validation Status: ✅ PASSED
```

**🎉 Success!** You just ran your first DeepAgents agent with real Gemini API!

**What happened:**
1. Agent loaded with Gemini 2.5 Flash model
2. Made real API call to Gemini
3. Got response: "4"
4. All using your FREE API quota!

**✅ Checkpoint:** Try a more complex query:
```bash
super agent run research_agent_deepagents --goal "What is LangGraph? Answer in exactly 2 sentences."
```

**Expected Response:**
```
Response │ LangGraph is a library that helps build stateful, multi-actor 
         │ applications with LLMs, by representing computation as a graph. 
         │ It extends LangChain by enabling cyclic execution flows, allowing 
         │ for more complex and dynamic agent behaviors.
```

---

### Step 6: Evaluate Agent (Baseline Performance)

Run BDD scenarios to establish baseline performance:

```bash
super agent evaluate research_agent_deepagents
```

**Expected Output:**
```
═══════════════════════════════════════════════════════════════════════════════
🧪 SuperOptiX BDD Spec Runner - Professional Agent Validation
═══════════════════════════════════════════════════════════════════════════════

📋 Test Configuration
┏━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Attribute       ┃ Value                              ┃
┡━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ Agent           │ research_agent_deepagents          │
│ Framework       │ DeepAgents                         │
│ Optimization    │ ⚙️  Base Model                     │
│ Specifications  │ 3 BDD scenarios                    │
└─────────────────┴────────────────────────────────────┘

🔍 Discovering BDD Specifications...
📋 Found 3 BDD specifications

🧪 Executing BDD Specification Suite
────────────────────────────────────────────────────────────

🔍 Evaluating research_agent_deep_agents...

Testing 3 BDD scenarios:

✅ DeepAgents agent initialized with model: google-genai:gemini-2.5-flash
✅ Simple research query: PASS
❌ Technical comparison: FAIL
❌ Complex research: FAIL

============================================================
Overall: 1/3 PASS (33.3%)
============================================================

╭────────────────────── 🔴 Specification Results Summary ──────────────────────╮
│                                                                              │
│  📊 Total Specs:         3                🎯 Pass Rate:         33.3%        │
│  ✅ Passed:              1                                                   │
│  ❌ Failed:              2                                                   │
│  🏆 Quality Gate:        ❌ NEEDS WORK                                       │
│                                                                              │
╰──────────────────────────────────────────────────────────────────────────────╯
```

**Analysis:**
- **Baseline performance: 33.3%** (1 out of 3 scenarios pass)
- Simple queries work well
- Complex research needs improvement
- **Perfect candidate for GEPA optimization!**

**✅ Checkpoint:** Note your baseline score - we'll compare after optimization.

---

### Step 7: Optimize with GEPA (The Magic!)

Now let's use GEPA to automatically improve the agent:

```bash
super agent optimize research_agent_deepagents \
  --framework deepagents \
  --auto medium \
  --reflection-lm google-genai:gemini-2.5-pro
```

**What's happening:**
- `--framework deepagents` - Specifies the framework
- `--auto medium` - GEPA budget (light/medium/heavy)
- `--reflection-lm gemini-2.5-pro` - Uses Pro model for better reflection

**Expected Output:**
```
================================================================================

🚀 Optimizing agent 'research_agent_deepagents'...

🌟 Using Universal GEPA Optimizer
   Framework: deepagents

🔬 Running Universal GEPA Optimization
   Framework: deepagents
   Training examples: 3
   Train: 2, Val: 1

📦 Creating deepagents component...
   ✅ Component created: research_agent_deep_agents
   Framework: deepagents
   Optimizable: True

🚀 Initializing Universal GEPA optimizer...
   ✅ Optimizer created
   Budget: medium
   Reflection LM: google-genai:gemini-2.5-pro

⚡ Running GEPA optimization...
   This may take 5-10 minutes...

✅ DeepAgents agent initialized with model: google-genai:gemini-2.5-flash

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Iteration 0: Base program full valset score: 0.33
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Reflection on failures...
Proposing improvements...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Iteration 1: Testing 3 candidates...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ Candidate 1: Score 0.50 (+51% improvement!)
✅ Candidate 2: Score 0.67 (+103% improvement!)
✅ Candidate 3: Score 0.50 (+51% improvement!)

🎯 Best candidate: #2 with score 0.67

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Iteration 2: Testing 3 candidates...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ Candidate 1: Score 0.83 (+152% improvement!)
✅ Candidate 2: Score 0.67 (+103% improvement!)
✅ Candidate 3: Score 0.67 (+103% improvement!)

🎯 New best! Score: 0.83 (was 0.33)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Iteration 3: Testing 3 candidates...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ Candidate 1: Score 0.83 (+152% improvement!)
✅ Candidate 2: Score 1.00 (+203% improvement! 🎉)
✅ Candidate 3: Score 0.83 (+152% improvement!)

🎯 New best! Score: 1.00 (PERFECT!)

╭──────────────────────────────────────────────────────────────────────────────╮
│ ✅ OPTIMIZATION COMPLETE!                                                    │
╰──────────────────────────────────────────────────────────────────────────────╯

📊 Results:
   Initial Score:  0.33 (33.3%)
   Final Score:    1.00 (100.0%)
   Improvement:    +203% (0.33 → 1.00)

📁 Optimized prompt saved to:
   my_deepagents_project/agents/research_agent_deepagents/optimized/

💡 Next steps:
   1. Review optimized results
   2. Test: super agent run research_agent_deepagents
   3. Evaluate: super agent evaluate research_agent_deepagents --load-optimized
```

**What GEPA did:**
1. **Analyzed failures** from baseline
2. **Reflected** on why scenarios failed
3. **Proposed** 3 improved system prompts per iteration
4. **Evaluated** each proposal
5. **Selected** best performer (Pareto selection)
6. **Repeated** for 3 iterations
7. **Achieved** significantly improved performance (results vary by hardware and model)

**Cost:** $0.00 (all using FREE Gemini quota!)

**API Calls Made:**
- ~10 execution calls (Gemini 2.5 Flash)
- ~6 reflection calls (Gemini 2.5 Pro)
- Total: ~16 calls (well within free tier: 15/min, 1500/day)

**✅ Checkpoint:** Optimization should complete in 5-10 minutes. Be patient!

---

### Step 8: Compare Before vs. After

Let's see what improved:

**Before GEPA (Original System Prompt):**
```yaml
system_prompt: |
  Expert AI Researcher
  
  Goal: Conduct thorough research on AI and technology topics, producing 
  comprehensive, well-sourced reports
  
  Reasoning Method: planning
  Steps:
    1. Break down research into subtasks using write_todos
    2. Search for authoritative sources
    3. Save findings to research_notes.md
    4. Synthesize information
    5. Write comprehensive report
```

**After GEPA (Optimized System Prompt):**
```yaml
system_prompt: |
  You are a meticulous AI research specialist with expertise in technical 
  analysis and comprehensive documentation.
  
  CORE OBJECTIVE: Deliver thorough, well-sourced research reports that provide 
  deep insights into AI technologies and frameworks, with clear structure and 
  authoritative citations.
  
  RESEARCH METHODOLOGY:
  
  1. ANALYZE the research question
     - Identify main topic and key subtopics
     - Determine scope and depth required
     - Note any specific focus areas
  
  2. PLAN systematically using write_todos
     - List 3-5 specific research tasks
     - Prioritize authoritative sources (documentation, papers, expert blogs)
     - Define deliverable structure
  
  3. RESEARCH comprehensively
     - Query multiple authoritative sources
     - Extract key facts, examples, and technical details
     - Document findings with source URLs
     - Save to research_notes.md with proper citations
  
  4. SYNTHESIZE insights
     - Identify patterns and common themes
     - Note areas of consensus vs. debate
     - Highlight practical implications and use cases
  
  5. COMPOSE structured report
     - Clear introduction establishing context
     - Well-organized sections with descriptive headings
     - Specific examples and code snippets where relevant
     - Minimum 5-7 authoritative citations
     - Balanced perspective on controversial topics
  
  QUALITY STANDARDS:
  - Technical accuracy over brevity
  - Specific examples beat generic descriptions
  - Always cite sources with [Title](URL) format
  - Academic tone, professional language
  - Comprehensive coverage (users expect depth)
```

**Key Improvements:**
- ✅ More specific instructions
- ✅ Better structure and organization
- ✅ Explicit quality standards
- ✅ Clearer methodology steps
- ✅ Emphasis on citations and sources

---

### Step 9: Test Optimized Agent

Run the agent with the optimized prompt:

```bash
super agent run research_agent_deepagents --goal "Compare LangGraph vs LangChain. Give me key differences."
```

**Expected Output (Better Quality):**
```
Response │ LangGraph and LangChain serve different but complementary purposes:
         │ 
         │ **LangChain** is a framework for building applications powered by LLMs, 
         │ providing components for prompts, chains, agents, and integrations. It 
         │ focuses on linear workflows and simple agent loops.
         │ 
         │ **LangGraph** extends LangChain by adding stateful, cyclic computation 
         │ graphs. Key differences:
         │ 
         │ 1. **Architecture**: LangChain uses linear chains; LangGraph uses graphs
         │ 2. **State Management**: LangChain is stateless; LangGraph maintains state
         │ 3. **Cycles**: LangChain is acyclic; LangGraph supports cycles/loops
         │ 4. **Complexity**: LangChain for simple workflows; LangGraph for complex
         │ 5. **Use Cases**: LangChain for Q&A; LangGraph for multi-step agents
         │ 
         │ Sources:
         │ [1] LangGraph Documentation: https://langchain-ai.github.io/langgraph/
         │ [2] LangChain Documentation: https://python.langchain.com/
```

**Notice the improvement:**
- ✅ Better structured response
- ✅ More comprehensive coverage
- ✅ Clear key differences listed
- ✅ Proper source citations

---

### Step 10: Evaluate Optimized Agent

Measure the improvement:

```bash
super agent evaluate research_agent_deepagents --load-optimized
```

**Expected Output:**
```
═══════════════════════════════════════════════════════════════════════════════
🧪 SuperOptiX BDD Spec Runner - Professional Agent Validation
═══════════════════════════════════════════════════════════════════════════════

Optimization: 🚀 Optimized Model

🧪 Executing BDD Specification Suite
────────────────────────────────────────────────────────────

🔍 Evaluating research_agent_deep_agents...

Testing 3 BDD scenarios:

✅ DeepAgents agent initialized with model: google-genai:gemini-2.5-flash
✅ Simple research query: PASS
✅ Technical comparison: PASS
✅ Complex research: PASS

============================================================
Overall: 3/3 PASS (100.0%)
============================================================

╭────────────────────── 🟢 Specification Results Summary ──────────────────────╮
│                                                                              │
│  📊 Total Specs:         3                🎯 Pass Rate:         100.0%       │
│  ✅ Passed:              3                                                   │
│  ❌ Failed:              0                                                   │
│  🏆 Quality Gate:        ✅ EXCELLENT                                        │
│                                                                              │
╰──────────────────────────────────────────────────────────────────────────────╯

═══════════════════════════════════════════════════════════════════════════════
       🏁 Specification execution completed - 100.0% pass rate (3/3 specs)       
═══════════════════════════════════════════════════════════════════════════════
```

**🎉 Amazing Results!**
- **Before:** Baseline performance
- **After:** Significantly improved performance
- **Improvement:** Noticeable enhancement (results vary by hardware and model)

**All scenarios now passing:**
- ✅ Simple research query
- ✅ Technical comparison
- ✅ Complex research

**✅ Checkpoint:** This demonstrates GEPA's power - it automatically improved the agent's performance significantly!

---

## 🗄️ Backend Configuration (DeepAgents 0.2.0)

### Understanding Backends

DeepAgents 0.2.0 introduces **pluggable backends** that control where agent files are stored. This is a game-changer for production agents!

### Backend Type 1: StateBackend (Default - Ephemeral)

**Use Case:** Temporary scratch space, single-conversation agents

**Configuration:**
```yaml
spec:
  backend:
    type: state  # Files exist only during current conversation
```

**Behavior:**
```bash
# First run
super agent run my_agent --goal "Save 'Hello' to /note.txt"
# Agent writes /note.txt

# New conversation (different thread)
super agent run my_agent --goal "Read /note.txt"
# ❌ File not found (ephemeral storage)
```

**Best For:**
- Quick Q&A
- Temporary calculations
- Draft generation
- Development/testing

---

### Backend Type 2: StoreBackend (Persistent Memory!)

**Use Case:** Chatbots that remember users, learning agents

**Configuration:**
```yaml
spec:
  backend:
    type: store  # ✨ Files persist FOREVER!
```

**Example: Persistent Chatbot**

```bash
# Pull demo
super agent pull chatbot_persistent
super agent compile chatbot_persistent --framework deepagents

# First conversation
super agent run chatbot_persistent --goal "Hi! My name is Alice and I love gardening."
```

**Agent's Actions:**
1. Creates `/user_profile.txt`:
   ```
   Name: Alice
   Interests: gardening
   First Contact: 2025-10-29
   ```
2. Saves to LangGraph store (persistent database)
3. Responds: "Nice to meet you, Alice! I see you love gardening..."

**Days Later, New Conversation:**
```bash
super agent run chatbot_persistent --goal "What's my name?"
```

**Agent's Actions:**
1. **Reads `/user_profile.txt`** (still there! ✅)
2. Finds: "Name: Alice"
3. Responds: **"Your name is Alice!"**

**Weeks Later:**
```bash
super agent run chatbot_persistent --goal "What hobbies do I have?"
```

**Response:** "You love gardening!" ✅

**🎉 The agent remembers across ALL conversations!**

**Best For:**
- Customer support chatbots
- Personal assistants
- Learning agents
- Any agent that needs memory

---

### Backend Type 3: FilesystemBackend (Real Files!)

**Use Case:** Code analysis, file editing, project work

**Configuration:**
```yaml
spec:
  backend:
    type: filesystem
    root_dir: /Users/local/my_project  # Path to your project
```

**Example: Code Review Agent**

```bash
# Setup: Create a sample project
mkdir -p /tmp/demo_code
cat > /tmp/demo_code/app.py << 'EOF'
def login(username, password):
    query = f"SELECT * FROM users WHERE username='{username}'"  # SQL injection!
    return db.execute(query)
EOF

# Pull code reviewer
super agent pull code_reviewer

# Edit playbook to set root_dir:
# backend:
#   type: filesystem
#   root_dir: /tmp/demo_code

# Compile and run
super agent compile code_reviewer --framework deepagents
super agent run code_reviewer --goal "Review app.py for security issues"
```

**Agent's Actions:**
1. **Reads REAL file:** `/tmp/demo_code/app.py`
2. Analyzes code
3. Finds: SQL injection vulnerability (line 2)
4. **Writes REAL report:** `/tmp/demo_code/security_report.md`

**Verify:**
```bash
cat /tmp/demo_code/security_report.md
```

**You'll see a complete security report written to an actual file on your disk!**

**Best For:**
- Code review agents
- Documentation generators
- File refactoring tools
- Project analysis

**⚠️ Security:** Agent can modify actual files! Use with trusted agents and limited `root_dir` scope.

---

### Backend Type 4: CompositeBackend (Hybrid - Production!)

**Use Case:** Production agents with complex storage needs

**Configuration:**
```yaml
spec:
  backend:
    type: composite
    default: state                # Scratch space (fast)
    routes:
      /memories/: store          # Research findings (persistent)
      /papers/: filesystem       # Academic papers (real files)
      /cache/: state             # Search results (temporary)
    root_dir: /Users/local/research
```

**How It Works:**

```
┌──────────────────────────────────────────┐
│         Agent Filesystem                 │
├──────────────────────────────────────────┤
│                                          │
│  /memories/                              │
│  ├─ research_notes.txt → Database ✅     │
│  ├─ findings.txt → Database ✅           │
│  └─ index.txt → Database ✅              │
│      (PERSISTS FOREVER)                  │
│                                          │
│  /papers/                                │
│  ├─ transformer.pdf → Real File ✅       │
│  ├─ bert.pdf → Real File ✅              │
│  └─ gpt3.pdf → Real File ✅              │
│      (ACTUAL FILES on your disk)         │
│                                          │
│  /cache/                                 │
│  ├─ search.txt → Ephemeral ❌            │
│  └─ temp.txt → Ephemeral ❌              │
│      (CLEARED each conversation)         │
│                                          │
│  / (root)                                │
│  ├─ draft.txt → Ephemeral ❌             │
│  └─ workspace.txt → Ephemeral ❌         │
│      (SCRATCH SPACE)                     │
│                                          │
└──────────────────────────────────────────┘
```

**Example: Advanced Researcher**

```bash
# Pull demo
super agent pull researcher_hybrid

# Edit playbook to set your root_dir
super agent compile researcher_hybrid --framework deepagents

# First research session
super agent run researcher_hybrid --goal "Research transformers and save important findings to /memories/"
```

**Agent's Workflow:**
1. Checks `/memories/research_index.txt` (empty - first time)
2. Searches for transformer information
3. Saves temp results to `/cache/search_results.txt` (fast ephemeral storage)
4. Reads `/papers/attention.pdf` if available (real file)
5. **Writes to `/memories/transformer_research.txt`** (PERSISTS in database!)
6. Updates `/memories/research_index.txt`

**Week Later:**
```bash
super agent run researcher_hybrid --goal "What did I research about transformers?"
```

**Agent's Workflow:**
1. **Reads `/memories/research_index.txt`** (STILL THERE from last week!)
2. Finds reference to transformer_research.txt
3. **Reads `/memories/transformer_research.txt`** (PERSISTS!)
4. Responds: "Based on your research from October 29th, transformers are..."

**🎉 Perfect hybrid strategy:**
- Fast temporary storage (`/cache/`, `/`)
- Persistent memory (`/memories/`)
- Real file access (`/papers/`)

**Best For:**
- Development assistants
- Complex research agents
- Multi-domain agents
- Production systems

---

## 📊 Complete Workflow Summary

### Commands Reference

```bash
# 1. Initialize
super init my_project && cd my_project

# 2. Pull agent
super agent pull research_agent_deepagents

# 3. Compile
super agent compile research_agent_deepagents --framework deepagents

# 4. Run
super agent run research_agent_deepagents --goal "Your query here"

# 5. Evaluate (baseline)
super agent evaluate research_agent_deepagents

# 6. Optimize (uses your Gemini key from fish config)
super agent optimize research_agent_deepagents \
  --framework deepagents \
  --auto medium \
  --reflection-lm google-genai:gemini-2.5-pro

# 7. Evaluate (optimized)
super agent evaluate research_agent_deepagents --load-optimized

# 8. Run optimized
super agent run research_agent_deepagents --goal "Complex query here"
```

### Expected Results

| Step | Baseline | After GEPA |
|------|----------|------------|
| **Simple queries** | ✅ Good | ✅ Excellent |
| **Technical comparisons** | ❌ Poor | ✅ Good |
| **Complex research** | ❌ Poor | ✅ Good |
| **Overall** | Baseline | Significantly Improved (results vary by hardware/model) |

### API Costs

| Operation | Calls | Model | Cost |
|-----------|-------|-------|------|
| Run (x1) | 1 | Gemini Flash | $0.00 |
| Evaluate (x1) | 3 | Gemini Flash | $0.00 |
| Optimize (medium) | ~30 | Flash + Pro | $0.00 |
| **Total** | **~35** | **FREE tier** | **$0.00** |

**You can run ~40 optimizations per day completely FREE!**

---

## 🎓 Advanced Examples

### Example 1: Building a Persistent Memory Chatbot

**Full Playbook:**
```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: Personal Assistant with Memory
  id: my_assistant
spec:
  target_framework: deepagents
  
  language_model:
    provider: google-genai
    model: gemini-2.5-flash
    temperature: 0.7
  
  # Enable persistent memory
  backend:
    type: store
  
  input_fields:
    - name: query
      type: str
  
  output_fields:
    - name: response
      type: str
  
  persona:
    system_prompt: |
      You are a personal AI assistant with PERSISTENT LONG-TERM MEMORY.
      
      MEMORY FILES (These persist forever across ALL conversations):
      
      📝 /user_profile.txt
      - User's name, preferences, interests, background
      - Update whenever you learn something new
      
      📚 /conversation_topics.txt
      - Key topics discussed in past conversations
      - Add new topics as you discuss them
      
      ✅ /reminders.txt
      - User's reminders, to-dos, future plans
      - Update when user mentions tasks
      
      WORKFLOW (Follow strictly):
      
      1. BEFORE responding:
         - Read /user_profile.txt
         - Read /conversation_topics.txt
         - Check /reminders.txt
      
      2. PERSONALIZE response:
         - Use their name
         - Reference previous conversations
         - Build on existing knowledge
      
      3. AFTER responding:
         - Update /user_profile.txt if you learned something
         - Add to /conversation_topics.txt if new topic
         - Update /reminders.txt if tasks mentioned
      
      Remember: These files SURVIVE FOREVER. Build a relationship!
  
  feature_specifications:
    scenarios:
      - name: Remember name
        input:
          query: "My name is Sarah"
        expected_output:
          response: "Nice to meet you"
          expected_keywords:
            - Sarah
      
      - name: Recall name
        input:
          query: "What's my name?"
        expected_output:
          response: "Sarah"
          expected_keywords:
            - Sarah
```

**Usage:**
```bash
# Save the playbook above, then:
super agent compile my_assistant --framework deepagents

# First conversation
super agent run my_assistant --goal "Hi! I'm Sarah and I love gardening."
# Response: "Nice to meet you, Sarah! I see you love gardening..."

# Hours later...
super agent run my_assistant --goal "What's my name?"
# Response: "Your name is Sarah!"

# Days later...
super agent run my_assistant --goal "What do I like to do?"
# Response: "You love gardening!"

# Weeks later...
super agent run my_assistant --goal "Remind me what we've talked about"
# Response: "We've discussed your interest in gardening..."
```

---

### Example 2: Code Review Agent with Real Files

**Setup Test Project:**
```bash
mkdir -p /tmp/my_app/src
cat > /tmp/my_app/src/auth.py << 'EOF'
def login(username, password):
    # TODO: Add input validation
    query = f"SELECT * FROM users WHERE username='{username}' AND password='{password}'"
    return db.execute(query)

def register(username, password, email):
    # Missing email validation
    user = User(username, password, email)
    db.save(user)
    return user
EOF
```

**Playbook:**
```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: Code Reviewer
  id: code_reviewer
spec:
  target_framework: deepagents
  
  language_model:
    provider: google-genai
    model: gemini-2.5-pro  # Pro for better code analysis
    temperature: 0.3
  
  # Access real project files
  backend:
    type: filesystem
    root_dir: /tmp/my_app
  
  input_fields:
    - name: query
      type: str
  
  output_fields:
    - name: report
      type: str
  
  persona:
    system_prompt: |
      You are a senior code reviewer with DIRECT FILESYSTEM ACCESS.
      
      Available tools:
      - ls /src/ - List source files
      - read_file /src/auth.py - Read code
      - write_file /review.md - Write reports
      - grep_search "TODO" /src/ - Find patterns
      
      SECURITY CHECKLIST:
      - SQL injection
      - XSS/CSRF risks
      - Input validation
      - Authentication flaws
      - Hardcoded secrets
      
      WORKFLOW:
      1. List files with ls
      2. Read code with read_file
      3. Analyze for security issues
      4. Write detailed report to /security_report.md
      
      Include:
      - File path and line numbers
      - Severity (Critical/High/Medium/Low)
      - Code examples
      - Recommended fixes
```

**Usage:**
```bash
super agent compile code_reviewer --framework deepagents

# Review specific file
super agent run code_reviewer --goal "Review src/auth.py for security vulnerabilities"
```

**Expected Response:**
```
Found 2 CRITICAL security issues in /src/auth.py:

1. SQL INJECTION - CRITICAL (Line 3)
   File: /src/auth.py
   
   Vulnerable code:
   query = f"SELECT * FROM users WHERE username='{username}' ..."
   
   Issue: Unsanitized user input directly in SQL query allows SQL injection.
   
   Fix: Use parameterized queries:
   query = "SELECT * FROM users WHERE username=? AND password=?"
   result = db.execute(query, (username, password))

2. MISSING INPUT VALIDATION - HIGH (Line 7)
   File: /src/auth.py
   
   Issue: Email address not validated before saving.
   
   Fix: Add email validation
```

**Generate Report:**
```bash
super agent run code_reviewer --goal "Analyze all Python files and write a complete security report to /security_report.md"
```

**Verify:**
```bash
# The report is a REAL file!
cat /tmp/my_app/security_report.md
```

---

### Example 3: Hybrid Research Agent (Production-Ready)

**Setup:**
```bash
mkdir -p /tmp/research_workspace/papers
echo "Sample academic paper about AI agents..." > /tmp/research_workspace/papers/agents_paper.txt
```

**Playbook:**
```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: Advanced Researcher
  id: researcher_hybrid
spec:
  target_framework: deepagents
  
  language_model:
    provider: google-genai
    model: gemini-2.5-flash
  
  # Hybrid storage strategy (PRODUCTION-READY)
  backend:
    type: composite
    default: state                # Fast scratch space
    routes:
      /memories/: store          # Research findings (persistent forever)
      /papers/: filesystem       # Academic papers (real files)
      /cache/: state             # Search results (temporary)
    root_dir: /tmp/research_workspace
  
  persona:
    system_prompt: |
      You are an advanced research agent with HYBRID STORAGE.
      
      STORAGE ARCHITECTURE:
      
      📚 /memories/ → Persistent Database
      - Research findings that should last forever
      - Literature reviews and summaries
      - Key insights and discoveries
      - Survives: ALL conversations, forever
      
      📂 /papers/ → Real Filesystem  
      - Actual PDF papers in /tmp/research_workspace/papers/
      - Academic publications
      - Technical documentation
      - Survives: Forever (real files on disk)
      
      💾 /cache/ → Temporary State
      - Internet search results  
      - Intermediate calculations
      - Survives: Current conversation only
      
      🗂️ / → Scratch Space
      - Current work in progress
      - Survives: Current conversation only
      
      RESEARCH WORKFLOW:
      
      1. CHECK PRIOR RESEARCH
         read_file /memories/research_index.txt
         → See if topic was researched before
      
      2. SEARCH & CACHE
         [Conduct internet search]
         write_file /cache/search_results.txt [results]
         → Store temporarily for this session
      
      3. ACCESS PAPERS
         ls /papers/
         read_file /papers/relevant_paper.pdf
         → Read actual academic papers
      
      4. SAVE FINDINGS
         write_file /memories/[topic]_research.txt [summary]
         edit_file /memories/research_index.txt
           Add: "- [topic]: See /memories/[topic]_research.txt"
         → Persist important findings
      
      5. RESPOND
         Return comprehensive answer with sources
```

**Usage - First Session:**
```bash
super agent compile researcher_hybrid --framework deepagents

super agent run researcher_hybrid --goal "Research transformer architectures. Save key findings to /memories/."
```

**Agent's Actions:**
1. Checks `/memories/research_index.txt` (empty - first time)
2. Searches for information
3. Saves to `/cache/search_results.txt` (temporary)
4. Checks `/papers/` for relevant PDFs
5. **Writes `/memories/transformer_research.txt`** (PERSISTS!)
6. Updates `/memories/research_index.txt`

**File Locations:**
- `/memories/transformer_research.txt` → LangGraph store (database)
- `/papers/transformer.pdf` → `/tmp/research_workspace/papers/transformer.pdf` (real file)
- `/cache/search_results.txt` → LangGraph state (ephemeral)

**Usage - Week Later:**
```bash
super agent run researcher_hybrid --goal "What did I learn about transformers?"
```

**Agent's Actions:**
1. **Reads `/memories/research_index.txt`** (STILL THERE!)
2. Finds: "transformers: See /memories/transformer_research.txt"
3. **Reads `/memories/transformer_research.txt`** (PERSISTS!)
4. Responds with full research summary from last week

**🎉 Perfect for production:** Fast temporary storage + persistent memory + real file access!

---

## 🐛 Troubleshooting

### Issue 1: "API key not set"

**Error:**
```
❌ GOOGLE_API_KEY not set
```

**Solution:**
```bash
# Check if set
echo $GOOGLE_API_KEY

# If empty, set it
export GOOGLE_API_KEY="AIzaSy-your-actual-key"

# For fish shell (permanent)
set -x GOOGLE_API_KEY "AIzaSy-your-key"
echo "set -x GOOGLE_API_KEY \"AIzaSy-your-key\"" >> ~/.config/fish/config.fish
```

---

### Issue 2: "Failed to initialize DeepAgents"

**Error:**
```
⚠️  Failed to initialize DeepAgents: No module named 'langchain_google_genai'
```

**Solution:**
```bash
pip install langchain-google-genai
```

---

### Issue 3: "Rate limit exceeded"

**Error:**
```
google.api_core.exceptions.ResourceExhausted: 429 Quota exceeded
```

**Solution:**
```bash
# Use lighter optimization (fewer API calls)
super agent optimize my_agent --auto light --reflection-lm google-genai:gemini-2.5-flash

# Or wait 1 minute (free tier: 15 requests/minute)
```

---

### Issue 4: "Pipeline not found"

**Error:**
```
❌ Pipeline not found for agent 'my_agent'
```

**Solution:**
```bash
# Make sure to specify framework when optimizing non-DSPy agents
super agent optimize my_agent --framework deepagents --auto medium --reflection-lm google-genai:gemini-2.5-pro

# Recompile if needed
super agent compile my_agent --framework deepagents
```

---

### Issue 5: Files not persisting

**Problem:** Agent doesn't remember things across conversations

**Check backend type:**
```yaml
# Wrong: Ephemeral
backend:
  type: state

# Correct: Persistent
backend:
  type: store
```

**Fix:**
1. Edit playbook
2. Change `type: state` to `type: store`
3. Recompile: `super agent compile my_agent --framework deepagents`
4. Test again

---

### Issue 6: Can't access local files

**Problem:** Agent can't read your project files

**Check configuration:**
```yaml
backend:
  type: filesystem
  root_dir: /Users/local/my_project  # Must be set!
```

**Verify path exists:**
```bash
ls /Users/local/my_project
# Should show your project files
```

---

## 🔒 Security Best Practices

### FilesystemBackend Security

When using `FilesystemBackend`, the agent can read and **modify** actual files!

**✅ Safe Configuration:**
```yaml
backend:
  type: filesystem
  root_dir: /tmp/agent_sandbox  # Isolated directory
```

**❌ Unsafe Configuration:**
```yaml
backend:
  type: filesystem
  root_dir: /  # CAN ACCESS ENTIRE SYSTEM!
```

### Recommendations

1. **Limit Scope:**
   ```yaml
   # Good: Specific project directory
   root_dir: /Users/local/my_project/src
   
   # Bad: System root
   root_dir: /
   ```

2. **Use Read-Only Patterns:**
   ```yaml
   persona:
     system_prompt: |
       You can READ files from /project/.
       Only WRITE to /reports/ directory.
       Never DELETE files.
   ```

3. **Validate Changes:**
   Add to system prompt:
   ```yaml
   Before modifying any file:
   1. Show the user the planned changes
   2. Explain why the changes are needed
   3. Only proceed after confirmation
   ```

4. **Use Composite for Safety:**
   ```yaml
   backend:
     type: composite
     default: state
     routes:
       /project/: filesystem  # Real files (read-only usage)
       /output/: state        # Reports (safe to write)
   ```

---

## 📈 Performance Optimization Tips

### 1. Choose Right Model for Each Task

```yaml
# For agent execution (runs many times)
language_model:
  model: gemini-2.5-flash  # Fast and cheap

# For GEPA reflection (runs fewer times)
optimization:
  optimizer:
    params:
      reflection_lm: gemini-2.5-pro  # Better reasoning
```

### 2. Optimize BDD Scenarios

Start with 3-5 good scenarios:
```yaml
feature_specifications:
  scenarios:
    - name: Simple case
      input:
        query: "Basic question"
      expected_output:
        expected_keywords: [keyword1, keyword2]
    
    - name: Medium complexity
      ...
    
    - name: Complex case
      ...
```

### 3. Use Appropriate GEPA Budget

```bash
# Quick test (5 min, ~15 API calls)
super agent optimize my_agent --auto light

# Balanced (10 min, ~30 API calls)
super agent optimize my_agent --auto medium

# Best results (20 min, ~60 API calls)
super agent optimize my_agent --auto heavy
```

### 4. Optimize Backend Strategy

```yaml
# Fast but ephemeral
backend:
  type: state

# Persistent but slower
backend:
  type: store

# Best of both worlds
backend:
  type: composite
  default: state        # Fast default
  routes:
    /memories/: store  # Only persist what's important
```

---

## 🚀 Production Deployment

### Production-Ready Playbook Template

```yaml
apiVersion: agent/v1
kind: AgentSpec
metadata:
  name: Production Agent
  version: 1.0.0
spec:
  target_framework: deepagents
  
  # Production model
  language_model:
    provider: google-genai
    model: gemini-2.5-flash
    temperature: 0.5  # Lower for more consistent responses
    max_tokens: 8192
  
  # Production backend (hybrid)
  backend:
    type: composite
    default: state
    routes:
      /memories/: store          # User data, persistent
      /workspace/: filesystem    # Project files
      /cache/: state             # Temporary
    root_dir: /var/app/workspace
  
  # Comprehensive BDD scenarios
  feature_specifications:
    scenarios:
      - name: Critical path 1
        ...
      - name: Critical path 2
        ...
      - name: Edge case 1
        ...
      # 10-15 scenarios recommended for production
  
  # GEPA optimization (run during CI/CD)
  optimization:
    optimizer:
      name: GEPA
      params:
        metric: response_accuracy
        auto: heavy  # Best for production
        reflection_lm: google-genai:gemini-2.5-pro
        max_full_evals: 10
    metric_threshold: 0.95  # 95% minimum for production
```

### Production Deployment Steps

```bash
# 1. Develop and test locally
super agent compile production_agent --framework deepagents
super agent evaluate production_agent

# 2. Optimize for production
super agent optimize production_agent \
  --framework deepagents \
  --auto heavy \
  --reflection-lm google-genai:gemini-2.5-pro

# 3. Validate optimized version
super agent evaluate production_agent --load-optimized
# Check performance metrics (varies by hardware/model)

# 4. Test with real data
super agent run production_agent --goal "Production query"

# 5. Deploy
# Copy optimized prompt to production config
# Set up monitoring and logging
# Deploy with proper API key management
```

---

## 📊 Performance Benchmarks

### GEPA Optimization Results

| Budget | Time | API Calls | Typical Improvement | Cost (Gemini) |
|--------|------|-----------|---------------------|---------------|
| **light** | 5 min | ~15 | +10-20% | $0.00 |
| **medium** | 10 min | ~30 | +20-30% | $0.00 |
| **heavy** | 20 min | ~60 | +30-50% | $0.00 |

### Backend Performance

| Backend | Read Speed | Write Speed | Persistence | Best For |
|---------|------------|-------------|-------------|----------|
| **state** | ⚡⚡⚡ | ⚡⚡⚡ | ❌ | Speed |
| **store** | ⚡⚡ | ⚡⚡ | ✅ | Memory |
| **filesystem** | ⚡⚡ | ⚡⚡ | ✅ | Real files |
| **composite** | ⚡⚡ | ⚡⚡ | ✅ | Production |

### Model Performance (Gemini 2.5)

| Model | Speed | Quality | Context | Cost |
|-------|-------|---------|---------|------|
| **Flash** | ⚡⚡⚡ 1-2s | ⭐⭐⭐⭐ | 1M tokens | FREE |
| **Pro** | ⚡⚡ 2-4s | ⭐⭐⭐⭐⭐ | 2M tokens | FREE |

---

## 🎓 Learning Path

### Beginner (Day 1)
1. ✅ Complete Steps 1-5 (Pull and run agent)
2. ✅ Try different queries
3. ✅ Understand BDD scenarios

### Intermediate (Day 2-3)
4. ✅ Complete Steps 6-10 (Evaluation and optimization)
5. ✅ Try persistent chatbot example
6. ✅ Experiment with backends

### Advanced (Week 1)
7. ✅ Build code review agent
8. ✅ Create hybrid researcher
9. ✅ Design custom backend strategies

### Expert (Week 2+)
10. ✅ Build production-ready agents
11. ✅ Optimize for your use case
12. ✅ Deploy to production

---

## 📚 Additional Resources

### Official Documentation

- [DeepAgents Integration Guide](deepagents-integration.md) - Complete guide
- [Backend Configuration Reference](deepagents-backends.md) - All backend types
- [Backend Tutorial](deepagents-backends-tutorial.md) - 6 hands-on tutorials

### Configuration Guides

- [Gemini Configuration Guide](../../GEMINI_CONFIGURATION_GUIDE.md) - Model setup
- [Quick Reference](../../DEEPAGENTS_QUICK_REFERENCE.md) - Command cheat sheet

### External Resources

- [DeepAgents 0.2.0 Announcement](https://blog.langchain.com/doubling-down-on-deepagents/) - LangChain blog
- [Google AI Studio](https://aistudio.google.com/) - Get FREE Gemini API key
- [Gemini Pricing](https://ai.google.dev/pricing) - Free tier details

---

## 🎯 Quick Command Reference

### Essential Commands

```bash
# Initialize
super init my_project && cd my_project

# Pull agent
super agent pull research_agent_deepagents

# Compile
super agent compile research_agent_deepagents --framework deepagents

# Run
super agent run research_agent_deepagents --goal "Your query"

# Evaluate
super agent evaluate research_agent_deepagents

# Optimize
super agent optimize research_agent_deepagents \
  --framework deepagents \
  --auto medium \
  --reflection-lm google-genai:gemini-2.5-pro

# Test optimized
super agent evaluate research_agent_deepagents --load-optimized
```

### All Demo Agents

```bash
# Basic research (StateBackend)
super agent pull research_agent_deepagents

# Persistent chatbot (StoreBackend)
super agent pull chatbot_persistent

# Code reviewer (FilesystemBackend)
super agent pull code_reviewer

# Hybrid researcher (CompositeBackend)
super agent pull researcher_hybrid
```

---

## 🎉 Success Criteria

By the end of this tutorial, you should be able to:

- ✅ Initialize a SuperOptiX project
- ✅ Pull and compile DeepAgents agents
- ✅ Run agents with real Gemini API calls
- ✅ Evaluate agent performance with BDD scenarios
- ✅ Optimize agents with GEPA (achieving 2-3x improvement)
- ✅ Configure all 4 backend types
- ✅ Build persistent chatbots
- ✅ Create code review agents
- ✅ Design hybrid storage strategies
- ✅ Deploy production-ready agents

**If you've done all this:** 🎊 **Congratulations! You're a DeepAgents expert!**

---

## 💡 Next Steps

### Immediate
1. Try all 4 demo agents
2. Experiment with different backends
3. Build your first custom agent

### This Week
4. Read the complete [Backend Reference](deepagents-backends.md)
5. Follow the [Backend Tutorial](deepagents-backends-tutorial.md)
6. Optimize your agents with GEPA

### This Month
7. Build production-ready agents
8. Deploy to real users
9. Monitor and iterate

---

## 🤝 Community & Support

### Get Help

- 📖 **Documentation:** [https://superagenticai.github.io/superoptix-ai/](https://superagenticai.github.io/superoptix-ai/)
- 📧 **Email:** hello@super-agentic.ai
- 🌐 **Website:** [https://superoptix.ai](https://superoptix.ai)

### Share Your Success

Built something cool? Share it with the community!

- 🐦 **Tag us on Twitter/X:** [@SuperagenticAI](https://twitter.com/SuperagenticAI)
- 📧 **Email us your success story:** hello@super-agentic.ai

---

**🎊 You're ready to build amazing DeepAgents! Happy coding!** 🚀

