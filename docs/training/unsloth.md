---
Title: Unsloth Fine-tuning
Summary: Fast LoRA/QLoRA fine-tuning for Llama-class models.
Tags: [training, finetune, unsloth, qlora]
Updated: 2025-08-29
Links:
  - label: Unsloth Docs
    url: https://docs.unsloth.ai/
---

# Unsloth Fine-tuning

Unsloth focuses on speed and memory efficiency for fine-tuning. It’s well-suited for document/task-specific adapters.

## Install
```bash
pip install unsloth
```

## Minimal Example (Python)
```python
from unsloth import FastLanguageModel

model, tokenizer = FastLanguageModel.from_pretrained(
    model_name="meta-llama/Llama-3-8b",
    load_in_4bit=True,
)

# prepare your dataset of instruction/response pairs
train_data = [{"instruction":"Summarize", "output":"..."}]

model.finetune_lora(
    train_data,
    r=8, alpha=32, lr=2e-4, epochs=1, bs=4
)

model.save_lora("./outputs/llama3-unsloth-lora")
```

## Serve
- Merge LoRA or load adapters with your serving stack (vLLM, TGI). Route via LiteLLM for a unified API.

