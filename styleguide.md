# Langdock Slide Style Guide

## The 3-Meter Rule

**All slides must be readable from 3 meters away.** This is the standard viewing distance for presentations. Design with this constraint in mind:

- No text smaller than 18px
- Important content should be 24px+
- Headlines should dominate the visual hierarchy
- Use contrast and whitespace to aid readability

---

## Design Tokens

### Frame Size

**Always use 1920x1080** for all slides. This is the standard HD presentation format.

```css
body {
  width: 1920px;
  height: 1080px;
}
```

### Colors

| Token | Value | Usage |
|-------|-------|-------|
| Background | `#FFFFFF` | Slide background |
| Surface | `#FFFFFF` | Cards, containers |
| Text Primary | `#111827` | Headlines, important text |
| Text Secondary | `#6B7280` | Body text, descriptions |
| Text Muted | `#9CA3AF` | Labels, captions |
| Border | `#E5E7EB` | Card borders, dividers |
| Accent Blue | `#4D65FF` | Brand blue, primary accent |
| Accent Beige | `#F0EBE3` | Warm pastel accent |
| Accent Sage | `#D4DDD6` | Green pastel accent |
| Accent Lavender | `#D5D0E5` | Purple pastel accent |
| Accent Gray | `#E3E0DB` | Warm gray accent |
| Accent Dark | `#1F2024` | Dark cards, badges |
| Code Background | `#1E293B` | Code blocks |

### Typography

**Font Families:**
- Primary: `'Inter', -apple-system, BlinkMacSystemFont, sans-serif`
- Monospace: `'JetBrains Mono', monospace`

**Type Scale (minimum sizes for 3m viewing):**

| Level | Size | Weight | Letter Spacing | Usage |
|-------|------|--------|----------------|-------|
| Display | 72-80px | 700 | -3px | Hero statements, section titles |
| Headline 1 | 56-64px | 700 | -2px | Slide titles |
| Headline 2 | 40-48px | 600 | -1.5px | Section headers, card titles |
| Headline 3 | 32-36px | 600 | -1px | Subsections, feature names |
| Body Large | 24-28px | 500 | -0.5px | Primary content, descriptions |
| Body | 20-24px | 500 | -0.3px | Standard body text |
| Label | 18-20px | 600 | 0.5px | Tags, badges, small labels |
| Caption | 16-18px | 500 | 0 | Minimal use - footnotes only |

**Never go below 16px.** If text needs to be smaller, reconsider whether it belongs on the slide.

```css
/* Example type styles */
.display {
  font-size: 72px;
  font-weight: 700;
  letter-spacing: -3px;
  line-height: 1.1;
}

.headline-1 {
  font-size: 56px;
  font-weight: 700;
  letter-spacing: -2px;
  line-height: 1.15;
}

.headline-2 {
  font-size: 40px;
  font-weight: 600;
  letter-spacing: -1.5px;
  line-height: 1.2;
}

.body-large {
  font-size: 24px;
  font-weight: 500;
  letter-spacing: -0.5px;
  line-height: 1.5;
}

.body {
  font-size: 20px;
  font-weight: 500;
  letter-spacing: -0.3px;
  line-height: 1.5;
}

.label {
  font-size: 18px;
  font-weight: 600;
  letter-spacing: 0.5px;
  text-transform: uppercase;
}
```

### Layout

| Token | Value | Usage |
|-------|-------|-------|
| Edge Padding | 64px | Distance from slide edges |
| Gap XL | 64px | Between major sections |
| Gap LG | 48px | Between content blocks |
| Gap MD | 32px | Between cards, rows |
| Gap SM | 16-24px | Within components |
| Gap XS | 8-12px | Tight spacing |
| Radius XL | 24px | Large cards, containers |
| Radius LG | 16px | Cards, code blocks |
| Radius MD | 12px | Buttons, inputs |
| Radius Pill | 100px | Tags, badges |

### Shadows

- **None by default** - Use borders for separation
- Exception: Elevated modals or overlays can use subtle shadow

---

## Components

### Slide Header

**Every slide must have a consistent header.** The header provides navigation context and branding.

```
┌─────────────────────────────────────────────────────────────────┐
│  [Logo]                                    Section Name / 01    │
│                                                    [LIVE DEMO]  │
└─────────────────────────────────────────────────────────────────┘
```

**Structure:**
- **Left**: Langdock logo (PNG, 28-32px height)
- **Right**: Section indicator + separator + slide number
- **Below number** (optional): Tag/pill for special slides (e.g., "LIVE DEMO", "EXERCISE")

