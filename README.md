# 🧠 Deep Agents with LangChain

[![Open in Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/deploy?repository=Aadarsh-x54/deep-agents-with-langchain&branch=main&mainModule=streamlit_app.py)

An interactive conversational AI assistant and multi-agent system built with **LangChain**, **LangGraph**, and the **`deepagents`** library, featuring a full-featured **Streamlit** user interface.

This project implements and demonstrates all core deep agent architectural patterns: multi-step planning, virtual filesystem tools, context engineering via `AGENTS.md`, modular skill progressive disclosure, swappable backends, and isolated subagents with structured output.

---

## 🌟 Key Features

- **📋 Built-in Autonomous Planning (`write_todos`)**: Break down complex user goals into tracked sequential steps (pending, in-progress, completed).
- **🗂️ Virtual & Physical Filesystem Tools**: Agent can read, write, edit, and inspect virtual or real workspace files (`write_file`, `edit_file`, `read_file`, `ls`, `glob`, `grep`).
- **🧠 Context Engineering (`AGENTS.md`)**: Injects persistent architectural context, coding rules, and conventions into the agent's memory without bloating model tokens.
- **⚡ Modular Skills (Progressive Disclosure)**: Domain expertise loaded on demand:
  - `aws`: Cloud infrastructure, IAM, and serverless best practices.
  - `langgraph`: State graph workflows and agent orchestration patterns.
  - `python`: Idiomatic Python development, typing, and testing.
  - `report-writer`: Structured report generation with citations and summaries.
- **🤖 Specialized Subagents & Context Quarantine**:
  - `research-agent`: Deep-dive web search assistant running in an isolated sub-context.
  - `structured-researcher`: Pydantic-powered subagent returning validated structured data (`summary`, `confidence`, `sources`).
- **💾 Swappable Backends**:
  - `StateBackend`: Ephemeral, thread-isolated in-memory virtual filesystem.
  - `FilesystemBackend`: Sandboxed disk workspace under `deepagentsdemo/`.
  - `StoreBackend`: Durable cross-thread memory powered by LangGraph's InMemoryStore.
- **🧵 Thread Memory & Checkpointing**: Stateful conversation memory preserved across turns using LangGraph `MemorySaver`.

---

## 📂 Project Structure

```text
├── deepagentsdemo/
│   ├── notes/
│   │   └── todo.txt                # Sample task tracking file
│   ├── projects/
│   │   └── AGENTS.md               # Context engineering memory specification
│   ├── skills/                     # Modular on-demand agent skills
│   │   ├── aws/                    # AWS cloud skill
│   │   ├── langgraph/              # LangGraph workflow skill
│   │   ├── python/                 # Python development skill
│   │   └── report-writer/          # Research report writer skill
│   ├── 1-basicsdeepagent.ipynb     # Notebook: Core deep agent concepts
│   ├── 2-contextengineering.ipynb  # Notebook: Context engineering & skills
│   ├── 3-backends.ipynb            # Notebook: Filesystem & storage backends
│   └── 4-subagents.ipynb           # Notebook: Subagents & structured outputs
├── deepagents.pdf                  # Architecture diagrams & design guide
├── streamlit_app.py                # Main interactive Streamlit application
├── requirements.txt                # Python dependencies
├── pyproject.toml                  # Project packaging configuration
├── .env.example                    # Sample environment variables template
└── README.md                       # Project documentation
```

---

## 🚀 Getting Started

### 1. Prerequisites

- Python 3.10+ (Recommended Python 3.11 - 3.13)
- API Keys:
  - **OpenAI API Key** or **Groq API Key** (for LLM inference)
  - **Tavily API Key** (for real-time internet search capability)

### 2. Clone and Setup

```bash
git clone https://github.com/Aadarsh-x54/deep-agents-with-langchain.git
cd deep-agents-with-langchain
```

Create and activate a virtual environment:

```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

### 3. Configure Environment Variables

Create a `.env` file based on `.env.example`:

```bash
cp .env.example .env
```

Edit `.env` and fill in your keys:

```env
OPENAI_API_KEY=sk-...
GROQ_API_KEY=gsk_...
TAVILY_API_KEY=tvly-...
```

### 4. Run the Application

Launch the Streamlit app:

```bash
streamlit run streamlit_app.py
```

The app will be accessible at `http://localhost:8501`.

---

## 🌐 Deploying to Streamlit Community Cloud

The easiest way to deploy this application online for free:

1. Push this repository to your GitHub account (public or private).
2. Go to [share.streamlit.io](https://share.streamlit.io/) and log in with GitHub.
3. Click **"New app"** and select:
   - **Repository**: `Aadarsh-x54/deep-agents-with-langchain`
   - **Branch**: `main`
   - **Main file path**: `streamlit_app.py`
4. Expand **Advanced settings** and paste your secrets in the **Secrets** section:
   ```toml
   OPENAI_API_KEY = "your-openai-api-key"
   GROQ_API_KEY = "your-groq-api-key"
   TAVILY_API_KEY = "your-tavily-api-key"
   ```
5. Click **Deploy!**

---

## 📖 Deep Agent Architecture Overview

Based on LangChain & LangGraph best practices:

```
[ User Input ]
      │
      ▼
[ Main Agent / Planner ] ◄──► [ MemorySaver Checkpointer (Thread History) ]
      │
      ├──► [ Context Engineering ] ──► Injects AGENTS.md guidelines
      ├──► [ Progressive Skills ]  ──► Loads AWS, Python, LangGraph skills on demand
      ├──► [ Backend Selection ]   ──► StateBackend / FilesystemBackend / StoreBackend
      ├──► [ Tools ]               ──► Tavily Web Search, Filesystem tools, write_todos
      └──► [ Subagent Routing ]    ──► research-agent | structured-researcher (Pydantic)
```

---

## 📄 License

This project is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.
