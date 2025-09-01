---
Title: Unsloth RL Training
Summary: Basic workflow for reinforcing LLMs with Unsloth.
Tags: [training, rl, unsloth]
Updated: 2025-09-01
Links:
  - label: Unsloth RL Guide
    url: https://docs.unsloth.ai/basics/reinforcement-learning-rl-guide/training-ai-agents-with-rl
---

# Unsloth RL Training

Unsloth offers a lightweight interface for reinforcement learning on top of popular Llama-class models.
It focuses on efficient PPO-style fine-tuning where an agent learns from reward signals rather than fixed outputs.

## Key Points
- Wrap a base model with `FastLanguageModel` and provide a reward function.
- Use proximal policy optimization (PPO) steps to update the policy.
- Log metrics such as reward, KL divergence, and token usage for debugging.

## Minimal Example
```python
from unsloth import FastLanguageModel
from unsloth.ppo import PPOTrainer, RLConfig

# load a quantized base model
model, tokenizer = FastLanguageModel.from_pretrained(
    model_name="meta-llama/Llama-3-8b",
    load_in_4bit=True,
)

config = RLConfig(batch_size=4, lr=1e-5, ppo_epochs=1)
trainer = PPOTrainer(model, tokenizer, config)

prompt = "Translate to French: Hello world"
outputs = trainer.generate(prompt)
reward = some_reward_fn(prompt, outputs)
trainer.step(prompt, outputs, reward)
```

## Notes
- Reward models can be learned or heuristic.
- Training often alternates between supervised fine-tuning and RL steps.
- Monitor stability; clip KL to prevent divergence.

## Further Reading
- [Unsloth RL Guide](https://docs.unsloth.ai/basics/reinforcement-learning-rl-guide/training-ai-agents-with-rl) — official walkthrough.
