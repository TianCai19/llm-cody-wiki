---
Title: EvalScope Quickstart
Summary: Evaluate prompts and models with a lightweight, scriptable workflow.
Tags: [evaluation, tooling, automation]
Updated: 2025-08-29
Links:
  - label: EvalScope
    url: https://github.com/your-org/evalscope
---

# EvalScope Quickstart

EvalScope provides a simple harness to define test cases, run them against models, and compute metrics. Use it to compare prompts, models, or decoding settings.

## Install
```bash
pip install evalscope
```

## Define Cases (YAML or JSON)
```yaml
cases:
  - id: greeting
    input: "Say hello in Spanish"
    expected_contains: ["hola"]
```

## Run
```bash
evalscope run \
  --cases cases.yaml \
  --model openai/gpt-4o-mini \
  --provider-base-url http://127.0.0.1:4000  # via LiteLLM
```

## Tips
- Add task-specific metrics (exact match, regex, BLEU/ROUGE) per use case.
- Version your cases alongside code to track regressions.

