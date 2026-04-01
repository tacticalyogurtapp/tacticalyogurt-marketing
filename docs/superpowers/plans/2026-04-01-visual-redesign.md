# Visual Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the blue palette with violet/amber, restructure the hero into a split layout with a dashboard mock, and swap the pill badge for a monospace status tag.

**Architecture:** All changes are in `index.html`. CSS variable updates propagate the color change site-wide automatically. The hero section gets a full HTML and CSS replacement — the rest of the page structure is untouched.

**Tech Stack:** Vanilla HTML/CSS. No build step, no dependencies.

**Design spec:** `docs/superpowers/specs/2026-04-01-visual-redesign-design.md`

---

## File Structure

| File | Change |
|---|---|
| `index.html` | CSS variables, hardcoded colors, button gradients, hero HTML + CSS |
| `preview-redesign-colors.html` | Delete (preview artifact) |
| `preview-redesign-hero.html` | Delete (preview artifact) |
| `preview-redesign-badge.html` | Delete (preview artifact) |

---

### Task 1: Update CSS variables and hardcoded background colors

**Files:**
- Modify: `index.html` lines 10–23 (`:root` block), line 39 (nav bg), line 58 (nav-mobile bg), line 68–69 (hero grid), line 73 (hero-glow), line 95 (photo-break-overlay)

- [ ] **Step 1: Replace the `:root` block**

Find:
```css
    :root {
      --bg:        #0a0c10;
      --bg2:       #0f1117;
      --card:      #13171f;
      --border:    rgba(255,255,255,0.07);
      --blue:      #3b6aff;
      --blue-glow: rgba(59,106,255,0.25);
      --green:     #2fd87a;
      --text:      #e8ecf4;
      --muted:     #6b7280;
      --mono:      'JetBrains Mono', monospace;
      --sans:      'Figtree', sans-serif;
      --display:   'Outfit', sans-serif;
    }
```
Replace with:
```css
    :root {
      --bg:           #0f0a1e;
      --bg2:          #140e24;
      --card:         #160f26;
      --border:       rgba(167,139,250,0.1);
      --blue:         #7c3aed;
      --blue-glow:    rgba(124,58,237,0.25);
      --green:        #4ade80;
      --violet:       #7c3aed;
      --violet-light: #a78bfa;
      --amber:        #ea580c;
      --amber-light:  #fb923c;
      --text:         #e8ecf4;
      --muted:        #6b7280;
      --mono:         'JetBrains Mono', monospace;
      --sans:         'Figtree', sans-serif;
      --display:      'Outfit', sans-serif;
    }
```

- [ ] **Step 2: Update nav background color**

Find:
```css
      background: rgba(10,12,16,.92); backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
    }
```
Replace with:
```css
      background: rgba(15,10,30,.92); backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
    }
```

- [ ] **Step 3: Update mobile nav background color**

Find:
```css
    .nav-mobile { display: none; position: fixed; top: 64px; left: 0; right: 0; background: rgba(10,12,16,.97);
```
Replace with:
```css
    .nav-mobile { display: none; position: fixed; top: 64px; left: 0; right: 0; background: rgba(15,10,30,.97);
```

- [ ] **Step 4: Update hero grid pattern color**

Find:
```css
      background-image: linear-gradient(rgba(59,106,255,.04) 1px,transparent 1px), linear-gradient(90deg,rgba(59,106,255,.04) 1px,transparent 1px);
```
Replace with:
```css
      background-image: linear-gradient(rgba(124,58,237,.04) 1px,transparent 1px), linear-gradient(90deg,rgba(124,58,237,.04) 1px,transparent 1px);
```

- [ ] **Step 5: Update hero glow color**

Find:
```css
    .hero-glow { position: absolute; width: 700px; height: 400px; background: radial-gradient(ellipse,rgba(59,106,255,.18) 0%,transparent 70%); top: 10%; left: 50%; transform: translateX(-50%); pointer-events: none; filter: blur(40px); }
```
Replace with:
```css
    .hero-glow { position: absolute; width: 700px; height: 400px; background: radial-gradient(ellipse,rgba(124,58,237,.18) 0%,transparent 70%); top: 10%; left: 50%; transform: translateX(-50%); pointer-events: none; filter: blur(40px); }
```

- [ ] **Step 6: Update photo-break overlay colors**

