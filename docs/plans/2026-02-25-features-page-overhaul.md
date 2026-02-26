# Features Page Overhaul - Plan v4

## Problem

Every AI tool starts you from zero. Every session, you re-explain your context, your preferences, your projects. Your knowledge lives in 12 different apps. Your tasks fall through cracks between tools. You spend more time managing AI than getting helped by it.

The current features.html fails to tell this story. It's a feature dump: 99 agents listed individually, 15 module cards, dense grids. It reads like documentation, not a product page.

## Inspiration: fairdrive.xyz

- Alternating two-column layouts (text left, visual right, then swap)
- Philosophy woven into the narrative, not a separate section
- Scroll-reveal animations for progressive disclosure
- Story-driven, not feature-driven

## New Page Structure (6 sections)

### 1. Hero - Name the Problem

**Category label:** "AI second brain" (small, above headline)

**Headline: "Every AI session starts from zero. This one doesn't."**

**Subtitle: "Datacore remembers everything. So your AI never starts from zero."**

### 1.5. The Shareable Moment - Before/After Split Screen

Immediately after the hero. This is the single element people screenshot and share. Full width, visually dominant.

**Left panel (muted/grey):** Generic AI chat bubble: "Hi! How can I help you today?"
**Right panel (vibrant/accent):** Datacore session: "Good morning. Your board deck is priority - I've drafted 3 slides based on yesterday's pricing strategy work."

This is the Purple Cow. The contrast is visceral, not explained. On mobile, this becomes a tap-to-toggle interaction: tap to flip between the two states, preserving the simultaneous comparison that makes it powerful.

### 2. "A Day with Datacore" - You Are the Hero

Alternating text+terminal mockup pairs. Every annotation focuses on what YOU achieve. Terminals capped at 3-4 lines.

**Morning: "You sit down with coffee. In 10 seconds, you know exactly what matters today."**

Terminal: `/today` — **HERO-SIZED** (full-width, largest element on page)
```
Overnight: Competitive analysis complete. Draft blog ready.
Priority: Board deck (Thursday). 3 key slides need your decision.
From yesterday: Your pricing strategy insight → ready to cite.
```
The emotional payoff. You slept, and your work moved forward. This terminal is the centerpiece of the entire page.

**Midday: "Seven things in your inbox. Two minutes later, zero."**

Terminal: `process inbox` — standard size
```
"Review investor deck" → What's the next action? → "Draft 3 key slides"
"Check staking rates" → Tagged for tonight's research
5 more routed. Inbox clear.
```

**End of day: "Everything you learned today is captured. Without you doing anything."**

Terminal: `/wrap-up` — standard size
```
Journal updated. 2 patterns learned. 1 zettel created.
Tomorrow you'll remember what today's you figured out.
```

**Night: "Tag it. Sleep. Wake up to finished work."**

Terminal: `/tomorrow` — standard size
```
4 tasks queued for overnight. 20 evaluator personas reviewing each.
Results in tomorrow's /today briefing.
```

**The loop compounds.** Day 1, you explain your project. Day 30, it reminds you of the insight you had three weeks ago, right when you need it for today's meeting. Friday, your weekly review surfaces the three projects that stalled and the two commitments you almost forgot. Nothing is lost.

### 3. Three Things That Make This Different

Three cards. User is the agent in every sentence. No DIP references on the cards themselves.

1. **You explain your project once.**
   A month later, your AI surfaces that exact insight in the meeting where you need it. Not because it has a chat history - because it learned your preferences, your project context, your communication style as structured knowledge that compounds with every session.

2. **You tag a task. You go to sleep. You wake up to finished work.**
   Research, writing, analysis done overnight. Each output reviewed by 20 evaluator personas - Hemingway checks clarity, Feynman checks first principles. Quality work, not hallucinations.

3. **Your knowledge stays yours. Forever.**
   Plain text files on your machine. Markdown and org-mode you can read in any editor, in 50 years. Your insight from six months ago surfaces when it matters. The intelligence layer is open-source software you can inspect, modify, and host yourself.

After the three cards, a single subtle link: "See how it works: Open specifications on GitHub →"

### 4. Extend It

Two-column layout:

**Left: Modules for your domain**
Three clean typographic lists with verb phrases:
- **Work**: Meetings (auto-notes from transcripts), Mail (classify and prioritize), CRM (track relationship health)
- **Knowledge**: Research (multi-source synthesis), News (personalized digest), Datacortex (semantic search)
- **Personal**: Trading (framework-driven journaling), Health (routine optimization), Finance (portfolio tracking)

**Right: Built on open specifications**
A growing library of Datacore Improvement Proposals defines system behavior. 4 privacy layers protect your data. Designed for community governance - and we're building that community now.

Honest about the project's stage. Links to: DIP repository, contribution model, module creation guide.

MIT Licensed. (Or actual license - stated prominently.)

### 5. Get Started

Two side-by-side pathways:

**Early Access** - Email capture form. "No migration. No data import. Start a session, do your work. Datacore learns as you go." Addresses adoption fear directly.

