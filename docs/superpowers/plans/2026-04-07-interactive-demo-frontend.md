# Interactive App Demo Section — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add an interactive app demo section to `index.html`, placed between the stats strip and the first photo break, showing a macOS-style browser frame wrapping a TacticalYogurt app shell with 4 clickable sidebar tabs (Dashboard, Printer Fleet, Filament Inventory, Print Jobs).

**Architecture:** All new code is self-contained inside `index.html` — CSS added to the existing `<style>` block, HTML inserted at one location, JS added to the existing `<script>` block as an IIFE. All mock data lives in a single `DEMO_DATA` object at the top of the IIFE for easy future editing. Tab switching uses a simple `demoSwitch(tab)` function wired to `onclick` attributes; no framework needed.

**Tech Stack:** Vanilla HTML/CSS/JS, no external dependencies. IntersectionObserver for scroll-triggered auto-cycle.

---

## File Map

| File | Change |
|------|--------|
| `index.html` (lines ~210–357, `<style>`) | Add `/* DEMO SECTION */` CSS block |
| `index.html` (lines ~516–518, between stats strip and first photo break) | Insert `<!-- INTERACTIVE DEMO -->` HTML |
| `index.html` (lines ~1170–1244, `<script>`) | Append IIFE with DEMO_DATA, renderers, demoSwitch, auto-cycle |
| `index.html` (line ~366, nav links) | Add Demo nav item |
| `index.html` (line ~1186, sections array) | Add `demo` to scroll-spy sections |
| `index.html` (line ~387, mobile nav drawer) | Add Demo mobile nav link |

---

### Task 1: Add CSS for the demo section

**Files:**
- Modify: `index.html` — inside `<style>` block, after the `/* ANIMATIONS */` comment (around line 210)

- [ ] **Step 1: Locate insertion point**

Open `index.html`. Find the line that reads:
```css
    /* ANIMATIONS */
    @keyframes fadeUp { from{opacity:0;transform:translateY(20px)} to{opacity:1;transform:translateY(0)} }
```
You will insert the new CSS block immediately before this line.

- [ ] **Step 2: Insert the CSS block**

Insert the following CSS immediately before `/* ANIMATIONS */`:

