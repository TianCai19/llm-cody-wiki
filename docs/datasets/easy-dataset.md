---
Title: Building Datasets with easy-dataset
Summary: Create instruction or QA datasets quickly for training and eval.
Tags: [datasets, curation, preprocessing]
Updated: 2025-08-29
Links:
  - label: easy-dataset
    url: https://github.com/your-org/easy-dataset
---

# Building Datasets with easy-dataset

`easy-dataset` streamlines collecting, transforming, and exporting datasets in JSONL format for training and evaluation.

## Install
```bash
pip install easy-dataset
```

## Example: Convert CSV to JSONL
```bash
easy-dataset convert \
  --input data/raw.csv \
  --input-format csv \
  --output data/train.jsonl \
  --map "instruction=question" --map "output=answer"
```

## Tips
- Keep a small dev/test split to catch regressions and overfitting.
- Deduplicate and sanitize PII before publishing datasets.

