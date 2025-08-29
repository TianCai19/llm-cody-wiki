# Contributing Guide

Thank you for helping grow the LLM Cody Wiki! This guide keeps contributions consistent, useful, and easy to review.

## How to Contribute
- Open an issue first for new sections or large changes.
- Use `docs/meta/templates/article.md` for new pages.
- Add links and cross-references where helpful.
- Keep claims neutral and cite original sources.
- Prefer stable, long-lived links (official docs, archived papers).

## Content Style
- Be concise; lead with the practical takeaway.
- Include a 1–3 sentence summary at the top.
- Date time-sensitive content (e.g., benchmarks, releases).
- Use headings and short paragraphs; avoid walls of text.
- Use code blocks for commands and snippets.

## Metadata (Frontmatter)
Use this YAML frontmatter at the top of new pages:

```yaml
---
Title: SHORT CLEAR TITLE
Summary: 1–2 lines of what/why
Tags: [llm, prompting, evaluation]
Updated: YYYY-MM-DD
Links:
  - label: Source/Spec
    url: https://...
---
```

## File Naming
- Lowercase with hyphens: `few-shot-prompting.md`, `vllm-setup.md`
- Place files under the closest topic folder.

## Taxonomy
- See `docs/meta/taxonomy.md` for topics and tags.
- If a tag is missing, propose it in an issue.

## Review Checklist
- Clear summary, correct placement, and tags
- Neutral tone; citations for claims
- Internal links to related concepts
- Up-to-date as of the `Updated` date

## Getting a Local Site
- Install MkDocs: `pip install mkdocs`
- Serve: `mkdocs serve` (open http://127.0.0.1:8000)
- Build: `mkdocs build` (outputs to `site/`)