```css
    /* DEMO SECTION */
    .demo-section { position: relative; z-index: 1; padding: 6rem 2rem; }
    .demo-header { max-width: 1100px; margin: 0 auto 3rem; }
    .demo-frame-wrap { max-width: 1100px; margin: 0 auto; }
    .demo-browser-frame {
      border-radius: 12px; overflow: hidden;
      border: 1px solid var(--border);
      box-shadow: 0 32px 80px rgba(0,0,0,.6);
      transform: perspective(1200px) rotateY(-3deg) rotateX(2deg);
      transition: transform .4s ease;
    }
    .demo-browser-frame:hover { transform: perspective(1200px) rotateY(-1deg) rotateX(1deg); }
    .demo-chrome {
      background: #0d1018; border-bottom: 1px solid var(--border);
      padding: .65rem 1rem; display: flex; align-items: center; gap: .75rem;
    }
    .demo-tl-wrap { display: flex; gap: .4rem; }
    .demo-tl { width: 10px; height: 10px; border-radius: 50%; }
    .demo-url {
      flex: 1; background: rgba(255,255,255,.05); border: 1px solid var(--border);
      border-radius: 6px; padding: .25rem .75rem;
      font-family: var(--mono); font-size: .68rem; color: var(--muted);
    }
    .demo-preview-tag { font-family: var(--mono); font-size: .62rem; color: #374151; white-space: nowrap; }
    .demo-app-shell { display: flex; height: 480px; background: var(--bg); }
    .demo-sidebar {
      width: 200px; flex-shrink: 0; background: rgba(14,9,28,.95);
      border-right: 1px solid var(--border); display: flex; flex-direction: column; padding: 1.25rem 0;
    }
    .demo-sidebar-brand {
      display: flex; align-items: center; gap: .5rem;
      padding: 0 1rem 1.25rem; border-bottom: 1px solid var(--border);
      font-family: var(--display); font-size: .85rem; font-weight: 600; margin-bottom: .5rem;
    }
    .demo-sidebar-brand-text {
      background: linear-gradient(90deg,#a78bfa,#fb923c);
      -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    }
    .demo-nav-item {
      display: flex; align-items: center; gap: .65rem;
      padding: .55rem 1rem; margin: .1rem .5rem; border-radius: 6px;
      font-size: .8rem; color: var(--muted); cursor: pointer;
      border: none; background: none; width: calc(100% - 1rem); text-align: left;
      transition: color .15s, background .15s; font-family: var(--sans);
    }
    .demo-nav-item:hover { color: var(--text); background: rgba(255,255,255,.04); }
    .demo-nav-item.active { color: var(--text); background: rgba(124,58,237,.15); }
    .demo-nav-item.active svg { stroke: var(--violet-light); }
    .demo-content {
      flex: 1; overflow-y: auto; padding: 1.5rem;
      transition: opacity .15s ease, transform .15s ease;
    }
    .demo-content.fade-out-state { opacity: 0; transform: translateY(6px); }
    .demo-stat-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: .75rem; margin-bottom: 1.25rem; }
    .demo-stat-card {
      background: rgba(255,255,255,.04); border: 1px solid var(--border);
      border-radius: 8px; padding: .85rem 1rem;
    }
    .demo-stat-label { font-size: .62rem; color: var(--muted); font-family: var(--mono); margin-bottom: .35rem; letter-spacing: .05em; }
    .demo-stat-num { font-family: var(--display); font-size: 1.4rem; font-weight: 700; }
    .demo-stat-sub { font-size: .62rem; color: var(--muted); margin-top: .15rem; }
    .demo-section-title { font-size: .65rem; color: var(--muted); font-family: var(--mono); letter-spacing: .08em; margin-bottom: .6rem; }
    .demo-activity-item {
      display: flex; align-items: flex-start; gap: .65rem;
      padding: .5rem 0; border-bottom: 1px solid rgba(255,255,255,.04); font-size: .78rem;
    }
    .demo-activity-item:last-child { border-bottom: none; }
    .demo-activity-dot { width: 6px; height: 6px; border-radius: 50%; flex-shrink: 0; margin-top: 4px; }
    .demo-activity-text { flex: 1; color: var(--text); line-height: 1.4; }
    .demo-activity-time { font-family: var(--mono); font-size: .65rem; color: var(--muted); white-space: nowrap; }
    .demo-table { width: 100%; border-collapse: collapse; }
    .demo-table th {
      font-size: .62rem; font-family: var(--mono); color: var(--muted); letter-spacing: .08em;
      text-align: left; padding: .4rem .5rem; border-bottom: 1px solid var(--border);
    }
    .demo-table td { font-size: .78rem; padding: .6rem .5rem; border-bottom: 1px solid rgba(255,255,255,.04); vertical-align: middle; }
    .demo-table tr:last-child td { border-bottom: none; }
    .demo-status-dot { width: 7px; height: 7px; border-radius: 50%; display: inline-block; flex-shrink: 0; }
    .demo-status-dot.printing { background: var(--green); box-shadow: 0 0 6px var(--green); animation: pulse 2s ease-in-out infinite; }
    .demo-status-dot.idle { background: #374151; }
    .demo-job-name { font-family: var(--mono); font-size: .72rem; color: var(--muted); }
    .demo-eta { font-family: var(--mono); font-size: .72rem; color: var(--violet-light); }
    .demo-bar-wrap { width: 80px; height: 3px; background: rgba(255,255,255,.07); border-radius: 2px; overflow: hidden; display: inline-block; }
    .demo-bar { height: 100%; border-radius: 2px; background: var(--violet-light); width: 0; transition: width .4s ease; }
    .demo-spool-row {
      display: flex; align-items: center; gap: .65rem;
      padding: .55rem .5rem; border-bottom: 1px solid rgba(255,255,255,.04);
    }
    .demo-spool-row:last-child { border-bottom: none; }
    .demo-spool-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
    .demo-spool-name { flex: 1; font-size: .8rem; }
    .demo-spool-variant { font-size: .7rem; color: var(--muted); }
    .demo-spool-bar-wrap { width: 100px; height: 4px; background: rgba(255,255,255,.07); border-radius: 2px; overflow: hidden; }
    .demo-spool-bar { height: 100%; border-radius: 2px; width: 0; transition: width .4s ease; }
    .demo-spool-pct { font-family: var(--mono); font-size: .68rem; color: var(--muted); width: 32px; text-align: right; }
    .demo-low-badge {
      font-size: .6rem; font-family: var(--mono); color: var(--amber-light);
      background: rgba(251,146,60,.1); border: 1px solid rgba(251,146,60,.25);
      border-radius: 4px; padding: .15rem .4rem; white-space: nowrap;
    }
    .demo-status-badge { font-size: .65rem; font-family: var(--mono); padding: .2rem .5rem; border-radius: 4px; letter-spacing: .05em; }
    .demo-status-badge.completed { background: rgba(74,222,128,.1); color: var(--green); border: 1px solid rgba(74,222,128,.2); }
    .demo-status-badge.in-progress { background: rgba(251,146,60,.1); color: var(--amber-light); border: 1px solid rgba(251,146,60,.2); }
    .demo-status-badge.failed { background: rgba(239,68,68,.1); color: #f87171; border: 1px solid rgba(239,68,68,.2); }
    .demo-stars { display: flex; gap: 2px; }
    .demo-star { font-size: .7rem; }
    .demo-star.filled { color: var(--amber-light); }
    .demo-star.empty { color: #374151; }
    @media (max-width:900px) {
      .demo-browser-frame { transform: none; }
      .demo-app-shell { flex-direction: column; height: auto; }
      .demo-sidebar {
        width: 100%; flex-direction: row; align-items: center;
        padding: .5rem; gap: .25rem; border-right: none; border-bottom: 1px solid var(--border);
        overflow-x: auto;
      }
      .demo-sidebar-brand { display: none; }
      .demo-nav-item { padding: .4rem .6rem; gap: .3rem; font-size: .7rem; margin: 0; width: auto; white-space: nowrap; }
      .demo-content { padding: 1rem; }
      .demo-stat-grid { grid-template-columns: 1fr 1fr; }
      .demo-section { padding: 4rem 1.25rem; }
    }

```

