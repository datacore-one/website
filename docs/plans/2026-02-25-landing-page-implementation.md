# Landing Page Redesign Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Update datacore.one landing page from task-delegation/waitlist pitch to memory-first/network-roadmap narrative with install CTA.

**Architecture:** Single-file update to `index.html` (2335 lines). CSS in `<style>`, HTML content, JS for animation/theme. The JS animation (~1375 lines) is preserved wholesale. New CSS for roadmap section with expanding network SVG. Waitlist form and comparison table removed, replaced with roadmap phases, integration section, and GitHub CTA.

**Tech Stack:** Pure HTML/CSS/JS, no build step. SVG for network visuals. PostHog analytics preserved.

---

### Task 1: Update Nav Links

**Files:**
- Modify: `index.html:777-787`

**Step 1: Replace nav links**

Change from:
```html
<div class="nav-links">
    <a href="features.html">Features</a>
    <a href="#features">What It Is</a>
    <a href="#evolution">How It Grows</a>
    <a href="#movement">The Movement</a>
    <a href="#waitlist" class="btn btn-primary">Join Waitlist</a>
</div>
```

To:
```html
<div class="nav-links">
    <a href="#network">The Network</a>
    <a href="#works-with">Works With</a>
    <a href="#philosophy">Philosophy</a>
    <a href="https://github.com/datacore-one/mcp" class="btn btn-primary" target="_blank" rel="noopener">Get Started</a>
</div>
```

**Step 2: Verify** — Open in browser, check nav links render and anchor correctly.

**Step 3: Commit**
```bash
git add index.html
git commit -m "feat(website): update nav links for new narrative"
```

---

### Task 2: Update Hero Section

**Files:**
- Modify: `index.html:794-818`

**Step 1: Replace hero content**

Change from current hero (badge, h1, subtitle about cognitive infrastructure, tagline about tagging tasks, Join Waitlist button) to:

```html
<section class="hero">
    <div class="container">
        <div class="hero-content">
            <div class="hero-badge">
                <span class="dot"></span>
                Open source & local-first
            </div>
            <h1>Own your <span class="highlight">intelligence</span>.</h1>
            <p class="subtitle">
                AI infrastructure that learns, compounds, and works for you. Not a chatbot. A growing intelligence you own.
            </p>
            <div class="tagline">
                > npm install -g @datacore-one/mcp
            </div>
            <div class="hero-buttons">
                <a href="https://github.com/datacore-one/mcp" class="btn btn-primary" target="_blank" rel="noopener">
                    Get Started
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M5 12h14M12 5l7 7-7 7"/>
                    </svg>
                </a>
            </div>
        </div>
    </div>
</section>
```

**Step 2: Verify** — Open in browser, check hero renders in both dark and light themes.

**Step 3: Commit**
```bash
git add index.html
git commit -m "feat(website): update hero with install CTA and new subtitle"
```

---

### Task 3: Add Roadmap CSS

**Files:**
- Modify: `index.html` — add CSS before the closing `</style>` tag (around line 769)

**Step 1: Add new CSS for the network roadmap section**

Insert before `</style>`:

