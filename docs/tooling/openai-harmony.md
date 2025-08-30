---
Title: OpenAI Harmony
Summary: OpenAI's response format library for gpt-oss models, enabling structured conversation formatting and tool calling.
Tags: [tooling, formatting, gpt-oss, openai, conversation]
Updated: 2025-01-02
Links:
  - label: GitHub Repository
    url: https://github.com/openai/harmony
  - label: OpenAI Cookbook Guide
    url: https://cookbook.openai.com/articles/openai-harmony
---

# OpenAI Harmony

OpenAI Harmony is the response format library for OpenAI's open-weight model series [gpt-oss](https://openai.com/open-models). It defines conversation structures, generates reasoning output, and structures function calls. The format is designed to mimic the OpenAI Responses API and is required when building custom inference solutions for gpt-oss models.

## Key Points

- **Required for gpt-oss models** — Models trained on the harmony response format won't work correctly without it
- **Multi-channel output** — Supports chain of thought, tool calling preambles, and regular responses
- **Tool namespaces** — Enables structured outputs with clear instruction hierarchy
- **Cross-language support** — Available in both Python and Rust with performance-optimized Rust core

## Installation

### Python

```bash
pip install openai-harmony
# or with uv
uv pip install openai-harmony
```

### Rust

Add to your `Cargo.toml`:

```toml
[dependencies]
openai-harmony = { git = "https://github.com/openai/harmony" }
```

## Usage Examples

### Python Example

```python
from openai_harmony import (
    load_harmony_encoding,
    HarmonyEncodingName,
    Role,
    Message,
    Conversation,
    DeveloperContent,
    SystemContent,
)

# Load the encoding for gpt-oss
enc = load_harmony_encoding(HarmonyEncodingName.HARMONY_GPT_OSS)

# Create a conversation
convo = Conversation.from_messages([
    Message.from_role_and_content(
        Role.SYSTEM,
        SystemContent.new(),
    ),
    Message.from_role_and_content(
        Role.DEVELOPER,
        DeveloperContent.new().with_instructions("Talk like a pirate!")
    ),
    Message.from_role_and_content(Role.USER, "Arrr, how be you?"),
])

# Render for completion
tokens = enc.render_conversation_for_completion(convo, Role.ASSISTANT)
print(tokens)

# Parse response after model completion
parsed = enc.parse_messages_from_completion_tokens(tokens, role=Role.ASSISTANT)
print(parsed)
```

### Rust Example

```rust
use openai_harmony::chat::{Message, Role, Conversation};
use openai_harmony::{HarmonyEncodingName, load_harmony_encoding};

fn main() -> anyhow::Result<()> {
    let enc = load_harmony_encoding(HarmonyEncodingName::HarmonyGptOss)?;
    let convo = Conversation::from_messages([
        Message::from_role_and_content(Role::User, "Hello there!")
    ]);
    let tokens = enc.render_conversation_for_completion(&convo, Role::Assistant, None)?;
    println!("{:?}", tokens);
    Ok(())
}
```

## Format Structure

The harmony format uses special delimiters and channels:

```text
<|start|>system<|message|>You are ChatGPT, a large language model trained by OpenAI.
Knowledge cutoff: 2024-06
Current date: 2025-06-28

Reasoning: high

# Valid channels: analysis, commentary, final. Channel must be included for every message.
Calls to these tools must go to the commentary channel: 'functions'.<|end|>

<|start|>developer<|message|># Instructions

Always respond in riddles

# Tools

## functions

namespace functions {
    // Gets the location of the user.
    type get_location = () => any;
    
    // Gets the current weather in the provided location.
    type get_current_weather = (_: {
        // The city and state, e.g. San Francisco, CA
        location: string,
        format?: "celsius" | "fahrenheit", // default: celsius
    }) => any;
} // namespace functions<|end|>

<|start|>user<|message|>What is the weather like in SF?<|end|>

<|start|>assistant
```

## Notes

- API providers (HuggingFace, Ollama, vLLM) handle formatting automatically
- Only needed when building custom inference solutions
- Provides consistent token-sequence formatting for rendering and parsing
- Heavy computational work happens in Rust for performance
- Python bindings offer full compatibility with 100% test parity

## Further Reading

- [OpenAI Harmony Documentation](https://cookbook.openai.com/articles/openai-harmony) — Complete format specification
- [gpt-oss Model Card](https://openai.com/index/gpt-oss-model-card/) — Official model information
- [GitHub Repository](https://github.com/openai/harmony) — Source code and development details