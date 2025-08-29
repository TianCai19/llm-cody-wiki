# LLM Cody Wiki

A community-friendly wiki for Large Language Model (LLM) knowledge: foundations, prompting, training, inference, evaluation, safety, agents, infrastructure, and applied patterns. Organized for quick lookup and steady growth.

## Quick Start
- Browse content in `docs/` directly.
- Optional site (MkDocs):
  - Install MkDocs + Material (`pip install mkdocs mkdocs-material`) when you’re ready.
  - Serve locally: `mkdocs serve` (open http://127.0.0.1:8000)
  - Build static site: `mkdocs build` (outputs to `site/`)

## Structure
- `docs/index.md`: Landing page and overview
- `docs/meta/`: Style guide, taxonomy, templates
- `docs/*/overview.md`: Topic overviews (Prompting, Models, Training, ...)
- `docs/resources.md`: Curated links, tools, and references
- `docs/glossary.md`: Terms and definitions

## Contributing
- See `CONTRIBUTING.md` for guidelines.
- Use the template in `docs/meta/templates/article.md` for new pages.
- Keep content concise, well-cited, and dated when relevant.

## Goals
- Clear taxonomy for fast discovery
- Practical, reproducible guidance and references
- Lightweight tooling with plain Markdown

## Non-Goals (for now)
- Heavy build systems or frameworks
- Keeping pace with every daily release without curation

---
Maintainers can adjust sections and tags in `docs/meta/taxonomy.md` as the wiki evolves.
