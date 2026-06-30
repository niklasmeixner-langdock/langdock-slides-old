# Langdock Slide Generator

Generate professional presentation slides for Langdock training sessions. Slides are authored as **HTML** using a shared template + design-token system, then built into **Figma** programmatically via the Figma MCP server.

This repo is meant to be driven by an AI agent (Claude Code). You describe the deck you want; the agent picks templates, fills in content, and creates the slides directly in your Figma file.

---

## Prerequisites

To import slides into Figma you need all of the following:

1. **Figma Desktop App** — the MCP runs against your running Figma session. The slides are created live in an open file. The web app alone is not sufficient.
2. **An LLM provider/client that supports local MCP servers** — e.g. Claude Code, Claude Desktop, or another MCP-capable client. The agent calls Figma through MCP, so the client must be able to connect to local/desktop MCP servers.
3. **The Figma MCP server** (see below) connected in your client.
4. A local web server for previewing/serving HTML slides and assets (`http-server`, ships with Node).

---

## Figma MCP — the `use_figma` tool

Slides are built using the **Figma MCP server**, specifically its **`use_figma`** tool (full name `mcp__claude_ai_Figma__use_figma`).

`use_figma` executes JavaScript against the **Figma Plugin API** in your open desktop file. The agent uses it to create frames, apply auto-layout, set fonts/colors, and insert SVG icons — i.e. it builds each slide node-by-node rather than pasting a screenshot.

> **Important:** Before the agent calls `use_figma`, it must read the `/figma-use` skill shipped with the Figma plugin (fallback: `skill://figma/figma-use/SKILL.md`). This documents the required patterns (auto-layout, font loading, child append order, etc.).

The same Figma server also exposes read/screenshot tools (`get_design_context`, `get_screenshot`, `get_metadata`), but slide generation uses `use_figma` for building.

### Setup checklist

1. Open the **Figma Desktop App** and open (or create) the destination file.
2. Connect the **Figma MCP server** in your MCP-capable client.
3. Grab the destination **file key** — the agent needs it to know where to build (`use_figma({ fileKey, code })`).

---

## The two skills (workflow)

The repo ships two slash-command skills. Both share the same style system and Figma import path; they differ in whether you start from a template.

| Skill | When to use | What it does |
|-------|-------------|--------------|
| **`/slides`** | You have a topic, schedule, or brief and want a full deck. | Analyzes your input, proposes a deck structure (which template per slide), gets your approval, then fills the templates and builds every slide in Figma. |
| **`/design-slide`** | No existing template fits and you need a custom one-off slide. | Designs a bespoke layout using the same design tokens (colors, type scale, spacing), then builds it in Figma. |

### Typical flow

```
1. git pull                         # get latest templates / styles / knowledge
2. Open Figma Desktop, grab file key
3. npx http-server . -p 8080 &      # serve HTML + assets locally
4. /slides  → describe your deck    # agent proposes structure → you approve
   (or /design-slide for a custom slide)
5. Agent writes HTML to slides/<project>/ and builds each slide via use_figma
```

`/slides` is the fast path (reuse + fill templates). Drop to `/design-slide` only for slides no template covers.

---

## Project structure

```
templates/        HTML slide templates (reusable layouts)
slides/           Generated slides (gitignored, per-client)
                    e.g. slides/bechtle/, slides/acme-training/
assets/
  brand-assets/   Langdock logo
  tabler-icons/   SVG icon library (see index.md)
  integration-icons/   Slack, Notion, Google Drive, etc.
  workflow-icons/      Agent / code / condition nodes, etc.
knowledge/
  index.md        Product knowledge → docs.langdock.com
styleguide.md     Full design-system reference
CLAUDE.md         Agent instructions (read this for technical detail)
```

---

## Design tokens (quick reference)

**3-Meter Rule:** every slide must be readable from 3 meters. No text below 18px. Canvas is **1920×1080** with **64px** margins.

| Role | Size / weight |
|------|---------------|
| Display | 72–80px / 700 |
| Headline 1 (titles) | 56–64px / 700 |
| Headline 2 | 40–48px / 600 |
| Body | 20–24px / 500 |

Colors: Background `#FFFFFF`, Text `#111827`, Secondary `#6B7280`, Border `#E5E7EB`, Accent blue `#456AFC`.

Full system: [`styleguide.md`](styleguide.md). Technical Figma-build patterns: [`CLAUDE.md`](CLAUDE.md).

---

## Contributing changes

When editing shared resources (templates, styles, knowledge), work on a branch and open a PR — keep `main` clean:

```bash
git switch -c <descriptive-branch-name>
# make changes
git add -A && git commit -m "Description" && git push -u origin HEAD
gh pr create --title "Title" --body "Description"
```

Generated client decks under `slides/` are gitignored and don't need a PR.
