# Interactive App Demo Section — Design Spec

**Date:** 2026-04-07
**Status:** Approved

---

## Overview

A new `#demo` section added to `index.html` between the stats strip and the features section. It shows a laptop/browser-framed mock of the TacticalYogurt app with a real sidebar nav and 4 clickable tab views. The section serves as a "see it in action" moment for prospective users before they read the feature list.

This is a **placeholder** — all mock data lives in a single `DEMO_DATA` config object so it can be updated or replaced with real screenshots/embeds when the app ships.

---

## Placement

```
[Hero]
[Stats Strip]
[>>> Interactive Demo Section <<<]  ← inserted here
[Photo Break]
[Features]
...
```

---

## Section Header

- Section label: `// see it in action`
- Heading: "The command center for your farm."
- Subtitle: "A preview of what's coming — one dashboard for every part of your operation."
- Small muted note: `// early preview — interface subject to change`

---

## Browser Frame

A macOS-style browser window mock wrapping the app shell:

- Traffic light dots (red / yellow / green)
- URL bar displaying `app.tacticalyogurt.com/{tab}` — updates dynamically as tabs change
- Max-width: ~1100px, centered
- Slight perspective tilt (matching hero tablet aesthetic) on desktop
- Border, dark chrome bar, subtle box shadow for depth
- Responsive: tilt removed and frame simplified on mobile (< 900px)

---

## App Shell (inside the frame)

### Sidebar (~200px wide)
- TY logo mark + "TacticalYogurt" wordmark at top
- 4 nav items with SVG icons:
  1. Dashboard
  2. Printer Fleet
  3. Filament Inventory
  4. Print Jobs
- Active item: violet background highlight, full-brightness text
- Inactive items: muted text, hover state

### Main Content Area
- Fills remaining width
- Content switches on sidebar click
- Transition: fade out (150ms) + fade in + slight upward slide (150ms) on enter
- Progress bars animate in (width from 0 to value) on each tab enter

---

## Tab Views

### 1. Dashboard
- 3 stat cards in a row: Active Spools, Printers Online, Pending Orders
- Recent Activity feed: 4–5 timestamped log entries (e.g. "Job completed on Bambu X1C #1", "Low stock: eSun PETG Amber")

### 2. Printer Fleet
- Table/list of 5 printers
- Per row: pulsing status dot (green = printing, grey = idle), printer name, current job filename, progress bar, ETA or "—"
- At least 1 idle printer, 1 with a nearly-full progress bar

### 3. Filament Inventory
- List of 6 spools
- Per row: color dot, brand + material + color name, horizontal progress bar, percentage remaining
- Any spool under 20% gets a small amber "Low Stock" badge
- At least 1 spool in low-stock state for visual interest

### 4. Print Jobs
- List of 5 recent jobs
- Per row: file name (monospace), printer assigned, status badge (Completed = green, In Progress = amber, Failed = red), star rating (1–5, shown as filled/empty dots or stars)
- Mix of statuses for visual variety

---

## Animations

- **On scroll into view:** Auto-cycles through all 4 tabs once (1.5s per tab), then stops on Dashboard and hands control to the user. Uses IntersectionObserver.
- **Auto-cycle fires once** — a `data-cycled` flag prevents it replaying on re-scroll.
- **Progress bars:** Animate width from 0 to target value on each tab enter (CSS transition, 400ms).
- **Status dots:** Pulse animation matching the hero nav dot style.
- **Tab switch:** 150ms fade-out / 150ms fade-in + translateY(-6px → 0) on enter.

---

## Data Structure

All mock data lives in a single config block at the top of the section's `<script>` tag:

```js
const DEMO_DATA = {
  fleet: [ /* printer objects */ ],
  inventory: [ /* spool objects */ ],
  jobs: [ /* job objects */ ],
  activity: [ /* activity log strings */ ],
  stats: { spools: 34, printersOnline: 4, pendingOrders: 8 }
};
```

To update when the real app ships: edit `DEMO_DATA`, or replace the entire mock with an `<iframe>` or screenshots — the outer frame and section wrapper stay intact.

---

## Placeholder Indicators

- Section subtitle explicitly mentions "early preview"
- A small `// preview — not final UI` badge rendered inside the browser chrome bar (right side, muted text)

---

## Nav Integration

- Add `<li><a href="#demo">Demo</a></li>` to the nav links (desktop + mobile drawer)
- Section gets `id="demo"` so scroll-spy active highlighting works

---

## Responsive Behavior

- **≥ 900px:** Full sidebar + content layout, perspective tilt on browser frame
- **< 900px:** Sidebar collapses to a horizontal icon-only tab bar above the content area; perspective tilt removed; frame simplified to just a top chrome bar

---

## Implementation Notes

- All styles scoped to the demo section via `.demo-*` class prefix — no impact on existing styles
- No external dependencies — pure HTML/CSS/JS inline with the rest of `index.html`
- The section `<script>` block is self-contained; `DEMO_DATA` is block-scoped with `const` inside an IIFE
