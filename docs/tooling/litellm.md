---
Title: LiteLLM Local Usage
Summary: Run a local OpenAI-compatible proxy and call it from apps.
Tags: [tooling, proxy, inference, litellm]
Updated: 2025-08-29
Links:
  - label: LiteLLM Docs
    url: https://docs.litellm.ai/
---

# LiteLLM Local Usage

LiteLLM provides an OpenAI-compatible API proxy that can route to many backends (OpenAI, Azure, Bedrock, Ollama, vLLM, etc.). Running it locally lets you standardize client code and swap providers without app changes.

## Quick Start
```bash
pip install litellm[proxy]

# Example: proxy to a local Ollama model
export OLLAMA_BASE_URL=http://127.0.0.1:11434
litellm --model ollama/llama3:8b --num_workers 2 --port 4000

# Now an OpenAI-compatible server is available at http://127.0.0.1:4000
```

## Python Client (OpenAI-compatible)
```python
from openai import OpenAI

client = OpenAI(base_url="http://127.0.0.1:4000", api_key="sk-local")
resp = client.chat.completions.create(
    model="ollama/llama3:8b",
    messages=[{"role": "user", "content": "Hello!"}],
)
print(resp.choices[0].message.content)
```

## Notes
- Swap `--model` to route to other providers or local servers (vLLM, TGI, etc.).
- You can set per-route keys/quotas and logging in LiteLLM config.
- Pair with LangGraph for structured flows and monitoring (see Agents › LangGraph Monitoring).