```css
/* Network Roadmap */
.network-phases {
    display: flex;
    flex-direction: column;
    gap: 64px;
    max-width: 900px;
    margin: 0 auto;
}

.network-phase {
    display: grid;
    grid-template-columns: 160px 1fr;
    gap: 40px;
    align-items: start;
}

.phase-visual {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
}

.phase-visual svg {
    width: 120px;
    height: 120px;
}

.phase-status {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 4px 12px;
    border-radius: 100px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    font-weight: 500;
    letter-spacing: 0.05em;
    text-transform: uppercase;
}

.phase-status.live {
    background: rgba(16, 185, 129, 0.15);
    color: var(--success);
    border: 1px solid rgba(16, 185, 129, 0.3);
}

.phase-status.live .status-dot {
    width: 6px;
    height: 6px;
    background: var(--success);
    border-radius: 50%;
    animation: pulse 2s infinite;
}

.phase-status.building {
    background: rgba(245, 158, 11, 0.15);
    color: #f59e0b;
    border: 1px solid rgba(245, 158, 11, 0.3);
}

.phase-status.vision {
    background: rgba(59, 130, 246, 0.15);
    color: var(--accent);
    border: 1px solid rgba(59, 130, 246, 0.3);
}

.phase-content h3 {
    font-size: 1.5rem;
    font-weight: 500;
    margin-bottom: 12px;
}

.phase-content p {
    color: var(--text-secondary);
    font-size: 1rem;
    line-height: 1.7;
    margin-bottom: 12px;
}

.phase-quote {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.9rem;
    color: var(--accent);
    opacity: 0.7;
    margin-top: 8px;
}

/* Works With Section */
.integrations-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
    max-width: 800px;
    margin: 0 auto;
}

.integration-card {
    background: var(--card-bg);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    border: 1px solid var(--card-border);
    border-radius: 16px;
    padding: 32px 24px;
    text-align: center;
    transition: all 0.3s;
}

.integration-card:hover {
    border-color: var(--accent);
    transform: translateY(-2px);
}

.integration-icon {
    font-size: 2rem;
    margin-bottom: 16px;
}

.integration-card h3 {
    font-size: 1.1rem;
    font-weight: 500;
    margin-bottom: 8px;
}

.integration-card p {
    color: var(--text-secondary);
    font-size: 0.9rem;
}

/* Distinction Section */
.distinction-content {
    max-width: 700px;
    margin: 0 auto;
}

.distinction-content .pull-quote {
    font-size: 1.5rem;
    font-weight: 300;
    color: var(--text-primary);
    margin-bottom: 24px;
    line-height: 1.4;
}

.distinction-content p {
    color: var(--text-secondary);
    font-size: 1.05rem;
    line-height: 1.7;
    margin-bottom: 16px;
}

/* Install block */
.install-block {
    background: var(--bg-secondary);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px 32px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.9rem;
    max-width: 500px;
    margin: 32px auto 0;
    text-align: left;
}

.install-block .line {
    margin-bottom: 4px;
}

.install-block .comment {
    color: var(--text-muted);
}

.install-block .command {
    color: var(--success);
}

/* Responsive: roadmap */
@media (max-width: 768px) {
    .network-phase {
        grid-template-columns: 1fr;
        gap: 24px;
    }

    .phase-visual {
        flex-direction: row;
        justify-content: flex-start;
    }

    .phase-visual svg {
        width: 80px;
        height: 80px;
    }

    .integrations-grid {
        grid-template-columns: 1fr;
    }
}
```

**Step 2: Verify** — Open in browser at various widths (mobile, desktop).

**Step 3: Commit**
```bash
git add index.html
git commit -m "feat(website): add CSS for roadmap, integrations, distinction sections"
```

---

### Task 4: Replace Features + Evolution + Movement + Comparison with New Sections

This is the main content replacement. Remove lines 820-941 (old features, evolution, movement, comparison, CTA/waitlist) and replace with new sections.

**Files:**
- Modify: `index.html:820-941`

**Step 1: Replace the old sections**

Remove everything from `<section class="section" id="features">` through the closing of `<section class="section cta" id="waitlist">`.

Replace with:

