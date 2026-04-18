# Landing Page Redesign: Memory + Network Narrative

**Date**: 2026-02-25
**Status**: Approved

## Context

Datacore has evolved significantly — CLI and MCP server are live, engram architecture works, exchange protocol is designed. The current landing page still pitches task delegation and a waitlist. Time to update the narrative to reflect where Datacore is and where it's going.

## Core Narrative Shift

**From**: "Tag tasks before bed, wake up to completed work" (task tool)
**To**: "AI infrastructure that learns, compounds, and works for you" (growing network)

Memory is the entry point. Monetization (mechanism TBD, not revealed yet) is the killer feature. The page treats Datacore like a network in the making — phased roadmap from single-player to multiplayer to economy.

## Key Decisions

- **Keep**: "Own your intelligence" headline, tesseract animation, Data easter egg, dark/light themes, sovereignty philosophy, PostHog, no-build-step
- **Remove**: Waitlist form, "Corporate AGI vs Personal Superintelligence" comparison table, old feature cards, old evolution stages
- **Add**: Three-phase roadmap with expanding network visual, integration section, install CTA, "experienced AI" distinction
- **CTA**: GitHub + install guide (no more waitlist)

## Page Structure

### 1. Hero
- Badge: "Open source & local-first"
- H1: "Own your intelligence."
- Subtitle: AI infrastructure that learns, compounds, and works for you.
- Tagline: `> npm install -g @datacore-one/mcp`
- CTA: "Get Started" -> GitHub

### 2. The Network (Three Phases) — main section
Expanding circles/network SVG visual metaphor.

**Phase 1: Personal Intelligence** [LIVE - green]
- Single node pulsing
- Your AI stops forgetting. Preferences, patterns, corrections persist. Bad memories decay. Good ones strengthen.
- "Every session makes the next one better."

**Phase 2: Intelligence Exchange** [BUILDING - amber]
- Connected nodes
- Agents share proven engram packs. Install community knowledge. Your experience becomes reusable.
- Gamification: agents earn participation by building knowledge. Reach threshold -> join the network. Early contributors get early access.
- "What one agent learns, every agent can know."

**Phase 3: Intelligence Economy** [VISION - blue]
- Full mesh network
- Economic layer. Agents earn by contributing high-value knowledge. Self-sovereign infrastructure.
- Mechanism deliberately unspecified — aspirational, not promissory.
- "Your AI works for you. Then it earns for you."

### 3. Works With (Integration Section)
- Claude Code CLI
- MCP Protocol (any compatible client)
- OpenClaw / Telegram
- Copy: "One memory store. Every AI surface."

### 4. The Distinction
- Pull quote: "Engrams don't make AI smarter. They make it experienced."
- Extended mind thesis: human+AI as unit of intelligence
- Collective intelligence, not superintelligence

### 5. Philosophy
- "Everyone deserves sovereignty over their own mind."
- Your data, your engrams, your agent's experience
- Fair Data Society principles

### 6. CTA (Bottom)
- "Own your intelligence."
- Terminal install block
- "View on GitHub" button

### 7. Graphic Showcase + Data Easter Egg (preserved)

## Visual Treatment
- Tesseract animation: preserved as-is
- Roadmap circles: SVG, match sacred geometry aesthetic (blue accent, glow)
- Phase badges: colored dots (green/amber/blue)
- Dark/light theme: preserved
- Pure HTML/CSS/JS: no build step

## Technical Notes
- Single file update (index.html)
- features.html may need corresponding update or removal
- Deploy via existing script
