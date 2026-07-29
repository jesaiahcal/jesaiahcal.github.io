# Resume Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and publish a single-page dark-themed resume website for Jesaiah Calderon at `https://jesaiahcal.github.io`.

**Architecture:** Plain static HTML/CSS/JS with no framework, build step, or external dependencies — three files (`index.html`, `style.css`, `script.js`) served directly by GitHub Pages from the `main` branch of the `jesaiahcal.github.io` repo.

**Tech Stack:** HTML5, CSS3 (custom properties, Grid/Flexbox), vanilla JavaScript (Canvas 2D API). No package manager, no bundler.

## Global Constraints

- No framework, build step, or npm/package dependencies — plain HTML/CSS/JS only (per spec Architecture).
- Single scrollable page, not multiple pages — each `<section>` is self-contained enough to split into its own page later, but do not create additional HTML files now (per spec Scope Decisions).
- Contact section shows email, phone, and LinkedIn fully in plain text/links — phone number is intentionally public, this was explicitly confirmed (per spec Scope Decisions).
- Dark theme: near-black background, cyan/blue accent color, monospace headings, sans-serif body text (per spec Visual Design).
- Background particle-network animation must stay subtle (low opacity, slow movement), must never block clicks/scroll (`pointer-events: none`), and must be disabled when the OS `prefers-reduced-motion` setting is on (per spec Visual Design).
- Repo name must be exactly `jesaiahcal.github.io` (per spec Architecture) — this repo already exists locally at `/Users/jesaiahcalderon/jesaiahcal.github.io` with one commit (the design spec).
- No automated test framework — the spec explicitly scopes this out for a static single-page site. Verification is manual browser checks, spelled out exactly in each task below (per spec Verification and Out of Scope).

---

### Task 1: Page structure and content (`index.html`)

**Files:**
- Create: `/Users/jesaiahcalderon/jesaiahcal.github.io/index.html`
- Create: `/Users/jesaiahcalderon/jesaiahcal.github.io/.gitignore`

**Interfaces:**
- Consumes: nothing (first task).
- Produces: the DOM structure later tasks depend on —
  - `<canvas id="bg-canvas">` (Task 3 attaches to this id)
  - `<link rel="stylesheet" href="style.css">` (Task 2 creates this file)
  - `<script src="script.js">` (Task 3 creates this file)
  - Section ids: `#summary`, `#skills`, `#experience`, `#certifications`, `#contact` (Task 2 styles these; nav links target them)
  - Class names Task 2 will style: `site-header`, `header-inner`, `identity`, `tagline`, `location`, `site-nav`, `section`, `skills-grid`, `skill-group`, `job`, `job-meta`, `cert-list`, `contact-list`, `site-footer`

- [ ] **Step 1: Create `.gitignore`**

```
.DS_Store
```

- [ ] **Step 2: Create `index.html` with full page content**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jesaiah Calderon — IT Support &amp; Cybersecurity</title>
<meta name="description" content="Resume site for Jesaiah Calderon, IT Support Technician and aspiring cybersecurity professional.">
<link rel="stylesheet" href="style.css">
</head>
<body>
<canvas id="bg-canvas" aria-hidden="true"></canvas>

<header class="site-header">
  <div class="header-inner">
    <div class="identity">
      <h1>Jesaiah Calderon</h1>
      <p class="tagline">IT Support Technician | Aspiring Cybersecurity Professional</p>
      <p class="location">Anaheim, California</p>
    </div>
    <nav class="site-nav" aria-label="Section navigation">
      <a href="#summary">Summary</a>
      <a href="#skills">Skills</a>
      <a href="#experience">Experience</a>
      <a href="#certifications">Certifications</a>
      <a href="#contact">Contact</a>
    </nav>
  </div>
</header>

