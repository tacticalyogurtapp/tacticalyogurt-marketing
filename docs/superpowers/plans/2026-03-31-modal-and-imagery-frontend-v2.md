# Modal & Imagery — Frontend Implementation Plan (v2: Google Forms)

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Activate all non-functional CTA buttons with a Google Forms modal, add two photo breaks, and replace emoji with inline SVG icons on feature category headers.

**Architecture:** All changes are in the single `index.html` file — CSS added to the `<style>` block, HTML added before `</body>`, JS added to the `<script>` block. The modal embeds a Google Form via iframe; no custom form fields, no backend, no submission JS.

**Tech Stack:** Vanilla HTML/CSS/JS. No frameworks, no external libraries. Inline SVGs (no icon library). Unsplash for photos (same pattern as existing page). Google Forms for contact/waitlist capture.

**Supersedes:** `docs/superpowers/plans/2026-03-31-modal-and-imagery-frontend.md`

**Design spec:** `docs/superpowers/specs/2026-03-31-google-forms-modal-pivot.md`

---

## File Structure

| File | Change |
|---|---|
| `index.html` | All changes — CSS, HTML, JS |
| `preview-modal.html` | Delete before final push (preview artifact) |

---

### Task 1: Replace emoji with SVG icons in feature category headers

**Files:**
- Modify: `index.html` (the 6 `.cat-icon` divs, lines ~292–375)

These are the 6 `.cat-icon` divs. Each currently contains an emoji. Replace the inner content with an inline SVG. The colored `background` on each div stays as-is.

- [ ] **Step 1: Replace Inventory Management icon (🧵 → box SVG)**

Find:
```html
<div class="cat-icon" style="background:rgba(59,106,255,.15)">🧵</div>
```
Replace with:
```html
<div class="cat-icon" style="background:rgba(59,106,255,.15)">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#3b6aff" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"><path d="M21 8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16Z"/><path d="m3.29 7 8.71 5 8.71-5"/><line x1="12" y1="22" x2="12" y2="12"/></svg>
</div>
```

- [ ] **Step 2: Replace Printer Fleet icon (🖨️ → printer SVG)**

Find:
```html
<div class="cat-icon" style="background:rgba(255,140,66,.15)">🖨️</div>
```
Replace with:
```html
<div class="cat-icon" style="background:rgba(255,140,66,.15)">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#ff8c42" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"><polyline points="6 9 6 2 18 2 18 9"/><path d="M6 18H4a2 2 0 0 1-2-2v-5a2 2 0 0 1 2-2h16a2 2 0 0 1 2 2v5a2 2 0 0 1-2 2h-2"/><rect x="6" y="14" width="12" height="8"/></svg>
</div>
```

- [ ] **Step 3: Replace Print Job Workflow icon (⚙️ → gear SVG)**

Find:
```html
<div class="cat-icon" style="background:rgba(47,216,122,.15)">⚙️</div>
```
Replace with:
```html
<div class="cat-icon" style="background:rgba(47,216,122,.15)">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#2fd87a" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1Z"/></svg>
</div>
```

- [ ] **Step 4: Replace Print File Management icon (📁 → file SVG)**

Find:
```html
<div class="cat-icon" style="background:rgba(59,106,255,.15)">📁</div>
```
Replace with:
```html
<div class="cat-icon" style="background:rgba(59,106,255,.15)">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#3b6aff" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/><line x1="16" y1="13" x2="8" y2="13"/><line x1="16" y1="17" x2="8" y2="17"/><polyline points="10 9 9 9 8 9"/></svg>
</div>
```

- [ ] **Step 5: Replace Orders & Customers icon (📦 → shopping bag SVG)**

Find:
```html
<div class="cat-icon" style="background:rgba(255,140,66,.15)">📦</div>
```
Replace with:
```html
<div class="cat-icon" style="background:rgba(255,140,66,.15)">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#ff8c42" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"><path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/><line x1="3" y1="6" x2="21" y2="6"/><path d="M16 10a4 4 0 0 1-8 0"/></svg>
</div>
```

- [ ] **Step 6: Replace Tasks/Markets icon (📋 → clipboard SVG)**

Find:
```html
<div class="cat-icon" style="background:rgba(47,216,122,.15)">📋</div>
```
Replace with:
```html
<div class="cat-icon" style="background:rgba(47,216,122,.15)">
  <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#2fd87a" stroke-width="1.75" stroke-linecap="round" stroke-linejoin="round"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="9" y1="12" x2="15" y2="12"/><line x1="9" y1="16" x2="13" y2="16"/></svg>
</div>
```

- [ ] **Step 7: Verify in browser**

Open `index.html` in a browser. Scroll to the Features section. Confirm:
- All 6 category icons show SVGs (not emoji)
- Icon colors match section accent colors (blue, orange, green, blue, orange, green)
- Icons are centered and correctly sized within their colored circle backgrounds

- [ ] **Step 8: Commit**

```bash
git add index.html
git commit -m "feat: replace emoji with SVG icons on feature category headers"
```

