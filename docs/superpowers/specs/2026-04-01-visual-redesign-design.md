# Visual Redesign — Design Spec
**Date:** 2026-04-01
**Status:** Approved

---

## Overview

Differentiate TacticalYogurt from visually similar competitors by replacing the blue palette with a violet/amber scheme, restructuring the hero into a split layout, and replacing the generic pill badge with an italic serif eyebrow label. All other page sections receive the color treatment passively — no structural changes outside the hero.

---

## 1. Color System

Replace all existing blue/cyan CSS variables with violet/amber equivalents.

| Variable | Old Value | New Value |
|---|---|---|
| `--bg` | `#0a0c10` | `#0f0a1e` |
| `--bg2` | `#0f1117` | `#140e24` |
| `--card` | `#13171f` | `#160f26` |
| `--border` | `rgba(255,255,255,0.07)` | `rgba(167,139,250,0.1)` |
| `--blue` | `#3b6aff` | `#7c3aed` |
| `--blue-glow` | `rgba(59,106,255,0.25)` | `rgba(124,58,237,0.25)` |
| `--green` | `#2fd87a` | `#4ade80` |
| `--text` | `#e8ecf4` | `#e8ecf4` (unchanged) |
| `--muted` | `#6b7280` | `#6b7280` (unchanged) |

New variables to add:
- `--violet: #7c3aed` — primary CTA, buttons
- `--violet-light: #a78bfa` — accents, highlights
- `--amber: #ea580c` — secondary accent
- `--amber-light: #fb923c` — eyebrow text, warm highlights

Gradient accent (used on headline span, logo, stats):
```css
background: linear-gradient(90deg, #a78bfa 0%, #fb923c 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
```

CTA button gradient (replaces solid blue):
```css
background: linear-gradient(90deg, #7c3aed, #ea580c);
box-shadow: 0 4px 24px rgba(124,58,237,.4);
```

Hero background glow (replaces existing hero glow):
```css
background:
  radial-gradient(ellipse at 20% 50%, rgba(124,58,237,.15) 0%, transparent 50%),
  radial-gradient(ellipse at 80% 20%, rgba(234,88,12,.08) 0%, transparent 40%);
```

---

## 2. Typography

Add **DM Serif Display** to the Google Fonts import:
```
family=DM+Serif+Display:ital@1
```

Add CSS variable:
```css
--serif: 'DM Serif Display', serif;
```

Used only for the hero eyebrow label.

---

## 3. Hero Restructure

### Layout

Replace the current centered single-column hero with a two-column CSS grid:

```
[text column — 1fr] [visual column — 1fr]
```

- Aligned to page center, `max-width: 1200px`
- `min-height: calc(100vh - 64px)`, `padding: 5rem 3rem`
- On mobile (≤ 768px): stack to single column, visual column hidden

### Left Column — Text

**Eyebrow label** (replaces pill badge):
```html
<div class="hero-eyebrow">The all-in-one print farm platform</div>
```
```css
.hero-eyebrow {
  font-family: var(--serif);
  font-style: italic;
  font-size: 1.1rem;
  color: var(--amber-light);
  margin-bottom: .75rem;
}
```

**Headline:** unchanged text, left-aligned, gradient on `<span>`

**Subtext:** unchanged, left-aligned, `max-width: 420px`

**CTAs:** two buttons side by side
- Primary: "Join Early Access — It's Free" → gradient button, calls `openModal()`
- Secondary: "See how it works →" → plain text link, scrolls to `#how-it-works`

**Stats row** (below CTAs):
```
16+               5                  ∞
Part categories   Marketplace        Printers
tracked           integrations       supported
```
- Numbers in gradient text, labels in `--muted`
- `display: flex; gap: 2rem`

### Right Column — Dashboard Mock

A styled panel mimicking the TacticalYogurt dashboard. Dark card with browser chrome (three dots + monospace title bar), containing:

1. **3-stat row:** Spools (violet), Printing (amber), Orders (green)
2. **Filament inventory section:** 3 spool rows with color dot, name, progress bar, percentage
3. **Printer fleet section:** 3 printer rows with status dot (green/grey), name, job filename, ETA

This is a static HTML mockup — no real data, no JS. Purely visual.

```css
.hero-visual .dashboard-mock {
  background: rgba(255,255,255,.03);
  border: 1px solid rgba(167,139,250,.1);
  border-radius: 14px;
  box-shadow: 0 32px 80px rgba(0,0,0,.5), 0 0 0 1px rgba(167,139,250,.1);
}
```

---

## 4. Nav Updates

- Logo gradient: `linear-gradient(90deg, #a78bfa, #fb923c)` on the brand name
- `.nav-cta` background: `linear-gradient(90deg, #7c3aed, #ea580c)`
- `.nav-cta-outline` border: `rgba(167,139,250,.2)`, hover border: `rgba(167,139,250,.4)`
- `.nav-dot` pulse color: `#7c3aed`

---

## 5. What Does Not Change

- Page section structure (Features, Integrations, How it Works, Pricing, Compare, CTA, Footer)
- All copy
- Modal and Google Form embed
- SVG icons (colors derived from CSS variables — will update automatically)
- Photo breaks
- Scroll behavior / fade-in animations
- Nav link structure

The green feature accent (`--green` → `#4ade80`) is already close to the new palette and needs only the variable rename.

---

## 6. Files Changed

| File | Change |
|---|---|
| `index.html` | CSS variables, Google Fonts import, hero HTML restructure, hero CSS |

---

## Out of Scope

- Section-level layout restructuring (Features grid, Pricing cards, etc.)
- New page sections
- Animation changes
- Mobile nav drawer styling changes beyond inherited color updates