Find:
```css
    .photo-break-overlay { position: absolute; inset: 0; background: linear-gradient(to right,rgba(10,12,16,1) 0%,rgba(10,12,16,.25) 35%,rgba(10,12,16,.25) 65%,rgba(10,12,16,1) 100%), linear-gradient(to bottom,rgba(10,12,16,.5) 0%,transparent 20%,transparent 80%,rgba(10,12,16,.7) 100%); display: flex; align-items: center; justify-content: center; }
```
Replace with:
```css
    .photo-break-overlay { position: absolute; inset: 0; background: linear-gradient(to right,rgba(15,10,30,1) 0%,rgba(15,10,30,.25) 35%,rgba(15,10,30,.25) 65%,rgba(15,10,30,1) 100%), linear-gradient(to bottom,rgba(15,10,30,.5) 0%,transparent 20%,transparent 80%,rgba(15,10,30,.7) 100%); display: flex; align-items: center; justify-content: center; }
```

- [ ] **Step 7: Verify in browser**

Open `index.html`. Confirm:
- Background is deep purple-black (not blue-black)
- Nav bar has purple-tinted dark background
- Nav border is subtly purple-tinted
- Scroll to a photo break — edges should fade to the new dark purple

- [ ] **Step 8: Commit**

```bash
git add index.html
git commit -m "feat: update color variables and hardcoded bg colors to violet palette"
```

---

### Task 2: Update button and nav CTA gradients

**Files:**
- Modify: `index.html` — `.btn-primary`, `.btn-primary:hover`, `.nav-cta`, `.nav-cta:hover`, `h1 span`, `.hero-badge`

- [ ] **Step 1: Update `.btn-primary`**

Find:
```css
    .btn-primary { background: var(--blue); color: #fff; padding: .8rem 2rem; border-radius: 8px; font-weight: 500; font-size: .95rem; text-decoration: none; transition: all .2s; box-shadow: 0 4px 24px rgba(59,106,255,.4); }
    .btn-primary:hover { background: #4d7aff; transform: translateY(-2px); box-shadow: 0 8px 32px rgba(59,106,255,.5); }
```
Replace with:
```css
    .btn-primary { background: linear-gradient(90deg, #7c3aed, #ea580c); color: #fff; padding: .8rem 2rem; border-radius: 8px; font-weight: 500; font-size: .95rem; text-decoration: none; transition: all .2s; box-shadow: 0 4px 24px rgba(124,58,237,.4); }
    .btn-primary:hover { filter: brightness(1.15); transform: translateY(-2px); box-shadow: 0 8px 32px rgba(124,58,237,.5); }
```

- [ ] **Step 2: Update `.nav-cta`**

Find:
```css
    .nav-cta { background: var(--blue); color: #fff; padding: .45rem 1.1rem; border-radius: 6px; font-size: .8rem; font-weight: 500; text-decoration: none; transition: background .2s, box-shadow .2s; white-space: nowrap; flex-shrink: 0; margin-left: 1rem; }
    .nav-cta:hover { background: #4d7aff; box-shadow: 0 0 20px var(--blue-glow); }
```
Replace with:
```css
    .nav-cta { background: linear-gradient(90deg, #7c3aed, #ea580c); color: #fff; padding: .45rem 1.1rem; border-radius: 6px; font-size: .8rem; font-weight: 500; text-decoration: none; transition: filter .2s, box-shadow .2s; white-space: nowrap; flex-shrink: 0; margin-left: 1rem; }
    .nav-cta:hover { filter: brightness(1.15); box-shadow: 0 0 20px var(--blue-glow); }
```

- [ ] **Step 3: Update `h1 span` gradient**

Find:
```css
    h1 span { background: linear-gradient(135deg,#3b6aff 0%,#7da4ff 50%,#a0c0ff 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
```
Replace with:
```css
    h1 span { background: linear-gradient(90deg, #a78bfa 0%, #fb923c 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
```

- [ ] **Step 4: Update `.hero-badge` to use violet colors**