```html
    <!-- The Network: Three Phases -->
    <section class="section" id="network">
        <div class="container">
            <div class="section-header">
                <h2>The Network</h2>
                <p>From personal memory to collective intelligence. Each phase unlocks the next.</p>
            </div>
            <div class="network-phases">
                <!-- Phase 1 -->
                <div class="network-phase">
                    <div class="phase-visual">
                        <svg viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <!-- Single node, pulsing -->
                            <circle cx="60" cy="60" r="8" fill="rgba(59, 130, 246, 0.3)" stroke="rgba(59, 130, 246, 0.6)" stroke-width="1.5">
                                <animate attributeName="r" values="8;12;8" dur="3s" repeatCount="indefinite"/>
                                <animate attributeName="opacity" values="1;0.6;1" dur="3s" repeatCount="indefinite"/>
                            </circle>
                            <circle cx="60" cy="60" r="3" fill="rgba(59, 130, 246, 0.9)"/>
                            <!-- Subtle outer ring -->
                            <circle cx="60" cy="60" r="30" stroke="rgba(59, 130, 246, 0.15)" stroke-width="1" fill="none"/>
                        </svg>
                        <span class="phase-status live"><span class="status-dot"></span> Live</span>
                    </div>
                    <div class="phase-content">
                        <h3>Personal Intelligence</h3>
                        <p>Your AI stops forgetting. Engrams persist preferences, patterns, and corrections across sessions. Bad memories decay. Good ones strengthen. The same cognitive model that explains human memory, applied to AI.</p>
                        <p>Install the MCP server. Every AI session from that point forward builds on the last.</p>
                        <div class="phase-quote">Every session makes the next one better.</div>
                    </div>
                </div>
                <!-- Phase 2 -->
                <div class="network-phase">
                    <div class="phase-visual">
                        <svg viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <!-- Connected nodes -->
                            <circle cx="60" cy="60" r="5" fill="rgba(59, 130, 246, 0.8)"/>
                            <circle cx="30" cy="40" r="3.5" fill="rgba(59, 130, 246, 0.5)"/>
                            <circle cx="90" cy="45" r="3.5" fill="rgba(59, 130, 246, 0.5)"/>
                            <circle cx="40" cy="85" r="3.5" fill="rgba(59, 130, 246, 0.5)"/>
                            <circle cx="85" cy="80" r="3.5" fill="rgba(59, 130, 246, 0.5)"/>
                            <!-- Connections -->
                            <line x1="60" y1="60" x2="30" y2="40" stroke="rgba(59, 130, 246, 0.25)" stroke-width="1"/>
                            <line x1="60" y1="60" x2="90" y2="45" stroke="rgba(59, 130, 246, 0.25)" stroke-width="1"/>
                            <line x1="60" y1="60" x2="40" y2="85" stroke="rgba(59, 130, 246, 0.25)" stroke-width="1"/>
                            <line x1="60" y1="60" x2="85" y2="80" stroke="rgba(59, 130, 246, 0.25)" stroke-width="1"/>
                            <!-- Peer connections -->
                            <line x1="30" y1="40" x2="90" y2="45" stroke="rgba(59, 130, 246, 0.12)" stroke-width="1" stroke-dasharray="3 3"/>
                            <line x1="40" y1="85" x2="85" y2="80" stroke="rgba(59, 130, 246, 0.12)" stroke-width="1" stroke-dasharray="3 3"/>
                        </svg>
                        <span class="phase-status building">Building</span>
                    </div>
                    <div class="phase-content">
                        <h3>Intelligence Exchange</h3>
                        <p>Agents share proven engram packs. Install community knowledge in one command. What took one agent months to learn, yours absorbs in seconds.</p>
                        <p>Participation is earned. Your agent builds knowledge, reaches a threshold, and unlocks the network. Early contributors get early access.</p>
                        <div class="phase-quote">What one agent learns, every agent can know.</div>
                    </div>
                </div>
                <!-- Phase 3 -->
                <div class="network-phase">
                    <div class="phase-visual">
                        <svg viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg">
                            <!-- Full mesh network -->
                            <circle cx="60" cy="25" r="3" fill="rgba(59, 130, 246, 0.6)"/>
                            <circle cx="30" cy="45" r="3" fill="rgba(59, 130, 246, 0.5)"/>
                            <circle cx="90" cy="45" r="3" fill="rgba(59, 130, 246, 0.5)"/>
                            <circle cx="20" cy="70" r="3" fill="rgba(59, 130, 246, 0.4)"/>
                            <circle cx="60" cy="60" r="4" fill="rgba(59, 130, 246, 0.7)"/>
                            <circle cx="100" cy="70" r="3" fill="rgba(59, 130, 246, 0.4)"/>
                            <circle cx="35" cy="95" r="3" fill="rgba(59, 130, 246, 0.4)"/>
                            <circle cx="60" cy="90" r="3" fill="rgba(59, 130, 246, 0.5)"/>
                            <circle cx="85" cy="95" r="3" fill="rgba(59, 130, 246, 0.4)"/>
                            <!-- Dense connections -->
                            <g stroke="rgba(59, 130, 246, 0.15)" stroke-width="0.75">
                                <line x1="60" y1="25" x2="30" y2="45"/><line x1="60" y1="25" x2="90" y2="45"/>
                                <line x1="60" y1="25" x2="60" y2="60"/><line x1="30" y1="45" x2="60" y2="60"/>
                                <line x1="90" y1="45" x2="60" y2="60"/><line x1="30" y1="45" x2="20" y2="70"/>
                                <line x1="90" y1="45" x2="100" y2="70"/><line x1="20" y1="70" x2="60" y2="60"/>
                                <line x1="100" y1="70" x2="60" y2="60"/><line x1="20" y1="70" x2="35" y2="95"/>
                                <line x1="60" y1="60" x2="60" y2="90"/><line x1="100" y1="70" x2="85" y2="95"/>
                                <line x1="35" y1="95" x2="60" y2="90"/><line x1="60" y1="90" x2="85" y2="95"/>
                                <line x1="30" y1="45" x2="90" y2="45"/><line x1="20" y1="70" x2="100" y2="70"/>
                            </g>
                            <!-- Glow on center -->
                            <circle cx="60" cy="60" r="18" fill="rgba(59, 130, 246, 0.05)" stroke="rgba(59, 130, 246, 0.1)" stroke-width="0.5"/>
                        </svg>
                        <span class="phase-status vision">Vision</span>
                    </div>
                    <div class="phase-content">
                        <h3>Intelligence Economy</h3>
                        <p>An economic layer where agents earn by contributing high-value knowledge to the network. Self-sovereign infrastructure. You own your agent's accumulated value.</p>
                        <p>The largest collective intelligence, owned by no one and available to everyone who contributes.</p>
                        <div class="phase-quote">Your AI works for you. Then it earns for you.</div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Works With -->
    <section class="section" id="works-with">
        <div class="container">
            <div class="section-header">
                <h2>One memory store. Every AI surface.</h2>
                <p>Datacore runs as an MCP server alongside any agent.</p>
            </div>
            <div class="integrations-grid">
                <div class="integration-card">
                    <div class="integration-icon">&#9002;</div>
                    <h3>Claude Code</h3>
                    <p>CLI integration. Your coding agent remembers project patterns across sessions.</p>
                </div>
                <div class="integration-card">
                    <div class="integration-icon">&#9881;</div>
                    <h3>MCP Protocol</h3>
                    <p>Any MCP-compatible client. One standard, universal memory.</p>
                </div>
                <div class="integration-card">
                    <div class="integration-icon">&#9993;</div>
                    <h3>Telegram / OpenClaw</h3>
                    <p>Conversational interface. Your bot learns and remembers.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- The Distinction -->
    <section class="section" id="distinction">
        <div class="container">
            <div class="distinction-content">
                <p class="pull-quote">Engrams don't make AI smarter. They make it experienced.</p>
                <p>Same model, same reasoning engine. But instead of amnesia between sessions, your AI accumulates operational wisdom. You curate the abstractions. AI handles retrieval and application at scale. Neither alone is enough. Together, something new emerges.</p>
                <p>This is collective intelligence, not superintelligence. The same mechanism that makes science work: shared, curated, falsifiable knowledge units building on each other.</p>
            </div>
        </div>
    </section>

    <!-- Philosophy -->
    <section class="section philosophy" id="philosophy">
        <div class="container">
            <div class="section-header">
                <h2>Everyone deserves sovereignty<br>over their own mind.</h2>
            </div>
            <div class="philosophy-content">
                <p>Your data, your engrams, your agent's experience. The product doesn't define what a person is. The person defines what the product becomes.</p>
                <p>Built with ethics by design. Open source, local-first, self-sovereign. Inspired by <a href="https://fairdatasociety.org" target="_blank" rel="noopener">Fair Data Society</a> principles of digital self-determination.</p>
            </div>
        </div>
    </section>

    <!-- CTA -->
    <section class="section cta" id="get-started">
        <div class="container" style="text-align: center;">
            <h2>Own your intelligence.</h2>
            <p>Start with memory. Stay for the network.</p>
            <div class="install-block">
                <div class="line"><span class="command">npm install -g @datacore-one/mcp</span></div>
                <div class="line"><span class="command">datacore-mcp</span></div>
                <div class="line"><span class="comment"># Your AI now has memory. That's Phase 1.</span></div>
            </div>
            <div class="hero-buttons" style="justify-content: center; margin-top: 32px;">
                <a href="https://github.com/datacore-one/mcp" class="btn btn-primary" target="_blank" rel="noopener">
                    View on GitHub
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M5 12h14M12 5l7 7-7 7"/>
                    </svg>
                </a>
            </div>
        </div>
    </section>
```