**Explore the Code** - "[License]. Clone the repo. Read the specs. Build a module." Link to GitHub, CONTRIBUTING.md, getting-started tutorial.

## Design Approach

- **Alternating layouts** for the workflow section
- **Before/after split screen**: full-width, immediately after hero. Left muted, right vibrant. Mobile: tap-to-toggle interaction
- **Terminal hierarchy**: `/today` is full-width hero-sized (1.25x font, extra padding); others are standard narrower terminals
- **Scroll-reveal**: animate ONLY the terminals (they "appear" as you scroll, reinforcing the system-responds metaphor). Text sections simply exist - no animation
- **Plain-English annotations** above each terminal for non-technical visitors
- **Canvas animation**: 30% opacity on features page. No animation behind terminals (CSS `position: relative; z-index: 1; background: var(--section-bg)` on terminal sections)
- **Module lists**: typographic, no cards. Verb phrases for each module
- **Single "See how it works" link** for technical depth - not on individual cards

## Mobile Strategy

Explicit design decisions for < 768px:

1. **Before/after split screen**: Becomes a tap-to-toggle card. User taps to flip between "Before" and "After" states. Both states visible but one at a time. This preserves the comparison impact that vertical stacking would destroy.

2. **Terminal mockups**: Responsive font size using `clamp(0.7rem, 2.5vw, 0.875rem)`. Natural text wrapping, NOT horizontal scroll. Terminals are 3-4 short lines - they fit naturally when text wraps.

3. **Alternating layouts**: Stack vertically. Annotation text first, terminal below. Reading order preserved.

4. **Two-column "Extend It"**: Stacks to single column. Modules first, governance below.

5. **Anchor nav**: Collapses to hamburger or horizontal scroll pills.

6. **Get Started pathways**: Stack vertically. Email capture first (primary action), code pathway below.

## What Gets Cut

- Individual agent listings → "99 agents" as proof point only
- Individual module cards for all 23 → clean typographic lists with verb phrases
- Evolution steps section → folded into workflow
- Principles section → embedded in story
- Separate positioning section → contrast built into capability cards and split screen
- Separate philosophy section → woven throughout
- DIP references on product cards → single link after cards

## Technical Notes

- Same CSS design system as index.html (variables, card-bg, backdrop-filter)
- Sacred geometry canvas at 30% opacity on features page
- Terminal mockup component (`.terminal-window` with `.terminal-header` + `.terminal-body`)
- Before/after component (`.comparison-split` with `.comparison-before` + `.comparison-after`)
- Anchor nav in header for section jumping
- `datacore-theme` localStorage key (matches index.html)
- Scroll-reveal via IntersectionObserver, targeting `.terminal-window` elements only

## Evaluator Feedback Log

### Round 1 (v1) - Average: 0.676
| Persona | Score | Key Issue |
|---------|-------|-----------|
| Godin | 0.72 | No antagonist, defensive positioning |
| Jobs | 0.68 | 6 cards too many, no aha moment |
| Nielsen | 0.61 | Fails 10-second test, no anchor nav |
| Allen | 0.79 | Missing capture step |
| Swartz | 0.58 | No evidence, no contributor pathway |

### Round 2 (v2) - Average: 0.749
| Persona | Score | Key Issue |
|---------|-------|-----------|
| Godin | 0.78 | No remarkable/shareable moment |
| Jobs | 0.76 | Sections overlap, terminals too long |
| Nielsen | 0.72 | Subtitle still overloaded, no mobile plan |
| Allen | 0.82 | Missing weekly review mention |
| Swartz | 0.67 | Governance outpaces reality |
| Tufte | 0.74 | No visual hierarchy between terminals |
| Sierra | 0.75 | Product is hero, not user |

### Round 3 (v3) - Average: 0.840
| Persona | Score | Key Issue |
|---------|-------|-----------|
| Godin | 0.84 | Split screen placement uncommitted |
| Jobs | 0.86 | DIP refs break flow on product cards |
| Nielsen | 0.83 | Mobile plan is CSS fragment |
| Allen | 0.87 | Weekly review still absent |
| Swartz | 0.80 | DIP count verifiability, no license |
| Tufte | 0.82 | Scroll animations uniform, module lists bare |
| Sierra | 0.86 | Cards regress to system-as-hero |

### Changes for v4
1. Before/after split screen committed to section 1.5 with full visual dominance
2. Single shareable moment (split screen), single emotional payoff (`/today` terminal) - no competition
3. Mobile: tap-to-toggle for split screen, responsive font sizing for terminals, NO horizontal scroll
4. DIP references removed from capability cards; single "See how it works" link below
5. Module lists enhanced with verb phrases for each item
6. Weekly review mentioned in "The loop compounds" paragraph
7. License stated prominently in contributor pathway
8. Capability card copy rewritten with user as subject throughout
9. Scroll-reveal limited to terminals only (text sections don't animate)
10. DIP count changed to "A growing library of..." avoiding verifiability issues