```html
<div class="slide-header">
  <img class="logo" src="assets/brand-assets/langdock-logo.png" alt="Langdock" height="32">
  <div class="header-right">
    <div class="header-nav">
      <span class="section-name">Introduction</span>
      <span class="separator">/</span>
      <span class="slide-number">01</span>
    </div>
    <!-- Optional: only include for special slides -->
    <div class="slide-tag">LIVE DEMO</div>
  </div>
</div>
```

```css
.slide-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 32px;
}

.logo {
  height: 32px;
  width: auto;
}

.header-right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 8px;
}

.header-nav {
  display: flex;
  align-items: center;
  gap: 8px;
}

.section-name {
  font-size: 18px;
  font-weight: 500;
  color: #6B7280;
}

.separator {
  font-size: 18px;
  color: #9CA3AF;
}

.slide-number {
  font-size: 18px;
  font-weight: 600;
  color: #6B7280;
}

.slide-tag {
  background: #1F2937;
  color: white;
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 0.5px;
  padding: 6px 12px;
  border-radius: 100px;
}

/* Tag variants */
.slide-tag.demo { background: #456AFC; }
.slide-tag.exercise { background: #0D9488; }
```

**Tag variants:**
| Tag | Background | Use for |
|-----|------------|---------|
| Default | `#1F2937` | Generic labels |
| Demo | `#456AFC` | Live demonstrations |
| Exercise | `#0D9488` | Hands-on activities |

### Tags & Pills

Dark background pills for feature tags:

```css
.tag {
  background: #1F2937;
  color: white;
  font-size: 18px;
  font-weight: 600;
  padding: 12px 24px;
  border-radius: 100px;
  display: inline-flex;
  align-items: center;
  gap: 10px;
}

.tag svg {
  width: 20px;
  height: 20px;
}
```

Light variant:
```css
.tag-light {
  background: #EDEDEE;
  color: #6B7280;
  font-size: 18px;
  font-weight: 500;
  padding: 12px 20px;
  border-radius: 100px;
}
```

### Cards

White cards with subtle border:

```css
.card {
  background: #FFFFFF;
  border: 1px solid #E5E7EB;
  border-radius: 20px;
  padding: 32px;
}

.card-title {
  font-size: 24px;
  font-weight: 600;
  color: #111827;
  margin-bottom: 12px;
}

.card-body {
  font-size: 20px;
  color: #6B7280;
  line-height: 1.5;
}
```

### Icon Containers

For stat icons or feature icons:

```css
.icon-container {
  width: 56px;
  height: 56px;
  background: #F3F4F6;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-container svg {
  width: 28px;
  height: 28px;
  color: #456AFC;
}
```

### Code Blocks

```css
.code-block {
  background: #1E293B;
  border-radius: 16px;
  overflow: hidden;
}

.code-header {
  background: #334155;
  padding: 16px 20px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 16px;
  color: #94A3B8;
}

.code-content {
  padding: 24px;
  font-family: 'JetBrains Mono', monospace;
  font-size: 18px;  /* Minimum for code */
  line-height: 1.6;
  color: #E2E8F0;
}
```

Syntax highlighting colors:
- Keywords: `#67E8F9` (cyan)
- Strings: `#86EFAC` (green)
- Numbers: `#FBBF24` (yellow)
- Booleans: `#F472B6` (pink)
- Comments: `#94A3B8` (gray)

---

## Design Principles

1. **The 3-Meter Rule** - Every element must be readable from 3 meters away
2. **Less is More** - One concept per slide, generous whitespace
3. **Clear Hierarchy** - Headlines dominate, body supports, labels orient
4. **Use Available Assets** - Always use `assets/brand-assets/langdock-logo.png`, icons from `assets/tabler-icons/`
5. **Consistent Spacing** - Use the spacing tokens, don't invent new values
6. **No Tiny Text** - If it needs to be small, it probably shouldn't be on the slide

---

## Readability Checklist

Before finalizing a slide, verify:

- [ ] Smallest text is at least 18px
- [ ] Body text is 20-24px
- [ ] Headlines are clearly larger than body
- [ ] Sufficient contrast (text vs background)
- [ ] Not too much content (can read in 5-10 seconds)
- [ ] Icons are at least 24px

---

## Icons

Use icons from `assets/tabler-icons/` - see `assets/tabler-icons/index.md` for the full catalog.

**Minimum icon sizes:**
- Inline with text: 20-24px
- Standalone: 32-48px
- Decorative/hero: 64-80px

Common icons:
- `check` - Checkmark for feature tags
- `player-play` - Demo/play buttons
- `sparkles` - AI/magic decoration
- `code` - Code examples
- `plug-connected` - Integrations/connections

---

## Template Catalog

See `templates/` directory for reusable slide templates.
