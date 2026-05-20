# LangGraph Tool-Calling Demo

A minimal LangGraph agent that routes between an LLM and a tool node. Use it to explore tool calling, graph visualization, and LangSmith tracing.

## What it does

- **LLM**: Groq `llama3-8b-8192` via LangChain
- **Tool**: `add(a, b)` — the model calls it for math questions (e.g. “what is 5 plus 20”)
- **Graph**: `tool_calling_llm` → (tool call?) → `tools` → back to LLM, or END

## Files

| File | Purpose |
|------|---------|
| `debugging.ipynb` | Step-by-step notebook (build graph, visualize, invoke) |
| `agent.py` | Compiled graph exported as `tool_agent` |
| `langgraph.json` | LangGraph Studio config (`tool_agent` → `./agent.py:tool_agent`) |

## Setup

1. Create a `.env` in the project root (parent of this folder) with:

   ```
   GROQ_API_KEY=your_key
   LANGCHAIN_API_KEY=your_langsmith_key   # optional, for tracing
   ```

2. Install dependencies (LangGraph, LangChain, python-dotenv, etc.) in your environment.

3. Run the notebook, or use LangGraph Studio with this directory.

## Quick usage (notebook)

```python
from agent import tool_agent

# General question — no tool
tool_agent.invoke({"messages": "What is machine learning?"})

# Math — uses add tool
tool_agent.invoke({"messages": "what is 5 plus 20"})
```

LangSmith tracing is enabled when `LANGCHAIN_API_KEY` is set (`LANGSMITH_PROJECT=TestProject`).