<main>
  <section id="summary" class="section">
    <h2>Summary</h2>
    <p>
      Motivated IT support professional with hands-on experience in Windows and
      Linux environments, user account management, troubleshooting, and basic
      networking. Currently preparing for CompTIA Security+ and building home lab
      experience in Active Directory, system administration, and security
      fundamentals. Brings a strong customer service background and
      problem-solving skills developed from managing a small business.
    </p>
  </section>

  <section id="skills" class="section">
    <h2>Skills</h2>
    <div class="skills-grid">
      <div class="skill-group">
        <h3>Systems</h3>
        <ul>
          <li>Windows &amp; Linux environments</li>
          <li>Active Directory</li>
          <li>User account management</li>
        </ul>
      </div>
      <div class="skill-group">
        <h3>Security</h3>
        <ul>
          <li>CompTIA Security+ (in progress)</li>
          <li>Google Cybersecurity Certificate</li>
          <li>Security fundamentals home lab</li>
        </ul>
      </div>
      <div class="skill-group">
        <h3>Support</h3>
        <ul>
          <li>Troubleshooting</li>
          <li>Basic networking</li>
          <li>POS systems</li>
          <li>Customer service</li>
        </ul>
      </div>
    </div>
  </section>

  <section id="experience" class="section">
    <h2>Experience</h2>
    <article class="job">
      <h3>Operator — Flowers by Jade</h3>
      <p class="job-meta">Small Business</p>
      <ul>
        <li>Provided daily technical troubleshooting for POS systems, computers, printers, and software</li>
        <li>Managed online orders, website updates, and digital communication platforms</li>
        <li>Delivered high-volume customer support while resolving issues efficiently</li>
        <li>Maintained accurate records, scheduling, and workflow processes</li>
        <li>Demonstrated strong communication, time management, and problem-solving skills</li>
      </ul>
    </article>
  </section>

  <section id="certifications" class="section">
    <h2>Certifications</h2>
    <ul class="cert-list">
      <li>CompTIA Security+</li>
      <li>Google Cybersecurity Certificate</li>
    </ul>
  </section>

  <section id="contact" class="section">
    <h2>Contact</h2>
    <ul class="contact-list">
      <li><a href="mailto:jesaiah.calderon2020@gmail.com">jesaiah.calderon2020@gmail.com</a></li>
      <li><a href="tel:+17143319825">(714) 331-9825</a></li>
      <li><a href="https://www.linkedin.com/in/jesaiah-calderon-a045a029b" target="_blank" rel="noopener">linkedin.com/in/jesaiah-calderon-a045a029b</a></li>
    </ul>
  </section>
</main>

<footer class="site-footer">
  <p>&copy; 2026 Jesaiah Calderon</p>
</footer>

<script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 3: Create empty placeholder-free stubs so the page doesn't 404 during manual check**

Create `/Users/jesaiahcalderon/jesaiahcal.github.io/style.css` with just:

```css
/* populated in Task 2 */
```

Create `/Users/jesaiahcalderon/jesaiahcal.github.io/script.js` with just:

```js
// populated in Task 3
```

- [ ] **Step 4: Manually verify in a browser**

Run: `open /Users/jesaiahcalderon/jesaiahcal.github.io/index.html`

Check:
- Page title bar reads "Jesaiah Calderon — IT Support & Cybersecurity"
- All five section headings are visible in order: Summary, Skills, Experience, Certifications, Contact
- Clicking each nav link (Summary/Skills/Experience/Certifications/Contact) jumps to the matching section
- The email link opens a new email compose window addressed to `jesaiah.calderon2020@gmail.com`
- The phone link is `tel:+17143319825` (right-click → Copy Link, confirm)
- The LinkedIn link opens `https://www.linkedin.com/in/jesaiah-calderon-a045a029b` in a new tab
- Browser console (View → Developer → JavaScript Console) shows no errors

- [ ] **Step 5: Commit**

```bash
cd /Users/jesaiahcalderon/jesaiahcal.github.io
git add .gitignore index.html style.css script.js
git commit -m "Add resume page structure and content"
```

---

### Task 2: Dark cyber theme styling (`style.css`)

**Files:**
- Modify: `/Users/jesaiahcalderon/jesaiahcal.github.io/style.css` (replace placeholder from Task 1)

**Interfaces:**
- Consumes: element/class/id names produced by Task 1 (`site-header`, `header-inner`, `identity`, `tagline`, `location`, `site-nav`, `section`, `skills-grid`, `skill-group`, `job`, `job-meta`, `cert-list`, `contact-list`, `site-footer`, `#bg-canvas`).
- Produces: `#bg-canvas` CSS rules (fixed full-viewport, `pointer-events: none`, low opacity) that Task 3's JS relies on for correct visual placement; `prefers-reduced-motion` media query that hides the canvas as a CSS-level fallback in addition to Task 3's JS-level check.

- [ ] **Step 1: Replace `style.css` placeholder with full stylesheet**