Find:
```css
    .hero-badge { display: inline-flex; align-items: center; gap: .5rem; background: rgba(59,106,255,.12); border: 1px solid rgba(59,106,255,.3); color: #7da4ff; font-family: var(--mono); font-size: .75rem; padding: .35rem .85rem; border-radius: 100px; margin-bottom: 1.75rem; letter-spacing: .05em; animation: fadeUp .6s ease both; }
    .hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--blue); border-radius: 50%; box-shadow: 0 0 6px var(--blue); }
```
Replace with:
```css
    .hero-badge { display: inline-flex; align-items: center; gap: .5rem; background: rgba(124,58,237,.12); border: 1px solid rgba(124,58,237,.3); color: #a78bfa; font-family: var(--mono); font-size: .75rem; padding: .35rem .85rem; border-radius: 100px; margin-bottom: 1.75rem; letter-spacing: .05em; animation: fadeUp .6s ease both; }
    .hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--violet-light); border-radius: 50%; box-shadow: 0 0 6px var(--violet-light); }
```

- [ ] **Step 5: Verify in browser**

Open `index.html`. Confirm:
- "Start Free Trial" button in hero shows violet→amber gradient
- "Get Started" nav button shows the same gradient
- Headline "print farm." text shows violet→amber gradient
- Hero badge is now violet-tinted (not blue)

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: update buttons and headline to violet/amber gradient"
```

---

### Task 3: Restructure hero HTML

**Files:**
- Modify: `index.html` — the `<!-- HERO -->` section (lines ~280–289)

- [ ] **Step 1: Replace hero HTML**

Find:
```html
<!-- HERO -->
<div class="hero">
  <div class="hero-glow"></div>
  <span class="hero-badge">3D Print Farm Management — Simplified</span>
  <h1>Command your<br><span>print farm.</span><br>Not your spreadsheets.</h1>
  <p class="hero-sub">TacticalYogurt is the all-in-one operations platform for 3D print farms — track filament, manage printers, fulfill orders, and grow your business from a single dashboard.</p>
  <div class="hero-actions">
    <a href="#pricing" class="btn-primary">Start Free Trial</a>
    <a href="#features" class="btn-ghost">Explore Features →</a>
  </div>
</div>
```

Replace with:
```html
<!-- HERO -->
<div class="hero">
  <div class="hero-glow"></div>
  <div class="hero-inner">

    <!-- Left: text -->
    <div class="hero-text">
      <h1>Command your<br><span>print farm.</span><br>Not your spreadsheets.</h1>
      <div class="hero-tag">
        <span class="hero-tag-dot"></span>
        All in one inventory and print farm management
      </div>
      <p class="hero-sub">Track every spool, manage every printer, fulfill every order — from one dashboard built for serious makers.</p>
      <div class="hero-actions">
        <a href="#" class="btn-primary" onclick="event.preventDefault(); openModal()">Join Early Access — It's Free</a>
        <a href="#how-it-works" class="btn-ghost">See how it works →</a>
      </div>
      <div class="hero-stats">
        <div class="hero-stat">
          <div class="hero-stat-num">16+</div>
          <div class="hero-stat-label">Part categories tracked</div>
        </div>
        <div class="hero-stat">
          <div class="hero-stat-num">5</div>
          <div class="hero-stat-label">Marketplace integrations</div>
        </div>
        <div class="hero-stat">
          <div class="hero-stat-num">∞</div>
          <div class="hero-stat-label">Printers supported</div>
        </div>
      </div>
    </div>

    <!-- Right: dashboard mock -->
    <div class="hero-visual">
      <div class="dashboard-mock">
        <div class="mock-topbar">
          <span class="mock-dot" style="background:#ff5f57"></span>
          <span class="mock-dot" style="background:#febc2e"></span>
          <span class="mock-dot" style="background:#28c840"></span>
          <span class="mock-title">tacticalyogurt — dashboard</span>
        </div>
        <div class="mock-body">
          <div class="mock-stat-row">
            <div class="mock-stat-card">
              <div class="mock-stat-label">// SPOOLS</div>
              <div class="mock-stat-num violet">34</div>
              <div class="mock-stat-sub">12 materials</div>
            </div>
            <div class="mock-stat-card">
              <div class="mock-stat-label">// PRINTING</div>
              <div class="mock-stat-num amber">4/6</div>
              <div class="mock-stat-sub">printers active</div>
            </div>
            <div class="mock-stat-card">
              <div class="mock-stat-label">// ORDERS</div>
              <div class="mock-stat-num green">8</div>
              <div class="mock-stat-sub">pending fulfillment</div>
            </div>
          </div>
          <div class="mock-section">
            <div class="mock-section-label">// FILAMENT INVENTORY</div>
            <div class="mock-spool-row">
              <span class="mock-spool-dot" style="background:#a78bfa"></span>
              <span class="mock-spool-name">Bambu PLA Matte — Purple</span>
              <span class="mock-bar-wrap"><span class="mock-bar" style="width:78%;background:#a78bfa"></span></span>
              <span class="mock-pct">78%</span>
            </div>
            <div class="mock-spool-row">
              <span class="mock-spool-dot" style="background:#fb923c"></span>
              <span class="mock-spool-name">eSun PETG — Amber</span>
              <span class="mock-bar-wrap"><span class="mock-bar" style="width:42%;background:#fb923c"></span></span>
              <span class="mock-pct">42%</span>
            </div>
            <div class="mock-spool-row">
              <span class="mock-spool-dot" style="background:#4ade80"></span>
              <span class="mock-spool-name">Polymaker PLA — Silk Green</span>
              <span class="mock-bar-wrap"><span class="mock-bar" style="width:91%;background:#4ade80"></span></span>
              <span class="mock-pct">91%</span>
            </div>
          </div>
          <div class="mock-section">
            <div class="mock-section-label">// PRINTER FLEET</div>
            <div class="mock-printer-row">
              <span class="mock-status-dot" style="background:#4ade80;box-shadow:0 0 6px #4ade80"></span>
              <span class="mock-printer-name">Bambu X1C #1</span>
              <span class="mock-printer-job">grid-clip-v3.3mf</span>
              <span class="mock-printer-eta">1h 24m</span>
            </div>
            <div class="mock-printer-row">
              <span class="mock-status-dot" style="background:#4ade80;box-shadow:0 0 6px #4ade80"></span>
              <span class="mock-printer-name">Prusa MK4 #2</span>
              <span class="mock-printer-job">bracket-mount.3mf</span>
              <span class="mock-printer-eta">3h 02m</span>
            </div>
            <div class="mock-printer-row">
              <span class="mock-status-dot" style="background:#4b5563"></span>
              <span class="mock-printer-name">Bambu A1 #3</span>
              <span class="mock-printer-job" style="color:#4b5563">idle</span>
              <span class="mock-printer-eta" style="color:#4b5563">—</span>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</div>