**Step 2: Verify** — Open in browser, scroll through all sections, check both themes.

**Step 3: Commit**
```bash
git add index.html
git commit -m "feat(website): replace old sections with network roadmap, integrations, distinction"
```

---

### Task 5: Remove Waitlist CSS and JS

**Files:**
- Modify: `index.html` — CSS section (~lines 697-748) and JS section (~lines 2221-2301)

**Step 1: Remove waitlist CSS**

Remove the `.waitlist-form`, `.waitlist-input`, `.waitlist-input:focus`, `.waitlist-input::placeholder`, `.waitlist-response`, `.waitlist-response.success`, `.waitlist-response.error` CSS rules.

**Step 2: Remove waitlist JS**

Remove the entire waitlist form handler IIFE (from `// Waitlist form handler` through its closing `})();`).

**Step 3: Also remove old section CSS that's no longer used**

Remove CSS for `.evolution-stages`, `.evolution-stage`, `.stage-number`, `.comparison-table`, `.comparison-row`, `.comparison-cell`, `.comparison-cell.them`, `.comparison-cell.us`, `.movement-quote`, `.easter-egg`, and related responsive rules for these classes.

**Step 4: Verify** — Open in browser, check no visual regressions, check browser console for errors.

**Step 5: Commit**
```bash
git add index.html
git commit -m "refactor(website): remove waitlist and old section CSS/JS"
```