- [ ] **Step 3: Open `index.html` in browser and verify no style breakage**

The page should look identical to before this task — no new visible element yet. Check that hero, nav, stats strip, and features sections all render correctly.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add demo section CSS"
```

---

### Task 2: Insert the demo section HTML

**Files:**
- Modify: `index.html` — insert between the closing `</div>` of `<!-- STATS -->` and `<!-- PHOTO BREAK: PRINT FARM -->`

- [ ] **Step 1: Locate insertion point**

Find this exact line in `index.html` (around line 516):
```html
</div>

<!-- PHOTO BREAK: PRINT FARM -->
```
The blank line between `</div>` (end of stats strip) and the photo break comment is where the new section goes.

- [ ] **Step 2: Insert the HTML**

Insert the following between the stats strip closing `</div>` and `<!-- PHOTO BREAK: PRINT FARM -->`:

```html

<!-- INTERACTIVE DEMO -->
<div id="demo" class="demo-section">
  <div class="demo-header fade-in">
    <div class="section-label">// see it in action</div>
    <h2 class="section-title">The command center for your farm.</h2>
    <p class="section-sub">A preview of what's coming — one dashboard for every part of your operation.</p>
  </div>
  <div class="demo-frame-wrap fade-in">
    <div class="demo-browser-frame">
      <!-- Browser chrome bar -->
      <div class="demo-chrome">
        <div class="demo-tl-wrap">
          <span class="demo-tl" style="background:#ff5f57"></span>
          <span class="demo-tl" style="background:#febc2e"></span>
          <span class="demo-tl" style="background:#28c840"></span>
        </div>
        <div class="demo-url">app.tacticalyogurt.com/<span id="demo-url-path">dashboard</span></div>
        <span class="demo-preview-tag">// preview — not final UI</span>
      </div>
      <!-- App shell -->
      <div class="demo-app-shell">
        <!-- Sidebar -->
        <div class="demo-sidebar">
          <div class="demo-sidebar-brand">
            <div class="nav-dot"></div>
            <span class="demo-sidebar-brand-text">TacticalYogurt</span>
          </div>
          <button class="demo-nav-item active" data-tab="dashboard" onclick="demoSwitch('dashboard')">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="9"/><rect x="14" y="3" width="7" height="5"/><rect x="14" y="12" width="7" height="9"/><rect x="3" y="16" width="7" height="5"/></svg>
            Dashboard
          </button>
          <button class="demo-nav-item" data-tab="fleet" onclick="demoSwitch('fleet')">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 6 2 18 2 18 9"/><path d="M6 18H4a2 2 0 0 1-2-2v-5a2 2 0 0 1 2-2h16a2 2 0 0 1 2 2v5a2 2 0 0 1-2 2h-2"/><rect x="6" y="14" width="12" height="8"/></svg>
            Printer Fleet
          </button>
          <button class="demo-nav-item" data-tab="inventory" onclick="demoSwitch('inventory')">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16Z"/><path d="m3.29 7 8.71 5 8.71-5"/><line x1="12" y1="22" x2="12" y2="12"/></svg>
            Filament Inventory
          </button>
          <button class="demo-nav-item" data-tab="jobs" onclick="demoSwitch('jobs')">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1Z"/></svg>
            Print Jobs
          </button>
        </div>
        <!-- Main content — populated by JS -->
        <div class="demo-content" id="demo-content"></div>
      </div>
    </div>
  </div>