```

- [ ] **Step 2: Verify HTML structure in browser**

Open `index.html`. The hero will look unstyled (text stacked vertically, no grid) — that's expected. Confirm:
- All text content is present: headline, tag line, subtext, two CTA buttons, three stats
- Dashboard mock panel is present below the text
- No console errors

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: restructure hero HTML to split layout with dashboard mock"
```

---

### Task 4: Add hero split CSS and dashboard mock styles

**Files:**
- Modify: `index.html` — replace `.hero` CSS block and add new hero styles before `</style>`

- [ ] **Step 1: Replace the existing hero CSS block**

Find:
```css
    /* HERO */
    .hero { position: relative; min-height: 100vh; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 8rem 2rem 5rem; overflow: hidden; }
    .hero::after {
      content: ''; position: absolute; inset: 0;
      background-image: linear-gradient(rgba(124,58,237,.04) 1px,transparent 1px), linear-gradient(90deg,rgba(124,58,237,.04) 1px,transparent 1px);
      background-size: 48px 48px;
      mask-image: radial-gradient(ellipse 80% 60% at 50% 40%,black 30%,transparent 100%);
      pointer-events: none;
    }
    .hero-glow { position: absolute; width: 700px; height: 400px; background: radial-gradient(ellipse,rgba(124,58,237,.18) 0%,transparent 70%); top: 10%; left: 50%; transform: translateX(-50%); pointer-events: none; filter: blur(40px); }
    .hero-badge { display: inline-flex; align-items: center; gap: .5rem; background: rgba(124,58,237,.12); border: 1px solid rgba(124,58,237,.3); color: #a78bfa; font-family: var(--mono); font-size: .75rem; padding: .35rem .85rem; border-radius: 100px; margin-bottom: 1.75rem; letter-spacing: .05em; animation: fadeUp .6s ease both; }
    .hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--violet-light); border-radius: 50%; box-shadow: 0 0 6px var(--violet-light); }
    h1 { font-family: var(--display); font-size: clamp(2rem,5vw,3.75rem); font-weight: 700; line-height: 1.1; letter-spacing: -.025em; max-width: 820px; animation: fadeUp .7s .1s ease both; }
    h1 span { background: linear-gradient(90deg, #a78bfa 0%, #fb923c 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
    .hero-sub { margin-top: 1.5rem; font-size: 1.1rem; color: var(--muted); max-width: 540px; font-weight: 300; line-height: 1.75; animation: fadeUp .7s .2s ease both; }
    .hero-actions { display: flex; gap: 1rem; margin-top: 2.5rem; animation: fadeUp .7s .3s ease both; flex-wrap: wrap; justify-content: center; }
```