```css
:root {
  --bg: #0a0e14;
  --panel: #0d131d;
  --text: #dbe4ee;
  --text-dim: #93a3b8;
  --accent: #33e0ff;
  --border: rgba(51, 224, 255, 0.25);
  --font-mono: ui-monospace, "SF Mono", "JetBrains Mono", "Fira Code", monospace;
  --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
}

* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}

body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-sans);
  line-height: 1.6;
}

#bg-canvas {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  pointer-events: none;
  opacity: 0.4;
}

@media (prefers-reduced-motion: reduce) {
  #bg-canvas {
    display: none;
  }
}

.site-header {
  position: sticky;
  top: 0;
  z-index: 10;
  background: rgba(10, 14, 20, 0.85);
  backdrop-filter: blur(6px);
  border-bottom: 1px solid var(--border);
}

.header-inner {
  max-width: 760px;
  margin: 0 auto;
  padding: 1.5rem 1.5rem 1rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-end;
  gap: 1rem;
}

.identity h1 {
  font-family: var(--font-mono);
  font-size: 1.5rem;
  margin: 0 0 0.35rem;
  color: var(--text);
}

.tagline {
  margin: 0 0 0.25rem;
  color: var(--accent);
  font-family: var(--font-mono);
  font-size: 0.95rem;
}

.location {
  margin: 0;
  color: var(--text-dim);
  font-size: 0.85rem;
}

.site-nav {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  font-family: var(--font-mono);
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.site-nav a {
  color: var(--text-dim);
  text-decoration: none;
  padding-bottom: 0.2rem;
  border-bottom: 2px solid transparent;
}

.site-nav a:hover,
.site-nav a:focus {
  color: var(--accent);
  border-bottom-color: var(--accent);
}

main {
  max-width: 760px;
  margin: 0 auto;
  padding: 0 1.5rem;
}

.section {
  padding: 2.5rem 0;
  border-bottom: 1px solid var(--border);
}

.section:last-of-type {
  border-bottom: none;
}

.section h2 {
  font-family: var(--font-mono);
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 1.1rem;
  margin: 0 0 1.25rem;
  text-shadow: 0 0 8px rgba(51, 224, 255, 0.35);
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

.skill-group h3 {
  font-family: var(--font-mono);
  font-size: 0.9rem;
  color: var(--text);
  margin: 0 0 0.5rem;
}

.skill-group ul {
  margin: 0;
  padding-left: 1.1rem;
  color: var(--text-dim);
  font-size: 0.9rem;
}

.job h3 {
  margin: 0 0 0.25rem;
  font-size: 1rem;
}

.job-meta {
  margin: 0 0 0.75rem;
  color: var(--text-dim);
  font-size: 0.85rem;
}

.cert-list,
.contact-list {
  list-style: none;
  margin: 0;
  padding: 0;
}

.cert-list li {
  padding: 0.4rem 0;
}

.contact-list li {
  padding: 0.4rem 0;
}

.contact-list a,
.section a {
  color: var(--accent);
  text-decoration: none;
}

.contact-list a:hover,
.section a:hover {
  text-decoration: underline;
}

.site-footer {
  max-width: 760px;
  margin: 0 auto;
  padding: 1.5rem;
  color: var(--text-dim);
  font-size: 0.8rem;
  text-align: center;
}

@media (max-width: 640px) {
  .header-inner {
    flex-direction: column;
    align-items: flex-start;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }
}
```

- [ ] **Step 2: Manually verify in a browser**

Run: `open /Users/jesaiahcalderon/jesaiahcal.github.io/index.html`

Check:
- Background is near-black, body text is light-colored, section headings and links are cyan
- Header stays pinned to the top while scrolling (sticky nav)
- Resize the window down to ~375px wide (or use browser devtools device toolbar) — header stacks vertically, skills grid becomes a single column, no horizontal scrollbar appears
- Section headings have a visible cyan glow/underline treatment

- [ ] **Step 3: Commit**

```bash
cd /Users/jesaiahcalderon/jesaiahcal.github.io
git add style.css
git commit -m "Add dark cyber theme styling"
```

---

### Task 3: Particle network background (`script.js`)

**Files:**
- Modify: `/Users/jesaiahcalderon/jesaiahcal.github.io/script.js` (replace placeholder from Task 1)

**Interfaces:**
- Consumes: `#bg-canvas` element and its CSS positioning/opacity from Task 2.
- Produces: nothing consumed by later tasks (this is the last content task before deploy).

- [ ] **Step 1: Replace `script.js` placeholder with the particle animation**

