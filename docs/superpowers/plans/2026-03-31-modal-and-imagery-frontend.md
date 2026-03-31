# Modal & Imagery — Frontend Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Activate all non-functional CTA buttons with a plan-aware contact/waitlist modal, add two photo breaks, and replace emoji with inline SVG icons on feature category headers.

**Architecture:** All changes are in the single `index.html` file — CSS added to the `<style>` block, HTML added before `</body>`, JS added to the `<script>` block. The modal POSTs to a configurable API URL constant; until the backend exists it logs to console and shows a success state. No build step, no dependencies.

**Tech Stack:** Vanilla HTML/CSS/JS. No frameworks, no external libraries. Inline SVGs (no icon library). Unsplash for photos (same pattern as existing page).

**Backend plan:** See `docs/superpowers/plans/2026-03-31-modal-and-imagery-backend.md` (not yet written). Until then, the `API_URL` constant is set to `null` and the form shows a success state immediately on submit.

---

## File Structure

| File | Change |
|---|---|
| `index.html` | All changes — CSS, HTML, JS |

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
  border-radius: 12px; width: 100%; max-width: 480px;
  max-height: 90vh; overflow-y: auto;
  padding: 2rem; position: relative;
  box-shadow: 0 24px 64px rgba(0,0,0,.5);
}
.modal-close {
  position: absolute; top: 1rem; right: 1rem;
  background: none; border: none; cursor: pointer;
  color: var(--muted); font-size: 1.25rem; line-height: 1;
  padding: .25rem .5rem; border-radius: 4px; transition: color .2s;
}
.modal-close:hover { color: var(--text); }
.modal-title {
  font-family: var(--display); font-size: 1.2rem; font-weight: 600;
  letter-spacing: -.01em; margin-bottom: .35rem;
}
.modal-subtitle {
  font-size: .85rem; color: var(--muted); margin-bottom: 1.5rem;
}
.modal-form { display: flex; flex-direction: column; gap: 1rem; }
.form-row { display: flex; gap: .75rem; }
.form-row .form-group { flex: 1; }
.form-group { display: flex; flex-direction: column; gap: .35rem; }
.form-group label {
  font-size: .78rem; font-weight: 500; color: var(--text);
  font-family: var(--mono); letter-spacing: .03em;
}
.form-group label span { color: var(--muted); font-weight: 400; }
.form-group input,
.form-group select,
.form-group textarea {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: 6px; color: var(--text); font-family: var(--sans);
  font-size: .9rem; padding: .6rem .85rem; outline: none;
  transition: border-color .2s;
}
.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus { border-color: var(--blue); }
.form-group select { appearance: none; cursor: pointer; }
.form-group textarea { resize: vertical; min-height: 90px; }
.form-group input::placeholder,
.form-group textarea::placeholder { color: var(--muted); }
.modal-submit {
  background: var(--blue); color: #fff; border: none; cursor: pointer;
  padding: .8rem 2rem; border-radius: 8px; font-weight: 500;
  font-size: .95rem; font-family: var(--sans);
  transition: background .2s, box-shadow .2s; margin-top: .5rem;
  box-shadow: 0 4px 24px rgba(59,106,255,.4);
}
.modal-submit:hover:not(:disabled) { background: #4d7aff; box-shadow: 0 8px 32px rgba(59,106,255,.5); }
.modal-submit:disabled { opacity: .6; cursor: not-allowed; }
.modal-error {
  font-size: .82rem; color: #ff6060; margin-top: -.25rem;
  display: none;
}
.modal-error.visible { display: block; }
.modal-success { display: none; text-align: center; padding: 1rem 0; }
.modal-success.visible { display: block; }
.modal-success-icon { font-size: 2.5rem; margin-bottom: .75rem; }
.modal-success h3 {
  font-family: var(--display); font-size: 1.1rem; font-weight: 600;
  margin-bottom: .5rem;
}
.modal-success p { font-size: .9rem; color: var(--muted); line-height: 1.6; }
@media (max-width: 480px) {
  .form-row { flex-direction: column; }
}
```

- [ ] **Step 2: Add modal HTML**

Find the `<!-- FOOTER -->` comment. Insert the following block immediately before it:

```html
<!-- MODAL -->
<div class="modal-backdrop" id="modalBackdrop" onclick="handleBackdropClick(event)">
  <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
    <button class="modal-close" onclick="closeModal()" aria-label="Close">✕</button>

    <!-- Success state -->
    <div class="modal-success" id="modalSuccess">
      <div class="modal-success-icon">🎯</div>
      <h3>You're on the list.</h3>
      <p>We'll be in touch when it's time. In the meantime, your filament is still waiting to be tracked.</p>
      <button class="modal-submit" onclick="closeModal()" style="margin-top:1.25rem;">Close</button>
    </div>

    <!-- Form state -->
    <div id="modalFormWrap">
      <div class="modal-title" id="modalTitle">Join Early Access</div>
      <div class="modal-subtitle">No credit card. No spam. Just updates when it matters.</div>

      <form class="modal-form" id="modalForm" onsubmit="handleModalSubmit(event)">
        <input type="hidden" id="modalPlanField" name="plan" value="">

        <div class="form-row">
          <div class="form-group">
            <label for="modalFirstName">First Name</label>
            <input type="text" id="modalFirstName" name="firstName" placeholder="Jane" required autocomplete="given-name">
          </div>
          <div class="form-group">
            <label for="modalLastName">Last Name</label>
            <input type="text" id="modalLastName" name="lastName" placeholder="Smith" required autocomplete="family-name">
          </div>
        </div>

        <div class="form-group">
          <label for="modalEmail">Email</label>
          <input type="email" id="modalEmail" name="email" placeholder="jane@example.com" required autocomplete="email">
        </div>

        <div class="form-group">
          <label for="modalBusiness">Business Name <span>(optional)</span></label>
          <input type="text" id="modalBusiness" name="businessName" placeholder="Acme Print Co." autocomplete="organization">
        </div>

        <div class="form-group">
          <label for="modalReason">Reason for reaching out <span>(optional)</span></label>
          <select id="modalReason" name="reason">
            <option value="">Select a reason…</option>
            <optgroup label="Sales">
              <option value="interested-paid-plan">Interested in a paid plan</option>
              <option value="want-demo">Want a demo</option>
              <option value="pricing-question">Pricing question</option>
            </optgroup>
            <optgroup label="Support">
              <option value="help-setup">Need help with setup</option>
              <option value="found-bug">Found a bug</option>
              <option value="feature-request">Feature request</option>
            </optgroup>
            <optgroup label="General">
              <option value="just-checking">Just checking it out</option>
              <option value="other">Other</option>
            </optgroup>
          </select>
        </div>

        <div class="form-group">
          <label for="modalMessage">Message <span>(optional)</span></label>
          <textarea id="modalMessage" name="message" placeholder="Tell us about your print farm, or just say hi."></textarea>
        </div>

        <div class="modal-error" id="modalError"></div>
        <button type="submit" class="modal-submit" id="modalSubmitBtn">Send it →</button>
      </form>
    </div>
  </div>
</div>

```

- [ ] **Step 3: Verify in browser**

Open `index.html`. In the browser console, run:
```js
openModal('The Tinkerer')
```
Confirm:
- Modal appears centered with backdrop blur
- Title reads "Join Early Access — The Tinkerer"
- All form fields are present and styled correctly
- First Name / Last Name are side by side on desktop
- ✕ button is visible in top-right corner

Then run `closeModal()` in console. Confirm modal closes.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add modal HTML and CSS"
```

---

### Task 5: Add modal JS — open/close and plan-aware title

**Files:**
- Modify: `index.html` — add to `<script>` block

- [ ] **Step 1: Add modal open/close JS**

Find the closing `</script>` tag. Insert the following immediately before it:

```js
// Modal
const PLAN_TITLES = {
  'The Tinkerer': 'Join Early Access — The Tinkerer',
  'The Operator': 'Get Notified at Launch — The Operator',
  'The Studio':   'Get Notified at Launch — The Studio',
};

function openModal(plan) {
  const backdrop = document.getElementById('modalBackdrop');
  const title = document.getElementById('modalTitle');
  const planField = document.getElementById('modalPlanField');
  const formWrap = document.getElementById('modalFormWrap');
  const success = document.getElementById('modalSuccess');
  const form = document.getElementById('modalForm');
  const errorEl = document.getElementById('modalError');
  const submitBtn = document.getElementById('modalSubmitBtn');

  // Reset to form state
  success.classList.remove('visible');
  formWrap.style.display = '';
  form.reset();
  errorEl.classList.remove('visible');
  errorEl.textContent = '';
  submitBtn.disabled = false;
  submitBtn.textContent = 'Send it →';

  // Set plan-aware title and hidden field
  title.textContent = PLAN_TITLES[plan] || 'Join Early Access';
  planField.value = plan || '';

  backdrop.classList.add('open');
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

- [ ] **Step 2: Verify open/close in browser**

Open `index.html`. In the browser console:

```js
openModal('The Operator')
```

Confirm:
- Modal title reads "Get Notified at Launch — The Operator"
- Hidden plan input value: inspect `document.getElementById('modalPlanField').value` → `"The Operator"`

Click the backdrop outside the modal card. Confirm modal closes.
Press Escape key while modal is open. Confirm modal closes.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add modal open/close JS with plan-aware titles"
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
<a href="#" class="pbtn out" onclick="event.preventDefault(); openModal('The Tinkerer')">Join Early Access</a>
```

- [ ] **Step 2: Wire Operator pricing card button**

Find:
```html
<a href="#" class="pbtn sol">Get Notified at Launch</a>
```

Replace with:
```html
<a href="#" class="pbtn sol" onclick="event.preventDefault(); openModal('The Operator')">Get Notified at Launch</a>
```

- [ ] **Step 3: Wire Studio pricing card button**

Find:
```html
<a href="#" class="pbtn out">Get Notified at Launch</a>
```
(Inside the Studio pricing card — the second `pbtn out` in the pricing grid)

Replace with:
```html
<a href="#" class="pbtn out" onclick="event.preventDefault(); openModal('The Studio')">Get Notified at Launch</a>
```

- [ ] **Step 4: Wire comparison table CTA row buttons**

Find (Tinkerer column in cta-row):
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;">Join Early Access</a>
```
Replace with:
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;" onclick="event.preventDefault(); openModal('The Tinkerer')">Join Early Access</a>
```

Find (Operator column in cta-row):
```html
<a href="#" class="pbtn sol" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;">Get Notified</a>
```
Replace with:
```html
<a href="#" class="pbtn sol" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;" onclick="event.preventDefault(); openModal('The Operator')">Get Notified</a>
```

Find (Studio column in cta-row):
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;">Get Notified</a>
```
Replace with:
```html
<a href="#" class="pbtn out" style="display:block;text-align:center;font-size:.8rem;padding:.6rem;" onclick="event.preventDefault(); openModal('The Studio')">Get Notified</a>
```

- [ ] **Step 5: Wire CTA banner button**

Find:
```html
<a href="#" class="btn-primary">Join Early Access — It's Free</a>
```

Replace with:
```html
<a href="#" class="btn-primary" onclick="event.preventDefault(); openModal('')">Join Early Access — It's Free</a>
```

- [ ] **Step 6: Verify all buttons in browser**

Open `index.html`. Click each of the following and confirm the modal opens with the correct title:

| Button | Expected modal title |
|---|---|
| Tinkerer card "Join Early Access" | Join Early Access — The Tinkerer |
| Operator card "Get Notified at Launch" | Get Notified at Launch — The Operator |
| Studio card "Get Notified at Launch" | Get Notified at Launch — The Studio |
| Comparison table Tinkerer row | Join Early Access — The Tinkerer |
| Comparison table Operator row | Get Notified at Launch — The Operator |
| Comparison table Studio row | Get Notified at Launch — The Studio |
| CTA banner | Join Early Access |

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat: wire all CTA buttons to plan-aware modal"
```

---

### Task 7: Add form submission JS with states

**Files:**
- Modify: `index.html` — add to `<script>` block (after modal open/close JS)

- [ ] **Step 1: Add API URL constant and submit handler**

Find the closing `</script>` tag. Insert the following immediately before it:

```js
// Form submission
// Set to your Vercel API URL when backend is deployed e.g.:
// const API_URL = 'https://tacticalyogurt.vercel.app/api/contact';
const API_URL = null; // stub: shows success immediately until backend exists

async function handleModalSubmit(e) {
  e.preventDefault();

  const submitBtn = document.getElementById('modalSubmitBtn');
  const errorEl = document.getElementById('modalError');
  const formWrap = document.getElementById('modalFormWrap');
  const success = document.getElementById('modalSuccess');
  const form = document.getElementById('modalForm');

  // Submitting state
  submitBtn.disabled = true;
  submitBtn.textContent = 'Sending…';
  errorEl.classList.remove('visible');
  errorEl.textContent = '';

  const data = {
    firstName:    form.firstName.value.trim(),
    lastName:     form.lastName.value.trim(),
    email:        form.email.value.trim(),
    businessName: form.businessName.value.trim(),
    reason:       form.reason.value,
    message:      form.message.value.trim(),
    plan:         form.plan.value,
  };

  try {
    if (API_URL) {
      const res = await fetch(API_URL, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data),
      });
      if (!res.ok) {
        const body = await res.json().catch(() => ({}));
        throw new Error(body.error || 'Something went wrong. Please try again.');
      }
    } else {
      // Stub: log to console until backend is live
      console.log('[Modal stub] Form submission:', data);
      await new Promise(r => setTimeout(r, 600)); // simulate network
    }
    // Success state
    formWrap.style.display = 'none';
    success.classList.add('visible');
  } catch (err) {
    errorEl.textContent = err.message;
    errorEl.classList.add('visible');
    submitBtn.disabled = false;
    submitBtn.textContent = 'Send it →';
  }
}
```

- [ ] **Step 2: Verify stub submission in browser**

Open `index.html`. Click any CTA button to open the modal. Fill in:
- First Name: `Test`
- Last Name: `User`
- Email: `test@example.com`

Click "Send it →". Confirm:
- Button text changes to "Sending…" and is disabled
- After ~600ms the form is replaced by the success message: "You're on the list."
- Browser console shows: `[Modal stub] Form submission: {firstName: "Test", ...}`

Click "Close". Confirm modal closes.

Open the modal again. Confirm the form is reset to blank (not still showing success state).

- [ ] **Step 3: Verify error state**

In the browser console, temporarily override the stub to force an error:
```js
// Paste into console to test error state:
document.getElementById('modalForm').onsubmit = async function(e) {
  e.preventDefault();
  document.getElementById('modalSubmitBtn').disabled = true;
  document.getElementById('modalSubmitBtn').textContent = 'Sending…';
  await new Promise(r => setTimeout(r, 400));
  const err = document.getElementById('modalError');
  err.textContent = 'Something went wrong. Please try again.';
  err.classList.add('visible');
  document.getElementById('modalSubmitBtn').disabled = false;
  document.getElementById('modalSubmitBtn').textContent = 'Send it →';
};
openModal('The Tinkerer');
```
Submit the form. Confirm the error message appears in red below the submit button.

Reload the page to restore normal behaviour.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add form submission JS with submitting/success/error states"
```

---

### Task 8: Final review and push

- [ ] **Step 1: Full page walkthrough in browser**

Open `index.html` locally. Walk through the entire page top to bottom:

1. All 6 feature category icons show SVGs (not emoji)
2. Photo break appears between Features and Integrations with overlay text
3. Photo break appears between How it Works and Pricing with overlay text
4. All 7 CTA buttons open the modal with the correct title
5. Modal form fields all present and styled correctly
6. Form submits successfully (stub), shows success state
7. Modal closes cleanly, form resets on re-open
8. On mobile (resize browser to < 480px): First/Last Name stack vertically

- [ ] **Step 2: Push to GitHub**

```bash
git push origin main
```

- [ ] **Step 3: Verify on GitHub Pages**

Wait ~60 seconds after push. Open `https://tacticalyogurtapp.github.io/tacticalyogurt-marketing` and repeat the walkthrough from Step 1.