Replace with:
```css
    /* HERO */
    .hero { position: relative; min-height: 100vh; overflow: hidden; display: flex; align-items: center; padding: 80px 0 0; }
    .hero::after {
      content: ''; position: absolute; inset: 0;
      background-image: linear-gradient(rgba(124,58,237,.04) 1px,transparent 1px), linear-gradient(90deg,rgba(124,58,237,.04) 1px,transparent 1px);
      background-size: 48px 48px;
      mask-image: radial-gradient(ellipse 80% 60% at 30% 50%,black 30%,transparent 100%);
      pointer-events: none;
    }
    .hero-glow {
      position: absolute; width: 600px; height: 600px;
      background: radial-gradient(ellipse at 20% 50%, rgba(124,58,237,.15) 0%, transparent 50%),
                  radial-gradient(ellipse at 80% 20%, rgba(234,88,12,.08) 0%, transparent 40%);
      inset: 0; pointer-events: none; filter: blur(40px);
    }
    .hero-inner {
      display: grid; grid-template-columns: 1fr 1fr;
      align-items: center; gap: 4rem;
      max-width: 1200px; width: 100%; margin: 0 auto;
      padding: 5rem 3rem; position: relative; z-index: 1;
    }
    .hero-text { display: flex; flex-direction: column; }
    h1 { font-family: var(--display); font-size: clamp(2rem,3.5vw,3.25rem); font-weight: 700; line-height: 1.1; letter-spacing: -.025em; animation: fadeUp .7s .1s ease both; }
    h1 span { background: linear-gradient(90deg, #a78bfa 0%, #fb923c 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
    .hero-tag {
      display: inline-flex; align-items: center; gap: .6rem;
      border: 1px solid rgba(255,255,255,.1); border-radius: 6px;
      padding: .4rem .85rem; font-family: var(--mono); font-size: .72rem;
      color: #9ca3af; margin-top: 1rem; margin-bottom: 1rem; align-self: flex-start;
    }
    .hero-tag-dot {
      width: 6px; height: 6px; border-radius: 50%; flex-shrink: 0;
      background: var(--amber-light); box-shadow: 0 0 6px var(--amber-light);
      animation: pulse 2s ease-in-out infinite;
    }
    .hero-sub { font-size: 1rem; color: var(--muted); max-width: 440px; font-weight: 300; line-height: 1.75; animation: fadeUp .7s .2s ease both; }
    .hero-actions { display: flex; gap: 1rem; margin-top: 2rem; animation: fadeUp .7s .3s ease both; flex-wrap: wrap; }
    .hero-stats { display: flex; gap: 2rem; margin-top: 2.5rem; flex-wrap: wrap; }
    .hero-stat-num {
      font-family: var(--display); font-size: 1.5rem; font-weight: 700;
      background: linear-gradient(90deg, #a78bfa, #fb923c);
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    }
    .hero-stat-label { font-size: .72rem; color: var(--muted); margin-top: .15rem; line-height: 1.4; max-width: 80px; }
```

- [ ] **Step 2: Add dashboard mock CSS before `</style>`**

Find the closing `</style>` tag. Insert the following block immediately before it:

