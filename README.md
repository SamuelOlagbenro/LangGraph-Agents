<div align="center">

# 🧠 LangGraph Agents Labs: From Stateful Workflows to ReAct

**A hands-on learning path for building intelligent, stateful AI agents with LangGraph**

[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![LangGraph](https://img.shields.io/badge/langgraph-0.3+-green.svg)](https://github.com/langchain-ai/langgraph)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

*Build agents that reason, reflect, use tools, and improve themselves.*

[Getting Started](#-getting-started) •
[Learning Path](#-learning-path) •
[Notebooks](#-notebooks) •
[Concepts](#-core-concepts) •
[Contributing](#-contributing)

</div>

---

## 📖 Overview

This repository contains **four progressive Jupyter notebooks** that teach you how to build sophisticated AI agents using **LangGraph**, a framework for creating stateful, multi-step workflows powered by LLMs.

You'll start with the fundamentals of state-based graphs and progress to building **ReAct agents** that can reason step-by-step, use external tools, and self-improve through reflection loops.

By the end, you'll understand:

- ✅ How to model agent behavior as a **state graph**
- ✅ The difference between **linear, cyclic, and conditional workflows**
- ✅ How to implement **Reflection** for self-critique and refinement
- ✅ How to build **Reflexion** agents that research with external tools
- ✅ The **ReAct** (Reasoning + Acting) pattern for tool-using agents

---

## 🎯 Learning Path

The notebooks are designed to be completed in order. Each builds on the previous one:

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   1. LangGraph 101          2. Reflection Agent                 │
│   ─────────────────          ────────────────────               │
│   • States                   • Self-critique loops              │
│   • Nodes & Edges            • MessageGraph                     │
│   • Conditional routing      • Iterative refinement             │
│                                                                 │
│              │                          │                       │
│              ▼                          ▼                       │
│                                                                 │
│   3. Reflexion + Tools       4. ReAct Agent                     │
│   ───────────────────        ──────────────                     │
│   • External search (Tavily) • Reasoning + Acting loop          │
│   • Structured critiques     • Multi-tool orchestration         │
│   • Evidence-based answers   • Autonomous decision-making       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📓 Notebooks

| # | Notebook | Concepts | Time | Level |
|---|----------|----------|------|-------|
| 1 | [LangGraph 101: Building Stateful AI Workflows](notebooks/Lab-LangGraph101BuildingStatefulAIWorkflows.ipynb) | States, Nodes, Edges, Conditional Edges | ~60 min | 🟢 Beginner |
| 2 | [Building a Reflection Agent](notebooks/02_reflection_agent.ipynb) | Reflection pattern, MessageGraph, self-critique | ~45 min | 🟡 Intermediate |
| 3 | [Reflexion Agent with External Knowledge](notebooks/03_reflexion_external_knowledge.ipynb) | Tool integration, structured critique, Tavily search | ~30 min | 🟡 Intermediate |
| 4 | [ReAct: Reasoning + Acting Agents](notebooks/04_react_agent.ipynb) | ReAct loop, tool registry, agent state | ~90 min | 🔴 Advanced |

### What You'll Build

<details>
<summary><b>1. Authentication Workflow</b> — LangGraph 101</summary>

A stateful login flow that validates credentials, branches on success/failure, and loops back on error.

```python
workflow = StateGraph(AuthState)
workflow.add_node("InputNode", input_node)
workflow.add_node("ValidateCredential", validate_credentials_node)
workflow.add_conditional_edges("ValidateCredential", router, {...})
```
</details>

<details>
<summary><b>2. LinkedIn Post Generator</b> — Reflection Agent</summary>

An agent that drafts a LinkedIn post, critiques its own work, and refines it through multiple iterations.

```python
graph.add_node("generate", generation_node)
graph.add_node("reflect", reflection_node)
graph.add_conditional_edges("generate", should_continue)
```
</details>

<details>
<summary><b>3. Nutrition Research Agent</b> — Reflexion with Tools</summary>

A "deep research" agent that drafts answers, identifies gaps, searches the web, and revises with citations.

```python
graph.add_node("respond", initial_chain)
graph.add_node("execute_tools", execute_tools)
graph.add_node("revisor", revisor_chain)
graph.add_edge("execute_tools", "revisor")
```
</details>

<details>
<summary><b>4. Weather + Clothing Agent</b> — ReAct</summary>

An agent that autonomously decides which tools to call to answer compound questions like *"What's the weather in Zurich, and what should I wear?"*

```python
workflow.add_node("agent", call_model)
workflow.add_node("tools", tool_node)
workflow.add_conditional_edges("agent", should_continue, {...})
```
</details>

---

## 🧩 Core Concepts

### What is LangGraph?

LangGraph is a library for building **stateful, multi-step AI applications** using graphs. Unlike simple prompt chains, LangGraph lets you:

- Define **state** that persists across steps
- Create **nodes** as units of work
- Connect nodes with **edges** (including loops and conditionals)
- Build **cyclic workflows** that iterate and refine

### The Four Key Components

| Component | Role | Example |
|-----------|------|---------|
| **State** | Holds data flowing through the graph | `{"messages": [...], "answer": "..."}` |
| **Node** | A function that processes state | `def generate(state): ...` |
| **Edge** | Connects nodes in sequence | `graph.add_edge("a", "b")` |
| **Conditional Edge** | Routes based on state | `graph.add_conditional_edges("a", router)` |

### Agent Patterns Covered

- **Linear Workflow** — Tasks execute in a fixed order
- **Conditional Workflow** — Branching based on state
- **Reflection** — Self-critique and refinement loop
- **Reflexion** — Reflection + external tool use
- **ReAct** — Interleaved reasoning and acting

---

## 🚀 Getting Started

### Prerequisites

- Python 3.12+
- Basic familiarity with Python and LLMs
- (Optional) API keys if running locally:
  - OpenAI API key
  - IBM Watsonx API key
  - Tavily API key (for labs 3 & 4)

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/langgraph-agents-labs.git
cd langgraph-agents-labs

# Create a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Running the Notebooks

```bash
jupyter notebook notebooks/
```

Or use VS Code with the Jupyter extension.

### Environment Variables (for local runs)

Create a `.env` file in the root directory:

```bash
OPENAI_API_KEY=your_openai_key
WATSONX_API_KEY=your_watsonx_key
WATSONX_PROJECT_ID=your_project_id
TAVILY_API_KEY=your_tavily_key
```

---

## 📚 Documentation

Detailed guides for each concept are available in the [`docs/`](docs/) folder:

- [Getting Started](docs/01-getting-started.md)
- [Core Concepts](docs/02-core-concepts.md)
- [The Reflection Pattern](docs/03-reflection-pattern.md)
- [Reflexion with External Tools](docs/04-reflexion-with-tools.md)
- [The ReAct Pattern](docs/05-react-pattern.md)

---

## 🛠️ Standalone Examples

If you prefer runnable Python scripts over notebooks, check out the [`examples/`](examples/) directory:

```bash
python examples/auth_workflow.py
python examples/linkedin_post_generator.py
python examples/nutrition_research_agent.py
python examples/weather_clothing_agent.py
```

---

## 🤝 Contributing

Contributions are welcome! Whether it's:
- 🐛 Bug fixes
- 📝 Documentation improvements
- ✨ New example agents
- 🎨 Better diagrams

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- [LangChain](https://www.langchain.com/) and [LangGraph](https://github.com/langchain-ai/langgraph) teams
- IBM Skills Network for the original lab materials
- The open-source AI agent community

---

<div align="center">

**⭐ If this repo helped you learn LangGraph, please give it a star! ⭐**

</div>
