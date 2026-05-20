# /slides - Generate Slides from Templates

Generate presentation slides by selecting and filling existing templates. This is the primary workflow for creating slide decks.

## When to Use
- Creating multiple slides from a training schedule or topic list
- Standard slide types (agenda, features, comparisons, etc.)
- Quick turnaround with consistent quality

## Workflow

1. **Parse the request** - Identify topics/modules to cover
2. **Research content** - Read `knowledge/index.md`, fetch docs if needed
3. **Select templates** - Match content to appropriate template
4. **Generate HTML** - Fill template with content, save to `slides/<client>/`
5. **Import to Figma** - Use `use_figma` Plugin API (see CLAUDE.md)

---

## Template Catalog

Browse `templates/` for available layouts. Each template is self-documented with comments.

### Quick Selection Guide

| Content Type | Recommended Template |
|--------------|---------------------|
| Session opener, objectives | `02-goals-agenda.html` |
| Chapter break | `01-section-divider.html` |
| Feature overview | `03-comparison-grid.html`, `11-platform-overview.html` |
| Step-by-step process | `05-numbered-cards.html`, `timeline.html` |
| Feature + screenshot | `04-split-screenshot.html` |
| Code/API examples | `09-split-code.html` |
| Hands-on exercise | `06-exercise-dark.html` |
| Key statement | `08-centered-statement.html` |
| Before/after, pros/cons | `07-comparison-flex.html`, `comparison.html` |
| Client logos | `10-customer-logos.html` |
| Connected concepts | `13-network-connection.html` |

### Content Positioning Guide

| Content Amount | Position |
|----------------|----------|
| Simple (1-4 items) | Lower third (~600px from top) |
| Dense (5+ items) | Full height (from ~220px) |
| Single message | Centered |
| Content + Visual | Split layout |

---

## Template Workflow

For each slide:

```
1. Read the template HTML file
2. Understand its structure (comments explain customization points)
3. Replace placeholder content with actual content
4. Adjust number of items/cards as needed
5. Save to slides/<client>/slide-name.html
```

### Example

User: "Create a slide about Langdock integrations"

```
1. Check templates → 11-platform-overview.html or 13-network-connection.html
2. Read template to understand structure
3. Research: Read knowledge/index.md → fetch integrations docs
4. Fill template with integration names, icons, descriptions
5. Save to slides/client/integrations.html
6. Capture to Figma
```

---

## Multi-slide Sessions

When creating multiple slides:

1. **Start server once**: `npx http-server . -p 8080 &`
2. **Ask Figma destination once**: Let user pick file
3. **Create all slides**: Write HTML files
4. **Batch import**: Use `use_figma` to create each slide in Figma
5. **Verify**: Use `get_screenshot` to check each slide

---

## Tips

- **Don't over-customize** - Templates are designed to work; just fill content
- **One concept per slide** - Split dense topics across multiple slides
- **Use the right template** - If content doesn't fit, pick a different template or use `/design-slide`
- **Check icons** - Use `assets/tabler-icons/` for consistent iconography