```js
(function () {
  const canvas = document.getElementById('bg-canvas');
  const prefersReducedMotion = window.matchMedia(
    '(prefers-reduced-motion: reduce)'
  ).matches;

  if (!canvas || prefersReducedMotion) {
    return;
  }

  const ctx = canvas.getContext('2d');
  const DOT_COLOR = '51, 224, 255';
  const MAX_LINK_DISTANCE = 140;
  const PARTICLE_SPEED = 0.15;

  let particles = [];
  let width = 0;
  let height = 0;

  function createParticles(count) {
    const list = [];
    for (let i = 0; i < count; i++) {
      list.push({
        x: Math.random() * width,
        y: Math.random() * height,
        vx: (Math.random() - 0.5) * PARTICLE_SPEED,
        vy: (Math.random() - 0.5) * PARTICLE_SPEED,
      });
    }
    return list;
  }

  function resize() {
    width = canvas.width = window.innerWidth;
    height = canvas.height = window.innerHeight;
    const density = Math.floor((width * height) / 18000);
    const count = Math.max(20, Math.min(density, 70));
    particles = createParticles(count);
  }

  function step() {
    ctx.clearRect(0, 0, width, height);

    for (const p of particles) {
      p.x += p.vx;
      p.y += p.vy;

      if (p.x <= 0 || p.x >= width) p.vx *= -1;
      if (p.y <= 0 || p.y >= height) p.vy *= -1;

      ctx.beginPath();
      ctx.arc(p.x, p.y, 1.5, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(${DOT_COLOR}, 0.6)`;
      ctx.fill();
    }

    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const a = particles[i];
        const b = particles[j];
        const dx = a.x - b.x;
        const dy = a.y - b.y;
        const distance = Math.sqrt(dx * dx + dy * dy);

        if (distance < MAX_LINK_DISTANCE) {
          const alpha = 0.25 * (1 - distance / MAX_LINK_DISTANCE);
          ctx.beginPath();
          ctx.moveTo(a.x, a.y);
          ctx.lineTo(b.x, b.y);
          ctx.strokeStyle = `rgba(${DOT_COLOR}, ${alpha})`;
          ctx.lineWidth = 1;
          ctx.stroke();
        }
      }
    }

    requestAnimationFrame(step);
  }

  window.addEventListener('resize', resize);
  resize();
  requestAnimationFrame(step);
})();
```

- [ ] **Step 2: Manually verify in a browser**

Run: `open /Users/jesaiahcalderon/jesaiahcal.github.io/index.html`

Check:
- Faint drifting dots with occasional connecting lines are visible behind the page content, moving slowly
- The animation stays behind text and never blocks clicking links or selecting text
- Resize the browser window — the canvas resizes to fill the new viewport without stretching or leaving gaps
- Open devtools → Rendering tab → set "Emulate CSS media feature prefers-reduced-motion" to "reduce", then reload the page — the canvas is hidden and no animation runs
- Browser console shows no errors

- [ ] **Step 3: Commit**

```bash
cd /Users/jesaiahcalderon/jesaiahcal.github.io
git add script.js
git commit -m "Add subtle particle network background animation"
```

---

### Task 4: Publish to GitHub Pages

**Files:**
- None (this task is git/GitHub operations only, no file changes beyond what Tasks 1-3 already created).

**Interfaces:**
- Consumes: the fully built site from Tasks 1-3 and the existing local git repo at `/Users/jesaiahcalderon/jesaiahcal.github.io` (already initialized with one commit from the design spec).
- Produces: the live site at `https://jesaiahcal.github.io`.

- [ ] **Step 1: User creates the empty GitHub repo (manual, in browser)**

Since this is a real GitHub account action, do this yourself rather than via automation:

1. Go to https://github.com/new
2. Repository name: `jesaiahcal.github.io` (must match exactly)
3. Visibility: Public
4. Do **not** check "Add a README file", and leave `.gitignore` and license set to "None" — the local repo already has commits, and adding files on GitHub's side would create conflicting history on first push
5. Click "Create repository"

- [ ] **Step 2: Add the GitHub remote and push**

```bash
cd /Users/jesaiahcalderon/jesaiahcal.github.io
git branch -M main
git remote add origin https://github.com/jesaiahcal/jesaiahcal.github.io.git
git push -u origin main
```

Expected: push succeeds, output ends with something like `branch 'main' set up to track 'origin/main'`.

- [ ] **Step 3: Verify the live site**

Wait about 1 minute for GitHub Pages to build, then open `https://jesaiahcal.github.io` in a browser.

Check:
- The page loads with the same content and dark theme as the local version
- The particle background animates
- All nav links, email, phone, and LinkedIn links work the same as they did locally
- No mixed-content warnings or console errors on the live URL

- [ ] **Step 4: Commit any final tweaks (if verification on the live site surfaced issues)**

If everything matched, there is nothing to commit — the site is done. If you had to fix anything to match the live site, commit and push again:

```bash
cd /Users/jesaiahcalderon/jesaiahcal.github.io
git add -A
git commit -m "Fix issue found in live verification"
git push
```