</div>

```

- [ ] **Step 3: Open `index.html` in browser and verify structure**

You should see:
- Section heading "The command center for your farm." with a fade-in
- A dark browser-frame box (tilted slightly) with traffic light dots, a URL bar, and the preview tag
- App shell with the purple sidebar (showing Dashboard / Printer Fleet / Filament Inventory / Print Jobs buttons) and an empty dark content area on the right

The content area will be empty — that's expected until Task 3.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add demo section HTML structure"
```

---

### Task 3: Add JavaScript — DEMO_DATA, renderers, and tab switching

**Files:**
- Modify: `index.html` — append to the existing `<script>` block, immediately before the closing `</script>` tag (around line 1243)

- [ ] **Step 1: Locate insertion point**

Find the closing `</script>` tag (currently the last line before `</body>`). You will insert new code immediately before it, after the cycling headline code block that ends with:
```js
  }
</script>
```

- [ ] **Step 2: Insert the IIFE with DEMO_DATA, renderers, and tab switching**

Insert the following immediately before `</script>`:

```js

  // ---- INTERACTIVE DEMO ----
  (function() {
    // ================================================================
    // DEMO_DATA — edit this object to update the demo when app ships
    // ================================================================
    const DEMO_DATA = {
      stats: { spools: 34, printersOnline: 4, pendingOrders: 8 },
      activity: [
        { time: '2m ago',  text: 'Job completed: grid-clip-v3 on Bambu X1C #1', type: 'success' },
        { time: '8m ago',  text: 'Low stock detected: eSun PETG Amber (18%)',   type: 'warn'    },
        { time: '14m ago', text: 'Print job started on Prusa MK4 #2',           type: 'info'    },
        { time: '1h ago',  text: 'New order received — Etsy #4821',             type: 'info'    },
        { time: '2h ago',  text: 'Spool added: Polymaker PLA Silk Green 1kg',   type: 'success' }
      ],
      fleet: [
        { name: 'Bambu X1C #1',   status: 'printing', job: 'grid-clip-v3.3mf',   progress: 68, eta: '1h 24m' },
        { name: 'Prusa MK4 #2',   status: 'printing', job: 'bracket-mount.3mf',  progress: 31, eta: '3h 02m' },
        { name: 'Bambu A1 #3',    status: 'idle',     job: null,                  progress: 0,  eta: null     },
        { name: 'Bambu X1C #4',   status: 'printing', job: 'phone-stand-v2.3mf', progress: 89, eta: '12m'    },
        { name: 'Creality K1 #5', status: 'idle',     job: null,                  progress: 0,  eta: null     }
      ],
      inventory: [
        { color: '#a78bfa', name: 'Bambu PLA Matte',     variant: 'Purple', pct: 78 },
        { color: '#fb923c', name: 'eSun PETG',           variant: 'Amber',  pct: 18 },
        { color: '#4ade80', name: 'Polymaker PLA Silk',  variant: 'Green',  pct: 91 },
        { color: '#60a5fa', name: 'Bambu PLA Basic',     variant: 'Blue',   pct: 55 },
        { color: '#f9fafb', name: 'eSun PLA+',           variant: 'White',  pct: 43 },
        { color: '#f87171', name: 'Polymaker PolyTerra', variant: 'Red',    pct: 12 }
      ],
      jobs: [
        { file: 'grid-clip-v3.3mf',   printer: 'Bambu X1C #1',   status: 'in-progress', stars: null },
        { file: 'phone-stand-v2.3mf', printer: 'Bambu X1C #4',   status: 'in-progress', stars: null },
        { file: 'bracket-mount.3mf',  printer: 'Prusa MK4 #2',   status: 'completed',   stars: 5    },
        { file: 'wall-hook-v5.3mf',   printer: 'Bambu A1 #3',    status: 'completed',   stars: 4    },
        { file: 'nozzle-test-v1.3mf', printer: 'Creality K1 #5', status: 'failed',      stars: 1    }
      ]
    };

    const URL_PATHS = { dashboard: 'dashboard', fleet: 'printers', inventory: 'inventory', jobs: 'jobs' };
    const activityColors = { success: '#4ade80', warn: '#fb923c', info: '#a78bfa' };

    function renderDashboard() {
      const d = DEMO_DATA;
      return `
        <div class="demo-stat-grid">
          <div class="demo-stat-card">
            <div class="demo-stat-label">// SPOOLS</div>
            <div class="demo-stat-num" style="color:#a78bfa">${d.stats.spools}</div>
            <div class="demo-stat-sub">12 materials tracked</div>
          </div>
          <div class="demo-stat-card">
            <div class="demo-stat-label">// PRINTING</div>
            <div class="demo-stat-num" style="color:#fb923c">${d.stats.printersOnline}/5</div>
            <div class="demo-stat-sub">printers active</div>
          </div>
          <div class="demo-stat-card">
            <div class="demo-stat-label">// ORDERS</div>
            <div class="demo-stat-num" style="color:#4ade80">${d.stats.pendingOrders}</div>
            <div class="demo-stat-sub">pending fulfillment</div>
          </div>
        </div>
        <div class="demo-section-title">// RECENT ACTIVITY</div>
        <div>
          ${d.activity.map(a => `
            <div class="demo-activity-item">
              <span class="demo-activity-dot" style="background:${activityColors[a.type]}"></span>
              <span class="demo-activity-text">${a.text}</span>
              <span class="demo-activity-time">${a.time}</span>
            </div>
          `).join('')}
        </div>
      `;
    }

    function renderFleet() {
      return `
        <table class="demo-table">
          <thead>
            <tr>
              <th style="width:16px"></th>
              <th>PRINTER</th>
              <th>CURRENT JOB</th>
              <th>PROGRESS</th>
              <th>ETA</th>
            </tr>
          </thead>
          <tbody>
            ${DEMO_DATA.fleet.map(p => `
              <tr>
                <td><span class="demo-status-dot ${p.status}"></span></td>
                <td>${p.name}</td>
                <td><span class="demo-job-name">${p.job ? p.job : '<span style="color:#374151">idle</span>'}</span></td>
                <td>
                  ${p.status === 'printing'
                    ? `<div class="demo-bar-wrap"><div class="demo-bar" data-width="${p.progress}%"></div></div>`
                    : '<span style="color:#374151;font-family:var(--mono);font-size:.7rem">—</span>'}
                </td>
                <td><span class="demo-eta">${p.eta ? p.eta : '<span style="color:#374151">—</span>'}</span></td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      `;
    }

    function renderInventory() {
      return `
        <div class="demo-section-title" style="margin-bottom:.75rem">// FILAMENT INVENTORY — ${DEMO_DATA.inventory.length} SPOOLS</div>
        ${DEMO_DATA.inventory.map(s => `
          <div class="demo-spool-row">
            <span class="demo-spool-dot" style="background:${s.color}"></span>
            <span class="demo-spool-name">${s.name} <span class="demo-spool-variant">— ${s.variant}</span></span>
            <div class="demo-spool-bar-wrap">
              <div class="demo-spool-bar" style="background:${s.color}" data-width="${s.pct}%"></div>
            </div>
            <span class="demo-spool-pct">${s.pct}%</span>
            ${s.pct < 20 ? '<span class="demo-low-badge">Low</span>' : ''}
          </div>
        `).join('')}
      `;
    }

    function renderJobs() {
      const statusLabel = { 'completed': 'Completed', 'in-progress': 'In Progress', 'failed': 'Failed' };
      return `
        <table class="demo-table">
          <thead>
            <tr>
              <th>FILE</th>
              <th>PRINTER</th>
              <th>STATUS</th>
              <th>RATING</th>
            </tr>
          </thead>
          <tbody>
            ${DEMO_DATA.jobs.map(j => `
              <tr>
                <td><span class="demo-job-name">${j.file}</span></td>
                <td style="font-size:.78rem;color:var(--muted)">${j.printer}</td>
                <td><span class="demo-status-badge ${j.status}">${statusLabel[j.status]}</span></td>
                <td>
                  ${j.stars !== null
                    ? `<div class="demo-stars">${[1,2,3,4,5].map(i => `<span class="demo-star ${i <= j.stars ? 'filled' : 'empty'}">★</span>`).join('')}</div>`
                    : '<span style="color:#374151;font-family:var(--mono);font-size:.7rem">—</span>'}
                </td>
              </tr>
            `).join('')}
          </tbody>
        </table>
      `;
    }

    const renderers = { dashboard: renderDashboard, fleet: renderFleet, inventory: renderInventory, jobs: renderJobs };
    let activeTab = 'dashboard';

    function animateBars(container) {
      container.querySelectorAll('[data-width]').forEach(function(bar) {
        requestAnimationFrame(function() { bar.style.width = bar.dataset.width; });
      });
    }

    window.demoSwitch = function(tab) {
      if (tab === activeTab) return;
      activeTab = tab;

      document.querySelectorAll('.demo-nav-item').forEach(function(btn) {
        btn.classList.toggle('active', btn.dataset.tab === tab);
      });

      var urlPath = document.getElementById('demo-url-path');
      if (urlPath) urlPath.textContent = URL_PATHS[tab];

      var content = document.getElementById('demo-content');
      if (!content) return;
      content.classList.add('fade-out-state');
      setTimeout(function() {
        content.innerHTML = renderers[tab]();
        content.classList.remove('fade-out-state');
        animateBars(content);
      }, 150);
    };

    // Initial render
    var initContent = document.getElementById('demo-content');
    if (initContent) {
      initContent.innerHTML = renderDashboard();
      animateBars(initContent);
    }

    // Auto-cycle once on first scroll into view
    var demoSection = document.getElementById('demo');
    if (demoSection) {
      var demoObs = new IntersectionObserver(function(entries) {
        entries.forEach(function(entry) {
          if (entry.isIntersecting && !entry.target.dataset.cycled) {
            entry.target.dataset.cycled = '1';
            var tabs = ['dashboard', 'fleet', 'inventory', 'jobs'];
            var i = 0;
            var cycle = setInterval(function() {
              i++;
              if (i >= tabs.length) { clearInterval(cycle); demoSwitch('dashboard'); return; }
              demoSwitch(tabs[i]);
            }, 1500);
          }
        });
      }, { threshold: 0.3 });
      demoObs.observe(demoSection);
    }
  })();
