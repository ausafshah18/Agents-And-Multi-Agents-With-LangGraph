# 🚀 Production Agentic AI with LangGraph

[![Python 3.12+](https://img.shields.io/badge/Python-3.12%2B-blue.svg)](https://www.python.org/)
[![LangGraph](https://img.shields.io/badge/Orchestration-LangGraph-orange.svg)](https://github.com/langchain-ai/langgraph)
[![LangChain](https://img.shields.io/badge/Framework-LangChain-green.svg)](https://github.com/langchain-ai/langchain)
[![Groq Fast Inference](https://img.shields.io/badge/Inference-Groq-purple.svg)](https://groq.com/)
[![Observability-LangSmith](https://img.shields.io/badge/Observability-LangSmith-blueviolet.svg)](https://smith.langchain.com/)

A hands-on, production-oriented repository showcasing **Agentic AI Design Patterns** built using **LangGraph**, **LangChain**, and high-speed **Groq** LLMs (`llama-3.3-70b-versatile`, `openai/gpt-oss-120b`). This repository walks through foundational ReAct agents, state persistence, modern Human-in-the-Loop (HITL) workflows, enterprise observability with LangSmith, and hierarchical Multi-Agent supervisor architectures.

---

## 📁 Repository Modules & Functionality

Below is an overview of the modules implemented in this repository, including a concise summary of each folder:

| Module | 1–2 Line Summary | Documentation |
| :--- | :--- | :--- |
| [**`1-BasicChatBot`**](file:///1-BasicChatBot) | Builds stateful ReAct agents with Tavily web search and math tools, featuring thread-based `MemorySaver` persistence and multi-mode streaming. | [View README](file:///1-BasicChatBot/README.md) |
| [**`2-HumanAssistance`**](file:///2-HumanAssistance) | Implements Human-in-the-Loop (HITL) workflows using LangGraph `interrupt` and `Command(resume=...)` to pause graphs for human feedback and resume safely. | [View README](file:///2-HumanAssistance/README.md) |
| [**`3-Debugging`**](file:///3-Debugging) | Provides production observability and visual debugging by integrating LangSmith tracing and configuring LangGraph Studio via `langgraph.json`. | [View README](file:///3-Debugging/README.md) |
| [**`Agents`**](file:///Agents) | Demonstrates collaborative multi-agent architectures, including a sequential research-to-writing pipeline and an autonomous supervisor-worker system. | [View README](file:///Agents/README.md) |

---

## 🧠 Architectural Patterns Covered

### 1. Stateful ReAct Agent with Memory & Streaming (`1-BasicChatBot`)
- **StateGraph & Reducers**: Custom `TypedDict` state managed via `Annotated[list, add_messages]`.
- **Dynamic Tool Calling**: Seamless integration with Tavily Web Search and custom Python tools using `ToolNode` and `tools_condition`.
- **Session Checkpointing**: Multi-turn conversational memory isolated per session using `MemorySaver` and `thread_id`.
- **Streaming Modes**: Real-time token and state update streaming via `.stream(..., stream_mode="values" | "updates")` and asynchronous `.astream_events(...)`.

### 2. Modern Human-in-the-Loop (`2-HumanAssistance`)
- **Active Pausing with `interrupt()`**: Agents can escalate ambiguous tasks or sensitive actions directly to human experts.
- **State Preservation**: Checkpointer captures paused state at the tool execution boundary.
- **Resumption with `Command(resume=...)`**: Injects human review data back into the workflow to continue graph execution without duplicate tool runs.

### 3. Observability & Visual Studio (`3-Debugging`)
- **LangSmith Telemetry**: Full execution graphs, token accounting, latency metrics, and error stack traces.
- **LangGraph Studio**: Exported `agent.py:tool_agent` configured via `langgraph.json` for interactive visual graph execution and time-travel debugging.
- **Mermaid Renderers**: Graph inspection and diagram rendering directly inside Jupyter environments.

### 4. Multi-Agent Systems (`Agents`)
- **Sequential Pipeline**: Linear handoff between an autonomous ReAct `researcher` and an executive `writer`.
- **Hierarchical Supervisor Architecture**: A central supervisor LLM reasons over task state (`has_research`, `has_analysis`, `has_report`) and dynamically delegates subtasks to:
  - 🔍 **Researcher Agent**: Gathers facts, statistics, and industry benchmarks.
  - 📊 **Analyst Agent**: Identifies patterns, strategic implications, and risks.
  - ✍️ **Writer Agent**: Compiles an executive-ready markdown report.

---

## 🛠️ Tech Stack & Dependencies

- **Orchestration**: `langgraph`, `langgraph-cli`
- **Framework & Models**: `langchain`, `langchain-groq`, `ChatGroq`, `init_chat_model`
- **Search & Tools**: `langchain-tavily` (`TavilySearch`)
- **Observability**: `langsmith`
- **Environment & Utilities**: `python-dotenv`, `typing-extensions`

---

## 📂 Repository Structure

```text
LangGraph_CrashCourse_2/
├── 1-BasicChatBot/
│   ├── 1-basicchatbot.ipynb       # Stateful chatbot, ReAct tools, memory & streaming
│   └── README.md                  # Detailed module documentation
├── 2-HumanAssistance/
│   ├── humanintheloop.ipynb       # Human-in-the-loop with interrupt & Command
│   └── README.md                  # Detailed module documentation
├── 3-Debugging/
│   ├── agent.py                   # Standalone compiled graph for Studio
│   ├── debugging.ipynb            # LangSmith tracing & Mermaid visualization
│   ├── langgraph.json             # LangGraph Studio configuration manifest
│   └── README.md                  # Detailed module documentation
├── Agents/
│   ├── multiaiagent.ipynb         # Sequential pipeline & Supervisor multi-agent system
│   └── README.md                  # Detailed module documentation
├── .env                           # Environment variables (API keys)
├── requirements.txt               # Project dependencies
├── pyproject.toml                 # Package configuration
└── README.md                      # Main project showcase README
```

---

## ⚡ Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/LangGraph_CrashCourse_2.git
cd LangGraph_CrashCourse_2
```

### 2. Create and Activate a Virtual Environment
```bash
# Using python venv
python -m venv .venv

# Windows activation
.venv\Scripts\activate

# Unix / macOS activation
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables
Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key_here
TAVILY_API_KEY=your_tavily_api_key_here
LANGSMITH_API_KEY=your_langsmith_api_key_here
LANGSMITH_TRACING=true
LANGSMITH_PROJECT=LangGraph-Agentic-Course
```

### 5. Launch & Explore
Run any of the notebooks directly using Jupyter Lab or VS Code:
```bash
jupyter lab
```

To run LangGraph Studio for visual debugging:
```bash
cd 3-Debugging
langgraph dev
```