---

### Task 2: Add photo break between Features and Integrations

**Files:**
- Modify: `index.html` (after the closing `</div>` of the features section, before the integrations `<!-- INTEGRATIONS -->` comment, around line ~396)

- [ ] **Step 1: Add the photo break HTML**

Find this comment:
```html
<!-- INTEGRATIONS -->
```

Insert the following block immediately before it:

```html
<!-- PHOTO BREAK: FILAMENT WALL -->
<div class="photo-break">
  <img src="https://images.unsplash.com/photo-1609710228159-0fa9bd7c0827?w=1400&q=80" alt="Filament spool rack" onerror="this.src='https://images.unsplash.com/photo-1558618666-fcd25c85cd64?w=1400&q=80'" />
  <div class="photo-break-overlay">
    <div class="photo-break-text fade-in">
      <h2>Every spool. Every color. Every gram.</h2>
      <p>TacticalYogurt tracks your entire filament inventory in real time — so you never start a job you can't finish.</p>
    </div>
  </div>
</div>

```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Scroll to between the Features section and the Integrations section. Confirm:
- Full-width photo break appears with a 3D printing / filament image
- Overlay text is readable over the image
- If the primary image fails to load, the fallback Unsplash URL loads instead
- Fade-in animation triggers on scroll

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add filament wall photo break between features and integrations"
```

---

### Task 3: Add photo break between How it Works and Pricing

**Files:**
- Modify: `index.html` (after the How it Works section closing `</div>`, before `<!-- PRICING -->`, around line ~458)

- [ ] **Step 1: Add the photo break HTML**

Find this comment:
```html
<!-- PRICING -->
```

Insert the following block immediately before it:

```html
<!-- PHOTO BREAK: WORKBENCH -->
<div class="photo-break">
  <img src="https://images.unsplash.com/photo-1581092918056-0c4c3acd3789?w=1400&q=80" alt="3D printer workbench" onerror="this.src='https://images.unsplash.com/photo-1612198188060-c7c2a3b66eae?w=1400&q=80'" />
  <div class="photo-break-overlay">
    <div class="photo-break-text fade-in">
      <h2>Set it up once. Let it run.</h2>
      <p>Connect your printers, your markets, and your inventory — then get back to making things.</p>
    </div>
  </div>
</div>

```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Scroll to between the How it Works section and the Pricing section. Confirm:
- Full-width photo break appears with a workbench / printers image
- Overlay text is readable
- Fallback image loads if primary fails
- Fade-in animation triggers on scroll

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add workbench photo break between how-it-works and pricing"
```

---

### Task 4: Add modal HTML and CSS

**Files:**
- Modify: `index.html` — add CSS to `<style>` block, add modal HTML before `</body>`

The modal is a simple overlay with a close button and a Google Form iframe. No custom form fields.

- [ ] **Step 1: Add modal CSS**

Find the closing `</style>` tag. Insert the following block immediately before it:

```css
/* MODAL */
.modal-backdrop {
  display: none; position: fixed; inset: 0; z-index: 200;
  background: rgba(0,0,0,.6); backdrop-filter: blur(4px);
  align-items: center; justify-content: center; padding: 1rem;
}
.modal-backdrop.open { display: flex; }
.modal {
  background: var(--card); border: 1px solid var(--border);
  border-radius: 12px; width: 100%; max-width: 660px;
  max-height: 90vh; overflow-y: auto;
  padding: 2.5rem 2rem 2rem; position: relative;
  box-shadow: 0 24px 64px rgba(0,0,0,.5);
}
.modal-close {
  position: absolute; top: 1rem; right: 1rem;
  background: none; border: none; cursor: pointer;
  color: var(--muted); font-size: 1.25rem; line-height: 1;
  padding: .25rem .5rem; border-radius: 4px; transition: color .2s;
}
.modal-close:hover { color: var(--text); }
.modal iframe { display: block; width: 100%; border: none; border-radius: 4px; }
```

- [ ] **Step 2: Add modal HTML**

Find the `<!-- FOOTER -->` comment. Insert the following block immediately before it:

```html
<!-- MODAL -->
<div class="modal-backdrop" id="modalBackdrop" onclick="handleBackdropClick(event)">
  <div class="modal" role="dialog" aria-modal="true" aria-label="Contact form">
    <button class="modal-close" onclick="closeModal()" aria-label="Close">✕</button>
    <iframe
      src="https://docs.google.com/forms/d/e/1FAIpQLSeQht3YLPA9Na92ew4G0Y8GVSEchCRmosn1RJxhjBrqc6bWug/viewform?embedded=true"
      height="955"
      frameborder="0"
      marginheight="0"
      marginwidth="0">Loading…</iframe>
  </div>
</div>

```

- [ ] **Step 3: Verify in browser**

Open `index.html`. In the browser console, run:
```js
document.getElementById('modalBackdrop').classList.add('open')
```
Confirm:
- Modal appears centered with backdrop blur
- Google Form loads inside the iframe
- Close button (✕) is visible in the top-right corner of the modal card
- Modal card is wider than the rest of the page content (max-width 660px)