```

- [ ] **Step 3: Open `index.html` in browser and verify all 4 tabs**

Expected behavior:
- Dashboard tab (default): 3 stat cards (34 spools / 4/5 printers / 8 orders) + 5 activity feed items
- Click "Printer Fleet": table with 5 printers — 3 printing (green pulsing dot + progress bar), 2 idle (grey dot)
- Click "Filament Inventory": 6 spool rows — color dots, animated progress bars, two spools with amber "Low" badge (eSun PETG 18% and PolyTerra Red 12%)
- Click "Print Jobs": 5 job rows — 2 in-progress (amber badge, no stars), 2 completed (green badge, stars), 1 failed (red badge, 1 star)
- URL bar text updates on each tab click
- Tab transitions fade out/in smoothly
- Progress bars animate from 0 to value on each tab enter

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add demo section JS — DEMO_DATA, renderers, tab switching, auto-cycle"
```

---

### Task 4: Add demo to nav and scroll-spy

**Files:**
- Modify: `index.html` — 3 small edits: desktop nav list, mobile nav drawer, scroll-spy sections array

- [ ] **Step 1: Add Demo to the desktop nav links**

Find the nav links `<ul>` (around line 365). It currently starts:
```html
    <li><a href="#">Home</a></li>
    <li><a href="#features">Features</a></li>
```
Add the Demo link between Home and Features:
```html
    <li><a href="#">Home</a></li>
    <li><a href="#demo">Demo</a></li>
    <li><a href="#features">Features</a></li>
```