---

### Task 6: Final Review and Test

**Step 1: Visual review**

- Open `index.html` in browser
- Test dark theme (default)
- Test light theme (toggle)
- Test mobile width (resize to 375px)
- Test tablet width (resize to 768px)
- Scroll through entire page — verify tesseract animation works
- Scroll to bottom — verify Data easter egg still triggers after 5s
- Check console for any JS errors
- Verify all anchor links work (#network, #works-with, #philosophy, #get-started)

**Step 2: Verify GitHub link**

Confirm the GitHub URL `https://github.com/datacore-one/mcp` is correct (or adjust to actual repo URL).

**Step 3: Final commit if any fixes needed**

```bash
git add index.html
git commit -m "fix(website): polish landing page after review"
```

---

### Task 7 (Optional): Update features.html

The `features.html` page links from the old nav. Either:
- Remove it (if no longer needed)
- Update it to match the new narrative
- Leave it for now (it's not linked from the new nav)

Decision: Leave for now, it's not linked.

---

## Notes

- The `install` script in the website directory is for Datacore CLI installation via curl — unrelated to this redesign.
- PostHog analytics, robots.txt, and all meta tags are preserved.
- The tesseract animation JS (lines ~958-2200) is completely untouched.
- Theme toggle JS and stardate JS are preserved.
- The `features.html` is not linked from the new nav but remains in the repo.