```css
    /* HERO DASHBOARD MOCK */
    .hero-visual { position: relative; }
    .dashboard-mock {
      background: rgba(255,255,255,.02);
      border: 1px solid rgba(167,139,250,.12);
      border-radius: 14px; overflow: hidden;
      box-shadow: 0 32px 80px rgba(0,0,0,.5), 0 0 0 1px rgba(167,139,250,.08);
    }
    .mock-topbar {
      background: rgba(255,255,255,.03);
      border-bottom: 1px solid rgba(255,255,255,.05);
      padding: .65rem 1rem;
      display: flex; align-items: center; gap: .5rem;
    }
    .mock-dot { width: 10px; height: 10px; border-radius: 50%; display: inline-block; }
    .mock-title { font-size: .7rem; color: #4b5563; font-family: var(--mono); margin-left: auto; }
    .mock-body { padding: 1rem; display: flex; flex-direction: column; gap: .85rem; }
    .mock-stat-row { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: .6rem; }
    .mock-stat-card {
      background: rgba(255,255,255,.02); border: 1px solid rgba(255,255,255,.05);
      border-radius: 8px; padding: .65rem .75rem;
    }
    .mock-stat-card .mock-stat-label { font-size: .6rem; color: #4b5563; font-family: var(--mono); margin-bottom: .3rem; }
    .mock-stat-card .mock-stat-num { font-size: 1.1rem; font-weight: 700; font-family: var(--display); }
    .mock-stat-card .mock-stat-num.violet { color: #a78bfa; }
    .mock-stat-card .mock-stat-num.amber { color: #fb923c; }
    .mock-stat-card .mock-stat-num.green { color: #4ade80; }
    .mock-stat-card .mock-stat-sub { font-size: .62rem; color: #4b5563; margin-top: .15rem; }
    .mock-section { display: flex; flex-direction: column; gap: .35rem; }
    .mock-section-label { font-size: .6rem; color: #4b5563; font-family: var(--mono); letter-spacing: .05em; margin-bottom: .1rem; }
    .mock-spool-row {
      background: rgba(255,255,255,.02); border: 1px solid rgba(255,255,255,.04);
      border-radius: 6px; padding: .45rem .75rem;
      display: flex; align-items: center; gap: .6rem;
    }
    .mock-spool-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; display: inline-block; }
    .mock-spool-name { font-size: .72rem; flex: 1; }
    .mock-bar-wrap { flex: 2; height: 3px; background: rgba(255,255,255,.05); border-radius: 2px; overflow: hidden; display: inline-block; }
    .mock-bar { height: 100%; border-radius: 2px; display: block; }
    .mock-pct { font-size: .65rem; color: #4b5563; width: 28px; text-align: right; font-family: var(--mono); }
    .mock-printer-row {
      background: rgba(255,255,255,.02); border: 1px solid rgba(255,255,255,.04);
      border-radius: 6px; padding: .45rem .75rem;
      display: flex; align-items: center; gap: .6rem;
    }
    .mock-status-dot { width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0; display: inline-block; }
    .mock-printer-name { font-size: .72rem; flex: 1; }
    .mock-printer-job { font-size: .65rem; color: #6b7280; font-family: var(--mono); }
    .mock-printer-eta { font-size: .65rem; color: #a78bfa; margin-left: auto; }
    @media (max-width: 900px) {
      .hero-inner { grid-template-columns: 1fr; padding: 3rem 1.5rem; }
      .hero-visual { display: none; }
      h1 { font-size: clamp(2rem, 6vw, 3rem); }
    }
```

- [ ] **Step 3: Verify in browser**

Open `index.html`. Scroll to the top. Confirm:
- Hero is a two-column split layout — text left, dashboard mock right
- Headline is left-aligned, gradient "print farm." text in violet→amber
- Status tag sits below the headline with amber glowing dot and correct copy
- Dashboard mock shows stat cards, spool rows, and printer rows
- Three stats (16+, 5, ∞) with gradient numbers appear below the CTA buttons
- On mobile (resize to < 900px): single column, dashboard mock hidden
- No overlap with nav bar

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add split hero CSS and dashboard mock styles"
```

---

### Task 5: Delete preview files and push

**Files:**
- Delete: `preview-redesign-colors.html`, `preview-redesign-hero.html`, `preview-redesign-badge.html`

- [ ] **Step 1: Delete preview files**

```bash
rm "I:/Git/tacticalyogurt-marketing/preview-redesign-colors.html"
rm "I:/Git/tacticalyogurt-marketing/preview-redesign-hero.html"
rm "I:/Git/tacticalyogurt-marketing/preview-redesign-badge.html"
```

- [ ] **Step 2: Full page walkthrough in browser**

Open `index.html` locally and verify:
1. Background is deep violet-black throughout the page
2. Hero is split layout with dashboard mock visible on desktop
3. Status tag below headline: amber dot + "All in one inventory and print farm management"
4. Headline gradient: violet → amber
5. CTA buttons show violet → amber gradient
6. Nav "Get Started" button shows violet → amber gradient
7. Photo break edges fade to the new dark purple (not blue-black)
8. Features section, Pricing, Compare — all inherit the new card/border colors
9. Modal opens from any CTA button
10. On mobile: hero stacks to single column, mock hidden

- [ ] **Step 3: Commit and push**

```bash
git add index.html
git commit -m "chore: remove redesign preview files"
git push origin main
```
