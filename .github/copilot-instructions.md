# LLM Cody Wiki

The LLM Cody Wiki is a MkDocs-based documentation site that provides curated knowledge about Large Language Models. It's built with Python, MkDocs, and the Material theme, focusing on practical guidance for prompting, training, inference, evaluation, and LLM tooling.

**Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Bootstrap and Dependencies
Run these commands in order to set up the development environment:
```bash
# Verify Python environment
python3 --version  # Should be Python 3.7+
pip --version

# Install core dependencies
pip install --upgrade pip
pip install mkdocs mkdocs-material
# Note: pip install may fail due to network timeouts - this is normal in constrained environments
# If installation fails, check if packages are already installed with: mkdocs --version
```

**Timing:** Dependencies install in 30-60 seconds. Network timeouts may occur.

### Build and Validate
```bash
# Build the site (production build with strict validation)
mkdocs build --strict

# Expected output: "Documentation built in X.XX seconds"
# Build time: ~1-2 seconds. NEVER CANCEL.
```

### Local Development
```bash
# Serve locally for development
mkdocs serve --dev-addr=127.0.0.1:8000

# Site will be available at: http://127.0.0.1:8000
# Startup time: ~3-5 seconds. Auto-reloads on file changes.
```

### Validation and Testing
Always run these validation steps after making changes:
```bash
# 1. Validate YAML configuration
python3 -c "import yaml; yaml.safe_load(open('mkdocs.yml'))"

# 2. Build with strict validation
mkdocs build --strict

# 3. Test the built site
cd site && python3 -m http.server 8080
# Test accessibility: curl -I http://127.0.0.1:8080/
```

## Manual Validation Scenarios

**CRITICAL**: After making any content changes, ALWAYS validate these user scenarios:

### Scenario 1: Navigation and Content Rendering
1. Run `mkdocs serve`
2. Navigate to http://127.0.0.1:8000
3. Verify the hero section loads with "LLM knowledge that simply works"
4. Click through topic tiles (Prompting, Models, Training, etc.)
5. Verify internal links work between pages
6. Test search functionality

### Scenario 2: New Content Validation
1. Add new content using the template in `docs/meta/templates/article.md`
2. Update `mkdocs.yml` nav section if needed
3. Run `mkdocs build --strict` - must complete without errors
4. Serve locally and verify new content appears and renders correctly
5. Check that frontmatter (Title, Summary, Tags, Updated) displays properly

### Scenario 3: CSS and Assets
1. Verify custom CSS loads from `docs/assets/stylesheets/extra.css`
2. Check that hero section background and tiles grid display correctly
3. Test both light and dark mode themes

## Repository Structure

### Key Directories
- `docs/` - All documentation content (Markdown files)
- `docs/meta/` - Style guides, taxonomy, and templates
- `docs/assets/` - CSS, images, and other static assets
- `site/` - Generated static site (ignored in git)
- `.github/workflows/` - CI/CD automation

### Important Files
- `mkdocs.yml` - Main configuration file
- `docs/index.md` - Homepage with hero section
- `docs/meta/style-guide.md` - Content guidelines
- `docs/meta/taxonomy.md` - Topic organization
- `docs/meta/templates/article.md` - Template for new pages
- `CONTRIBUTING.md` - Contribution guidelines

### Content Organization
Topics are organized in these directories:
- `prompting/` - Prompting patterns and techniques
- `models/` - Model families and comparisons
- `training/` - Fine-tuning and training methods
- `inference/` - Serving and optimization
- `evaluation/` - Testing and benchmarking
- `agents/` - LLM agents and workflows
- `tooling/` - Development tools and utilities
- `infrastructure/` - Deployment and scaling

## Common Development Tasks

### Adding New Content
1. Use template: `cp docs/meta/templates/article.md docs/[topic]/[filename].md`
2. Update frontmatter: Title, Summary, Tags, Updated date
3. Add to navigation in `mkdocs.yml` if needed
4. Follow style guide in `docs/meta/style-guide.md`
5. Validate with `mkdocs build --strict`

### Content Guidelines
- Keep pages concise with 1-3 sentence summaries
- Use YAML frontmatter for metadata
- Include practical examples and code blocks
- Cross-link related concepts
- Date time-sensitive content
- Follow naming: lowercase-with-hyphens.md

### CI/CD Pipeline
The GitHub Actions workflow in `.github/workflows/mkdocs.yml` automatically:
1. Installs Python and dependencies
2. Runs `mkdocs build --strict`
3. Deploys to GitHub Pages

**Build timing:** CI build completes in 2-3 minutes. NEVER CANCEL.

## Troubleshooting

### Common Issues
- **Warning about unrecognized relative link 'url'**: Expected in template file, can be ignored
- **Build fails**: Check YAML syntax in frontmatter and `mkdocs.yml`
- **Content not appearing**: Verify file is in `docs/` and added to nav in `mkdocs.yml`
- **Search not working**: Rebuild with `mkdocs build --clean`

### Performance Notes
- Build is very fast (~1-2 seconds)
- Live reload during development is instant
- Site generation produces ~3.4MB output
- No heavy build processes or complex tooling

## Quick Commands Reference

```bash
# Development workflow
mkdocs serve                    # Start dev server
mkdocs build --strict          # Production build
mkdocs build --clean           # Clean rebuild

# Validation
python3 -c "import yaml; yaml.safe_load(open('mkdocs.yml'))"  # YAML check
curl -I http://127.0.0.1:8000/ # Test local site

# File operations
cp docs/meta/templates/article.md docs/[topic]/new-page.md  # New page
```

## Repository Context
- **Language**: Chinese and English content
- **License**: Open source documentation
- **Deployment**: GitHub Pages via Actions
- **Theme**: Material for MkDocs with custom CSS
- **Content Focus**: Practical LLM knowledge and tooling