Then run in console:
```js
document.getElementById('modalBackdrop').classList.remove('open')
```
Confirm modal closes.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add Google Forms modal HTML and CSS"
```

---

### Task 5: Add modal open/close JS

**Files:**
- Modify: `index.html` — add to `<script>` block

- [ ] **Step 1: Add modal JS**

Find the closing `</script>` tag. Insert the following immediately before it:

```js
// Modal
function openModal() {
  document.getElementById('modalBackdrop').classList.add('open');
  document.body.style.overflow = 'hidden';
}

function closeModal() {
  document.getElementById('modalBackdrop').classList.remove('open');
  document.body.style.overflow = '';
}

function handleBackdropClick(e) {
  if (e.target === document.getElementById('modalBackdrop')) closeModal();
}

// Close on Escape key
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') closeModal();
});
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. In the browser console, run:
```js
openModal()
```
Confirm modal opens. Then:
- Click the backdrop (outside the modal card) — confirm modal closes
- Run `openModal()` again — press Escape — confirm modal closes
- Run `openModal()` again — click the ✕ button — confirm modal closes

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add modal open/close JS"
```

---

### Task 6: Wire all CTA buttons to the modal

**Files:**
- Modify: `index.html` — update `href="#"` buttons to call `openModal()`

- [ ] **Step 1: Wire Tinkerer pricing card button**

Find:
```html
<a href="#" class="pbtn out">Join Early Access</a>
```
(Inside the Tinkerer pricing card — the first `pbtn out` in the pricing grid)

Replace with:
```html
<a href="#" class="pbtn out" onclick="event.preventDefault(); openModal()">Join Early Access</a>
```

- [ ] **Step 2: Wire Operator pricing card button**

Find:
```html
<a href="#" class="pbtn sol">Get Notified at Launch</a>
```

Replace with:
```html
<a href="#" class="pbtn sol" onclick="event.preventDefault(); openModal()">Get Notified at Launch</a>
```

- [ ] **Step 3: Wire Studio pricing card button**

Find:
```html
<a href="#" class="pbtn out">Get Notified at Launch</a>
```
(Inside the Studio pricing card — the second `pbtn out` in the pricing grid)

Replace with:
```html
<a href="#" class="pbtn out" onclick="event.preventDefault(); openModal()">Get Notified at Launch</a>
```

- [ ] **Step 4: Wire comparison table Tinkerer CTA button**

Find:
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;">Join Early Access</a>
```

Replace with:
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;" onclick="event.preventDefault(); openModal()">Join Early Access</a>
```

- [ ] **Step 5: Wire comparison table Operator CTA button**

Find:
```html
<a href="#" class="pbtn sol" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;">Get Notified</a>
```

Replace with:
```html
<a href="#" class="pbtn sol" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;" onclick="event.preventDefault(); openModal()">Get Notified</a>
```

- [ ] **Step 6: Wire comparison table Studio CTA button**

Find:
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;">Get Notified</a>
```

Replace with:
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;" onclick="event.preventDefault(); openModal()">Get Notified</a>
```

- [ ] **Step 7: Wire CTA banner button**

Find:
```html
<a href="#" class="btn-primary">Join Early Access — It's Free</a>
```

Replace with:
```html
<a href="#" class="btn-primary" onclick="event.preventDefault(); openModal()">Join Early Access — It's Free</a>
```

- [ ] **Step 8: Verify all buttons in browser**

Open `index.html`. Click each of the following and confirm the modal opens:

| Button | Location |
|---|---|
| Join Early Access | Tinkerer pricing card |
| Get Notified at Launch | Operator pricing card |
| Get Notified at Launch | Studio pricing card |
| Join Early Access | Comparison table — Tinkerer column |
| Get Notified | Comparison table — Operator column |
| Get Notified | Comparison table — Studio column |
| Join Early Access — It's Free | CTA banner |

- [ ] **Step 9: Commit**

```bash
git add index.html
git commit -m "feat: wire all CTA buttons to Google Forms modal"
```

---

### Task 7: Final review, cleanup, and push

- [ ] **Step 1: Delete preview file**

```bash
git rm preview-modal.html
```

- [ ] **Step 2: Full page walkthrough in browser**

Open `index.html` locally. Walk through the entire page top to bottom:

1. All 6 feature category icons show SVGs (not emoji)
2. Photo break appears between Features and Integrations with overlay text
3. Photo break appears between How it Works and Pricing with overlay text
4. All 7 CTA buttons open the modal
5. Google Form loads inside the modal iframe
6. Modal closes via ✕ button, backdrop click, and Escape key
7. Body scroll is locked while modal is open, restored on close

- [ ] **Step 3: Commit cleanup and push**

```bash
git commit -m "chore: remove modal preview file"
git push origin main
```

- [ ] **Step 4: Verify on GitHub Pages**

Wait ~60 seconds after push. Open the live GitHub Pages URL and repeat the walkthrough from Step 2.
