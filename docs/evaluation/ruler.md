---
Title: OpenPipe Ruler
Summary: Rule-based tests for validating LLM outputs.
Tags: [evaluation, openpipe, testing]
Updated: 2025-09-01
Links:
  - label: Ruler Docs
    url: https://art.openpipe.ai/fundamentals/ruler
---

# OpenPipe Ruler

Ruler provides a lightweight syntax to express expectations for model responses.
It lets teams encode guards like required phrases, regex patterns, or score thresholds and run them as unit tests.

## Key Points
- Define rules in YAML or Python for reuse across prompts.
- Run checks locally or in CI to catch regressions early.
- Supports custom evaluators for domain-specific metrics.

## Minimal Example
```python
from openpipe.ruler import Rule, evaluate

rules = [
    Rule.must_contain("bonjour"),
    Rule.max_tokens(50),
]

result = evaluate(prompt="Translate to French: hello", rules=rules)
print(result.passed)
```

## Notes
- Combine with RAG or fine-tuned models to enforce policy constraints.
- Failing tests surface diffs between expected and actual outputs.

## Further Reading
- [Ruler Docs](https://art.openpipe.ai/fundamentals/ruler) — official guide.