- [ ] **Step 2: Add Demo to the mobile nav drawer**

Find the mobile nav drawer (around line 387). It currently starts:
```html
  <a href="#" onclick="closeMenu()">Home</a>
  <a href="#features" onclick="closeMenu()">Features</a>
```
Add the Demo link between Home and Features:
```html
  <a href="#" onclick="closeMenu()">Home</a>
  <a href="#demo" onclick="closeMenu()">Demo</a>
  <a href="#features" onclick="closeMenu()">Features</a>
```

- [ ] **Step 3: Add `demo` to the scroll-spy sections array**

Find the `sections` array in the `<script>` block (around line 1186):
```js
  const sections = [
    { id: 'features', label: 'Features' },
```
Add the demo entry at the top:
```js
  const sections = [
    { id: 'demo', label: 'Demo' },
    { id: 'features', label: 'Features' },
```

- [ ] **Step 4: Open `index.html` in browser and verify nav**

- "Demo" link appears in the desktop nav between Home and Features
- Clicking "Demo" scrolls to the demo section
- As you scroll past the demo section, "Demo" becomes the active nav item (highlighted)
- Mobile hamburger menu includes "Demo" link and it works

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add demo to nav and scroll-spy"
```

---

## Done

All 4 tasks complete. The interactive demo section is live between the stats strip and the first photo break. To update the demo content in the future, edit only the `DEMO_DATA` object inside the `<script>` block — all rendering is data-driven from that single object.
