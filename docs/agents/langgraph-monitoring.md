---
Title: LangGraph Monitoring (with LiteLLM)
Summary: Build a small graph, route calls via LiteLLM, and record prompts/outputs.
Tags: [agents, langgraph, monitoring, tracing, litellm]
Updated: 2025-08-29
Links:
  - label: LangGraph Docs
    url: https://langchain-ai.github.io/langgraph/
---

# LangGraph Monitoring (with LiteLLM)

This example routes LLM calls through a local LiteLLM proxy and logs prompts/outputs from each node.

## Install
```bash
pip install langgraph langchain openai
```

## Minimal Graph
```python
from langgraph.graph import StateGraph, START, END
from typing import TypedDict
from openai import OpenAI

client = OpenAI(base_url="http://127.0.0.1:4000", api_key="sk-local")

class S(TypedDict):
    question: str
    answer: str

def llm_node(state: S):
    prompt = f"Answer briefly: {state['question']}"
    print("[prompt]", prompt)
    resp = client.chat.completions.create(
        model="ollama/llama3:8b",
        messages=[{"role": "user", "content": prompt}],
    )
    out = resp.choices[0].message.content
    print("[output]", out)
    return {"answer": out}

g = StateGraph(S)
g.add_node("llm", llm_node)
g.add_edge(START, "llm")
g.add_edge("llm", END)
app = g.compile()

print(app.invoke({"question": "What is LangGraph?"}))
```

## Monitoring Options
- Console printing as shown above for quick visibility.
- Add structured logging or tracing hooks (e.g., to files or a DB).
- Optional: integrate with LangSmith to capture traces and artifacts.

