# /design-slide - Create Custom Slides

Design unique slides when no existing template fits. Uses the same design system but creates custom layouts from scratch.

## When to Use
- Unique visualization needs (custom diagrams, flows)
- Content that doesn't fit any template
- One-off slides with special requirements
- Creative layouts for specific concepts

**Consider `/slides` first** - Templates cover most use cases and are faster to produce.

---

## Design Philosophy

### Avoid Boxy Layouts
Prefer flowing, organic layouts over rigid card-based grids.

**Avoid:**
- White cards with shadows for simple lists
- Rigid 3-4 column grids for everything
- `flex: 1` that stretches cards to fill space
- Heavy borders for simple content

**Prefer:**
- Flowing pill tags with `flex-wrap`
- Icon + label combinations (no box needed)
- Arrows/connectors for relationships
- Generous whitespace
- Content sized to fit, not stretched

### Pills/Tags Pattern
```css
.tag {
  background: #ededee;
  padding: 12px 16px;
  border-radius: 100px;
  font-size: 20px;
  color: #717279;
}

.tag-group {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
}
```

### When to Use Cards vs Tags

| Use Tags/Pills | Use Cards |
|----------------|-----------|
| Feature lists | Step-by-step processes |
| Capabilities | Detailed explanations |
| Quick labels | Code examples |
| Grouped items | Structured data |

---

## Visual Connectors

### Dashed Lines (annotations only)
```css
/* Info box with dashed border */
.info-box {
  border: 1.5px dashed #c0c0c0;
  border-radius: 12px;
  padding: 16px 20px;
}

/* SVG annotation connector */
<path d="M 0 40 C 50 40, 100 80, 150 80"
      stroke="#c0c0c0"
      stroke-width="1.5"
      stroke-dasharray="6 4"
      fill="none"/>
```

### Solid Lines (flow diagrams)
```css
/* Flow arrow (blue) */
<path d="M 50 0 L 50 40" stroke="#4D65FF" stroke-width="2" fill="none"/>
<polygon points="50,50 45,40 55,40" fill="#4D65FF"/>

/* Node connector (light gray) */
<path d="M 380 360 C 480 420, 620 420, 720 360"
      stroke="#e0e0e0"
      stroke-width="1.5"
      fill="none"/>
```

| Line Type | Use For | Color |
|-----------|---------|-------|
| Dashed gray | Info boxes, annotations | `#c0c0c0` |
| Solid blue | Flow arrows | `#4D65FF` |
| Solid light gray | Node connections | `#e0e0e0` |

---

## Base Structure

Start every custom slide with this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=1920, height=1080">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      font-family: 'Inter', sans-serif;
      width: 1920px;
      height: 1080px;
      background: #FFFFFF;
      padding: 64px;
      position: relative;
      -webkit-font-smoothing: antialiased;
    }

    /* Your custom styles here */
  </style>
</head>
<body>
  <!-- Your content here -->
</body>
</html>
```

---

## Design Tokens

```css
/* Colors */
--background: #FFFFFF;
--background-elevated: #F0EBE3;
--text-primary: #111827;
--text-secondary: #6B7280;
--accent-beige: #F0EBE3;
--accent-sage: #D4DDD6;
--accent-lavender: #D5D0E5;
--accent-gray: #E3E0DB;
--accent-dark: #1F2024;
--surface-white: #FFFFFF;

/* Typography */
.headline-1 {
  font-size: 64px;
  font-weight: 600;
  letter-spacing: -3.2px;
  color: #121420;
}

.headline-2 {
  font-size: 40px;
  font-weight: 700;
  letter-spacing: -1.6px;
  color: #121420;
}

.body {
  font-size: 20px;
  font-weight: 500;
  letter-spacing: -0.2px;
  color: #717279;
}

/* Layout */
Canvas: 1920 x 1080px
Margins: 64px all sides
```

---

## Workflow

1. **Understand the need** - What can't be done with templates?
2. **Sketch the layout** - Plan the visual hierarchy
3. **Start with base structure** - Use the HTML skeleton above
4. **Build incrementally** - Add elements, test in browser
5. **Use design tokens** - Keep colors/typography consistent
6. **Reference existing templates** - Borrow patterns that work
7. **Import to Figma** - Use `use_figma` Plugin API (see CLAUDE.md)

---

## Tips

- **Browse templates for inspiration** - Even custom slides can borrow patterns
- **Test in browser first** - Open the HTML locally before Figma capture
- **Keep it simple** - Custom doesn't mean complex
- **Use SVG for diagrams** - More control than CSS for custom shapes
- **Check `styleguide.md`** - Full design system reference
