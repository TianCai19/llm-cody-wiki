---
Title: Swift Fine-tuning (ms-swift)
Summary: Quick recipe to fine-tune an LLM with Swift and export for inference.
Tags: [training, finetune, lora]
Updated: 2025-08-29
Links:
  - label: Swift Repo
    url: https://github.com/modelscope/swift
---

# Swift Fine-tuning (ms-swift)

Swift provides concise scripts to fine-tune models with LoRA/QLoRA and export weights for serving.

## Install
```bash
pip install ms-swift  # or refer to repo instructions
```

## Minimal LoRA Run
```bash
swift finetune \
  --model "meta-llama/Llama-3-8b" \
  --dataset path/to/train.jsonl \
  --output ./outputs/llama3-lora \
  --batch-size 4 --accum 8 --epochs 1 \
  --lr 2e-4 --lora-r 8 --lora-alpha 32 --bf16
```

## Export and Serve
```bash
swift export --input ./outputs/llama3-lora --merge-lora --out ./merged
# Then load with vLLM/TGI or via LiteLLM routing.
```

## Notes
- Use QLoRA for low VRAM; validate outputs with small eval sets.
- Track dataset and hyperparams in the output folder for reproducibility.

