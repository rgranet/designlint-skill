---
name: designlint
version: 1.2.0
author: Ruben Granet
description: >
  Force distinctive, human-feeling UI/UX design before writing any code. Use this skill
  whenever building or designing any interface — web apps, landing pages, dashboards,
  iOS/SwiftUI screens, Android/Compose screens, or any UI component. Also use this skill
  when the user asks to review, critique, audit, or improve an existing interface.
  Mandatory when the user says "build a UI", "create a screen", "design a component",
  "make it look good", "design the UX", "review this design", "what's wrong with this UI",
  "improve this interface", or asks for any frontend/interface/experience work. This skill
  operates in two modes: CREATE mode (9 decisions + human critique before code) and AUDIT
  mode (diagnose an existing interface against the same standards and produce an improvement
  plan). It produces design that feels human — not just different, but intentional, empathetic,
  and crafted.
compatibility: claude-code, cursor, codex, copilot
---

# DesignLint

> **TL;DR** — AI agents produce interfaces that all look and feel the same. DesignLint fixes this in two modes: **Create** (understand the user, make 9 deliberate design decisions, resolve a creative tension, critique the result — before shipping) and **Audit** (diagnose an existing interface, identify what's generic, and produce a concrete improvement plan). The goal isn't just different. It's human.

---

## The Problem This Skill Solves

AI coding agents converge — at every level. Left unconstrained, they default to:

**UI convergence:**
- **Typography**: Inter, Roboto, or system fonts
- **Colors**: Purple/blue gradients, white backgrounds, gray text
- **Layout**: Centered column, 4px grid multiples, predictable spacing
- **Components**: shadcn/ui defaults, rounded-xl cards, subtle shadows
- **Motion**: opacity fade-in, nothing else

**UX convergence:**
- **Navigation**: Tab bar (5 icons) → List → Push detail. Always.
- **Actions**: Tap → Modal → Form → Submit → Toast. Always.
- **Feedback**: Green toast bottom-right for success, red for error. Always.
- **Empty states**: Centered illustration + one CTA. Always.
- **Onboarding**: 3-screen carousel with illustrations. Always.
- **Data entry**: Full form with a Submit button. Always.

**Human convergence (the deeper problem):**
- No understanding of who uses the product or how they feel
- Aesthetic choices disconnected from context or audience
- Archetypes copied instead of used as departure points
- Generic microcopy ("Submit", "Cancel", "Are you sure?")
- No creative tension — just safe, obvious choices
- No self-critique — first draft ships as final

This skill breaks all three layers.

---

## Two Modes

DesignLint operates in two modes depending on the task:

### → Create Mode (default)
When the user asks to **build, design, or create** an interface.
Follows the full protocol: Phase 0 → Phase 1 (9 decisions) → Phase 2 (brief) → Phase 3 (build) → Phase 4 (audit) → Phase 5 (critique).

### → Audit Mode
When the user asks to **review, critique, audit, fix, or improve** an existing interface — whether provided as a screenshot, a URL, code, or a description.
Follows the Audit Protocol documented at the end of this file: Diagnosis → Convergence Score → Improvement Brief → Execution.

**How to detect which mode:**
- "Build me a…" / "Create a…" / "Design a…" → **Create Mode**
- "What's wrong with this?" / "Review this UI" / "Improve this" / "Make this better" / "Audit this design" / "This looks generic" → **Audit Mode**
- "Redesign this" → **Audit Mode first** (diagnose), then **Create Mode** (rebuild with a fresh brief)

---

## Create Mode

### Quick Start (Express Mode)

Short on time? Make these 4 decisions minimum:

1. **Who and how they feel** — One sentence: who is the user and what emotional state are they in when they use this? (e.g., "A busy founder checking metrics between meetings — anxious, time-poor, wants reassurance")
2. **Pick an archetype as departure point** from `references/archetypes.md` — then name ONE thing you'll deliberately do differently from that archetype
3. **Pick a palette** from the Palette Library in the same file
4. **Pick a UX paradigm** from `references/ux.md`

Document:
```
/* Quick DDP: User=busy founder, anxious | Archetype=Linear (but warmer type) | Palette=Amber Night | UX=Command-First + Optimistic UI */
```

Then write code. For the full protocol (recommended for anything production-facing), continue below.

---

## Phase 0: Understand Before You Design

Before touching archetypes or aesthetics, answer three questions about the **human** who will use this.

### Step 0a — The User in Context

Ask:
> *"Who is this person, and what is their emotional state when they open this interface?"*

This is not a persona exercise. It's a single sentence that anchors every decision that follows.

**Examples**:
- "A nurse checking patient vitals during a 12-hour shift — exhausted, needs clarity, zero tolerance for friction"
- "A teenager customizing their profile — excited, playful, wants to express identity"
- "A CFO reviewing quarterly numbers before a board meeting — stressed, skeptical, needs confidence in the data"
- "A first-time user who just downloaded an app from a friend's recommendation — curious but impatient"

The emotional context changes everything. A dashboard for an exhausted nurse and a dashboard for an excited teenager should feel fundamentally different — even if they display similar data.

→ Document: `/* User: [who] — [emotional state] */`

### Step 0b — The Creative Tension

Great design lives in tension. Pick TWO qualities that seem contradictory, then commit to resolving both:

**Example tensions**:
- Dense BUT calm (Bloomberg data density + luxury whitespace)
- Technical BUT warm (monospace precision + serif softness)
- Playful BUT trustworthy (rounded/bouncy + structured layout)
- Minimal BUT expressive (almost nothing on screen + one bold signature)
- Fast BUT considered (snappy interactions + cinematic transitions on key moments)
- Powerful BUT invisible (deep functionality + zero learning curve)

The tension is your creative engine. Without it, you'll default to the obvious — and obvious is generic.

→ Document: `/* Tension: [quality A] BUT [quality B] */`

### Step 0c — Read the Archetypes Library (as departure points)

Open `references/archetypes.md`. **Read at least 5–6 archetypes.** But read them as a designer reads references — not as templates to reproduce.

For each archetype, the library documents tokens (type, palette, spatial, motion). **These are starting points, not specifications.** A human designer looks at Linear and thinks "I love the density but the coldness doesn't fit my users." That transformation — taking what works, discarding what doesn't, adding what's missing — is what makes design human.

Select 1 primary archetype + optionally 1 secondary for contrast. Then ask:
> *"What would I KEEP from this archetype, what would I DISCARD, and what would I ADD that isn't in any archetype?"*

→ Document: `/* Archetype: [name] — Keep: [x], Discard: [y], Add: [z] */`

### Step 0d — Read the UX Reference

Open `references/ux.md`. This is your UX vocabulary — navigation paradigms, interaction models, data entry patterns, feedback systems, onboarding approaches.

Ask:
> *"Given my user's emotional state and context — what interaction model would reduce their friction the most? If I removed all visual styling, would the experience still feel different from every other app in its category?"*

---

## Phase 1: Design Decision Protocol (DDP)

Work through these 9 decisions **in order**. Document your choices in a comment block at the top of your code.

### Decision 1 — Aesthetic Axis

Pick ONE from each column, then combine them:

| Mood | Treatment |
|------|-----------|
| Brutalist | Raw, exposed structure, heavy borders, no decoration |
| Editorial | Magazine-like, strong typographic hierarchy |
| Organic | Irregular shapes, natural textures, flowing |
| Utilitarian | Tool-first, dense, functional, no-frills |
| Luxury | Negative space, restraint, gold/cream accents |
| Playful | Bouncy, rounded, expressive, friendly |
| Industrial | Monospace, structured grids, technical |
| Retro | Era-specific (70s, 80s, 90s, Y2K), nostalgia |
| Neo-classical | Timeless, serif-forward, refined proportions |
| Maximalist | Rich, layered, abundant, visual feast |

**Check**: Does your aesthetic axis serve the user's emotional context from Phase 0? A "Brutalist" axis for an anxious nurse is probably wrong. An "Industrial" axis for a teenager's profile is probably wrong. Let the user pull you toward the right aesthetic, not the other way around.

→ Document: `/* Aesthetic: [axis] — because [why it serves the user] */`

### Decision 2 — Typography Contract

**BANNED fonts** (never use these as default choices):
- Inter, Roboto, Arial, Helvetica Neue, San Francisco (system-ui), DM Sans, Plus Jakarta Sans, Outfit, Nunito, Poppins, Space Grotesk

**Exceptions**: Helvetica Neue is allowed *only* for a committed Swiss International archetype. System fonts are allowed *only* as body fallbacks when the display font carries the full typographic identity.

**Allowed sources**: Google Fonts, Adobe Fonts, system serif stack, monospace stacks

**Required**: Pick a DISPLAY font + a BODY font. They must create contrast (e.g., a heavy slab serif display + light geometric body). Size scale must break from 16px body defaults — try 15px, 17px, 18px. Line heights must be intentional.

**Examples of bold choices**:
- Playfair Display (heavy) + Lora (body) → Neo-classical editorial
- Fragment Mono + IBM Plex Mono → Technical/industrial
- Abril Fatface + Source Serif 4 → Maximalist editorial
- Libre Baskerville + Karla → Approachable but grounded
- Bebas Neue + Karla → Urban/brutal contrast
- Cormorant Garamond + Lora → Luxury/Maison

→ Document: `/* Type: [Display] + [Body] */`

### Decision 3 — Color System

**BANNED palettes**:
- Purple/indigo gradients on white (#7C3AED, #8B5CF6 family)
- Default blues (#3B82F6, #2563EB) as primary
- Generic dark mode (#1F2937 backgrounds)
- "Safe" neutrals with one blue accent
- Gradient on gradient on gradient

**Required**: Build a 5-token system:
```
--color-bg       (base canvas — could be cream, slate, warm black, sand, etc.)
--color-surface  (elevated elements — cards, panels)
--color-primary  (dominant brand/action color)
--color-accent   (sharp contrast, used sparingly)
--color-text     (main text — never pure #000000 or #FFFFFF)
```

**Unexpected color moves**:
- Warm off-whites (#FAF7F2, #F5F0E8) instead of #FFFFFF
- Deep forest greens (#1A2E1A) or burgundy (#2D0A1A) as backgrounds
- Terracotta (#C85A38), sage (#87A878), or gold (#C9A84C) as primaries
- Muted, dusty tones with one electric accent
- Monochromatic palettes with a single unexpected pop

**⚠️ Accessibility check**: Verify that your `--color-text` on `--color-bg` meets WCAG AA contrast ratio (4.5:1 for body text, 3:1 for large text). Muted text tokens must still meet 3:1 minimum. Non-standard palettes are encouraged, but illegible text is not differentiation — it's a bug.

→ Document: `/* Palette: [bg] / [surface] / [primary] / [accent] / [text] — contrast verified */`

### Decision 4 — Spatial Grammar

**BANNED defaults**:
- Everything centered in a column
- Consistent 16px or 24px padding everywhere
- Cards with equal padding on all sides
- Predictable 8px grid applied uniformly

**Required**: Choose a spatial approach:
- **Asymmetric**: Heavy left gutter, light right — or deliberate imbalance
- **Breathing room**: Generous, almost excessive white space in key areas
- **Dense utility**: Compact, information-rich, tabular feel
- **Editorial bleed**: Elements that break the container, full-width moments
- **Layered depth**: Elements overlap, z-index used intentionally
- **Off-grid**: Intentionally break the grid at one key point

→ Document: `/* Spatial: [chosen approach] */`

### Decision 5 — Motion Character

**BANNED defaults**:
- `opacity: 0 → 1` fade-ins on everything
- Uniform 300ms transitions
- scale(0.95) → scale(1.0) as the only "entrance" animation
- Simultaneous animations (everything fades in at once)

**Required**: Motion must have **personality**. Pick a motion character:
- **Snappy**: Fast (150ms), sharp easing, almost instant feedback
- **Elastic**: Spring physics, slight overshoot on entrances
- **Cinematic**: Slower (600-800ms), smooth easing, deliberate pacing
- **Mechanical**: Linear timing, precise, no-nonsense
- **Playful**: Bounce, wobble, or stagger with personality
- **None**: Deliberately static — restraint IS a choice

For web: use `cubic-bezier` over generic `ease`. Use staggered delays for lists.
For iOS/SwiftUI: use `.spring()`, `.interpolatingSpring()`, or custom `Animation` curves.
For Android/Compose: use `spring()` with custom stiffness/damping, or `tween()` with specific easing.

→ Document: `/* Motion: [character] at [timing]ms */`

### Decision 6 — Signature Detail

Every memorable interface has one thing you remember. Pick ONE signature detail that is unexpected for this context:

**Examples**:
- A monospace timestamp in the corner showing live time
- Hover states that reveal something hidden (text, border, color shift)
- A subtle grain/noise texture on the background
- A single decorative line (1px, colored) that runs across the header
- A custom bullet/list marker (→, ●, ▲, etc.) used consistently
- Border radius that is either 0 or very large — never "medium"
- An SVG pattern or subtle geometric background
- Tab/active states that feel physical (like pressing a key)
- A data point displayed in a typographically distinctive way

→ Document: `/* Signature: [description] */`

### Decision 7 — UX Paradigm

This is the interaction layer. Read `references/ux.md` for the full vocabulary. Then define:

**Navigation model** — How does the user move through the product?
Choose from: Command-First / Spatial-Canvas / Progressive Stack / Feed+Panel / Mode-Based / Ambient

**Interaction model** — How do users act on content?
Choose from: Inline Editing / Swipe Vocabulary / Drag-First / Contextual Actions / Progressive Actions / Gesture-Native

**Data entry** — How does the user input information?
Choose from: Conversational Step-by-Step / Progressive Disclosure / Direct Manipulation / AI-Assisted / Bulk Import-First

**Feedback model** — How does the system communicate state?
Choose from: Optimistic UI / Contextual (no global toasts) / Ambient Loading / Undo-over-Confirmation

**Empty & onboarding** — What does a first-time user experience?
Choose from: Progressive (learn by doing) / Template-First / Job-to-be-Done / Zero-Friction / Social Proof

→ Document:
```
/* UX:
 * Navigation:  [chosen model]
 * Interaction: [chosen model]
 * Data entry:  [chosen pattern]
 * Feedback:    [chosen model]
 * Onboarding:  [chosen paradigm]
 */
```

### Decision 8 — Voice & Tone

The words in an interface are design. "Submit" is not the same as "Save changes", which is not the same as "Done", which is not the same as "Let's go." A human-feeling interface has a consistent voice.

**Define the voice along these axes:**

| Axis | Range |
|------|-------|
| Formality | Casual ←→ Formal |
| Warmth | Friendly ←→ Neutral ←→ Clinical |
| Confidence | Assertive ←→ Gentle |
| Brevity | Terse (1-2 words) ←→ Conversational (full sentences) |

**Then apply it to these common UI touchpoints:**
- **Primary CTA**: What does the main button say? (not "Submit")
- **Empty states**: What do you say when there's nothing to show? (not "No items found")
- **Error messages**: How do you communicate failure? (not "An error occurred")
- **Confirmations**: How do you celebrate success? (not "Success!")
- **Loading**: What do you say while waiting? (not just a spinner)

**Examples by voice:**
- **Warm + casual + brief**: "Save" / "Nothing here yet — start one?" / "That didn't work. Try again?" / "Saved ✓" / "Hang tight…"
- **Formal + confident + terse**: "Confirm" / "No records" / "Operation failed. Retry." / "Confirmed" / (no text, progress bar only)
- **Friendly + conversational**: "Save your work" / "You haven't created anything yet — here are some ideas" / "Something went wrong on our end. We're looking into it." / "All saved! You're good." / "Getting things ready…"
- **Playful + warm**: "Ship it!" / "It's quiet in here… 🦗" / "Oops — that broke. Let's fix it." / "Nailed it! 🎯" / "Brewing…"

→ Document: `/* Voice: [formality] + [warmth] + [confidence] + [brevity]. CTA=[x], Empty=[y], Error=[z] */`

### Decision 9 — The Departure

This is the decision that makes the design yours, not a reproduction of an archetype.

Look back at your archetype from Phase 0c. You documented what you'd keep, discard, and add. Now make it concrete:

**Name ONE specific thing in your design that exists in NO archetype in the reference library.**

This could be:
- A layout pattern you invented for this context
- A color combination that doesn't appear in any palette
- An interaction that isn't in the UX reference
- A typographic treatment that isn't in any archetype
- A feedback pattern that doesn't exist in the library

If you can't name one, you're reproducing, not designing. Go back and find the thing that makes this *this* — not a copy of something else.

→ Document: `/* Departure: [what I invented that isn't in any reference] */`

---

## Phase 2: Generate the Design Comment Block

Before your code, write this block:

```
/*
 * UI/UX Design Brief — DesignLint v1.2
 * ──────────────────────────────────────────────
 *
 * — Context —
 * User:        [who — emotional state]
 * Tension:     [quality A] BUT [quality B]
 * Archetype:   [name] — Keep: [x], Discard: [y], Add: [z]
 *
 * — UI —
 * Aesthetic:   [axis — why it serves the user]
 * Type:        [Display / Body]
 * Palette:     [bg / surface / primary / accent / text — contrast verified]
 * Spatial:     [approach]
 * Motion:      [character at timing]
 * Signature:   [description]
 *
 * — UX —
 * Navigation:  [model]
 * Interaction: [model]
 * Data entry:  [pattern]
 * Feedback:    [model]
 * Onboarding:  [paradigm]
 *
 * — Voice —
 * Tone:        [formality + warmth + confidence + brevity]
 * CTA:         [primary button text]
 * Empty:       [empty state text]
 * Error:       [error message text]
 *
 * — Departure —
 * [what I invented that isn't in any reference]
 *
 * — Anti-pattern check —
 * UI: ✗ No Inter/Roboto  ✗ No purple gradient  ✗ No centered column  ✗ No uniform padding
 * UX: ✗ No tab bar       ✗ No modal forms      ✗ No success toasts   ✗ No feature carousel
 * A11y: ✓ AA contrast     ✓ Focus indicators    ✓ Semantic markup
 */
```

This comment is **required**. It keeps you accountable and helps the user audit your choices.

---

## Phase 3: Platform-Specific Execution

Read the relevant reference file for implementation patterns:

- **Design vocabulary & archetypes** → `references/archetypes.md` ← Start here if not done
- **UX paradigms & interaction models** → `references/ux.md` ← Required for Decision 7
- **Web (React/Next.js/HTML)** → `references/web.md`
- **iOS / SwiftUI** → `references/ios.md`
- **Android / Jetpack Compose** → `references/compose.md`
- **React Native** → `references/react-native.md`
- **Dashboards / Data UIs** → `references/dashboards.md`

When using platform reference code: **adapt, don't copy.** The code samples are implementation patterns, not final code. Change the tokens, adjust the proportions, modify the behavior to match YOUR design brief — especially your creative tension and departure.

---

## Phase 4: Anti-Convergence Audit

Before delivering code, run this checklist:

**UI Audit:**
```
[ ] Could this design have been generated without this skill?
    → If yes, it's too generic. Revisit Decision 1.

[ ] Is the font choice immediately identifiable as not-Inter?
    → If not, change it.

[ ] Does the color palette break any "safe" default?
    → If not, push further.

[ ] Is there at least one spatial decision that breaks a grid?
    → If not, add one.

[ ] Is the motion character distinct and named?
    → If not, define it.

[ ] Can you name the Signature Detail?
    → If not, add one.
```

**UX Audit:**
```
[ ] Is there a tab bar with 5 generic icons?
    → If yes: reconsider the navigation paradigm. (references/ux.md §1)

[ ] Is every secondary action a modal?
    → If yes: consider contextual actions, inline editing, or panels.

[ ] Are there global success/error toasts?
    → If yes: replace with optimistic UI + contextual feedback.

[ ] Is the empty state a centered illustration with one CTA?
    → If yes: add template content, multiple smart actions, or personality.

[ ] Is onboarding a feature carousel?
    → If yes: replace with progressive or template-first onboarding.

[ ] Is every data entry a full form + Submit button?
    → If yes: introduce progressive disclosure or direct manipulation.

[ ] If you stripped all visual styling, would the UX still feel distinct?
    → If no: the experience is generic regardless of how it looks.
```

**Accessibility Audit:**
```
[ ] Does every text/bg combination meet WCAG AA (4.5:1 body, 3:1 large)?
    → If not: adjust the muted/accent tokens. Non-standard ≠ inaccessible.

[ ] Are interactive elements keyboard-focusable with visible indicators?
    → If not: add :focus-visible styles that match your aesthetic.

[ ] Is semantic HTML/role used (headings, landmarks, labels)?
    → If not: add it. Differentiation is visual+interactive, not structural.
```

If any answer is "no" — fix it before delivering.

---

## Phase 5: The Human Critique

This is the phase that separates anti-generic design from genuinely human design.

After the code is written and passes the audit, step back and answer these questions honestly:

### The Empathy Check
```
[ ] Would the user from Phase 0 feel understood by this interface?
    → Not "can they use it" but "does it feel like it was made for them?"
    → If not: what emotional signal is missing?

[ ] Does the interface respect the user's state?
    → A stressed user needs calm. An excited user needs energy.
    → Does the visual and interaction design match?
```

### The Craft Check
```
[ ] Is there a moment of delight — something small that would make
    someone say "that's nice" without knowing why?
    → A micro-animation, a well-worded empty state, a thoughtful default.
    → If not: add one. This is what separates tool from craft.

[ ] Does the voice feel like a person wrote it?
    → Read every label, button, and message out loud.
    → If it sounds like a robot or a legal document: rewrite it.

[ ] Is there anything you'd be proud to show a designer?
    → Not "does it pass the audit" but "does it have a point of view?"
    → If not: the Departure (Decision 9) isn't bold enough. Push further.
```

### The Honesty Check
```
[ ] Is the creative tension actually resolved in the design?
    → Or did you just pick two words and ignore one of them?
    → "Dense BUT calm" should feel dense AND calm — not just dense.

[ ] Would you use this app yourself and enjoy it?
    → If the honest answer is "it's fine" — that's not good enough.
    → "Fine" is the enemy. Push until the answer is "yes."
```

If anything fails here — iterate. Change one decision, re-execute, re-critique. The first version is rarely the human version.

---

## Audit Mode

Use this mode when reviewing, critiquing, or improving an existing interface. The input can be a screenshot, a URL, code (React, SwiftUI, Compose, HTML/CSS), or a description of the interface.

### Step A1 — Capture What Exists

Before judging, document what the current design IS. Not what's wrong — just what's there.

```
/*
 * DesignLint Audit — Current State
 * ─────────────────────────────────
 * Source:       [screenshot / code / URL / description]
 * Product:      [what is this interface for?]
 *
 * — Current UI —
 * Typography:   [what fonts, sizes, weights are used?]
 * Colors:       [what palette is in play? bg, text, primary, accents]
 * Layout:       [how is space used? grid, columns, padding patterns]
 * Components:   [cards, buttons, modals — what do they look like?]
 * Motion:       [any animations? what kind?]
 *
 * — Current UX —
 * Navigation:   [how does the user move through the product?]
 * Interactions:  [how does the user act on content?]
 * Data entry:   [how does the user input information?]
 * Feedback:     [how does the system communicate state?]
 * Empty states: [what happens when there's nothing to show?]
 *
 * — Current Voice —
 * CTAs:         [what do buttons say?]
 * Errors:       [how are errors communicated?]
 * Tone:         [formal? casual? generic?]
 */
```

### Step A2 — Convergence Diagnosis

Run the existing design through every checklist. Be specific — don't just flag "generic", explain WHY and WHAT the default is.

**UI Convergence Scan:**
```
[ ] Typography: Is it Inter, Roboto, system-ui, or another banned font?
    → Finding: [specific font detected + what to replace it with]

[ ] Colors: Is the palette purple/blue gradient on white? Default blues?
    Generic dark mode? Safe neutrals?
    → Finding: [specific hex values detected + what's generic about them]

[ ] Layout: Is everything centered in a single column? Uniform padding?
    Equal-sided card padding? Predictable grid?
    → Finding: [specific layout pattern + what's predictable]

[ ] Components: Are cards rounded-xl with subtle shadows? Default shadcn?
    → Finding: [specific component patterns detected]

[ ] Motion: Is it opacity fade-in only? Uniform 300ms? No motion at all?
    → Finding: [specific motion pattern or lack thereof]

[ ] Signature: Is there ANY memorable visual detail?
    → Finding: [what would you remember about this design? probably nothing]
```

**UX Convergence Scan:**
```
[ ] Navigation: Tab bar with 5 icons? Sidebar with icon+label?
    → Finding: [specific nav pattern + why it's default]

[ ] Actions: Everything behind a modal? Tap → Push → Back only?
    → Finding: [specific interaction patterns]

[ ] Data entry: Full forms with Submit buttons?
    → Finding: [specific form patterns]

[ ] Feedback: Global toasts? Green success / red error?
    → Finding: [specific feedback patterns]

[ ] Empty states: Centered illustration + one CTA?
    → Finding: [specific empty state pattern]

[ ] Onboarding: Feature carousel?
    → Finding: [specific onboarding pattern or absence]
```

**Human Convergence Scan:**
```
[ ] Empathy: Is there any evidence the design was shaped by who uses it?
    → Finding: [does the design feel like it was made for a specific person, or for "users"?]

[ ] Voice: Do the words sound human or robotic?
    → Finding: [list the worst offenders — "Submit", "An error occurred", etc.]

[ ] Tension: Is there any creative tension or point of view?
    → Finding: [is the design trying to be anything, or just trying to be "clean"?]

[ ] Memorability: If you stripped the logo, could you identify this product?
    → Finding: [honest answer — probably not]
```

### Step A3 — Convergence Score

Rate the existing design on a 5-point scale:

| Score | Label | Meaning |
|-------|-------|---------|
| 1 | **Generic** | Indistinguishable from any AI-generated default. Inter, purple, tab bar, "Submit". |
| 2 | **Safe** | One or two intentional choices, but the overall feel is still template-like. |
| 3 | **Adequate** | Clear aesthetic direction, but UX or voice is still default. Or vice versa. |
| 4 | **Distinctive** | Strong point of view in both UI and UX. Some generic edges remain. |
| 5 | **Human** | Feels like a specific person designed this for a specific audience. Memorable. |

→ Document: `/* Convergence Score: [1-5] — [label] */`

### Step A4 — Improvement Brief

Based on the diagnosis, produce a targeted improvement plan. Don't rewrite everything — focus on the highest-impact changes.

**Structure the brief as:**

```
/*
 * DesignLint Audit — Improvement Brief
 * ─────────────────────────────────────
 * Current score:  [X/5 — label]
 * Target score:   [Y/5 — label]
 *
 * — Context (inferred or provided) —
 * User:           [who uses this — emotional state]
 * Tension:        [what tension SHOULD this design resolve?]
 *
 * — Top 3 Changes (highest impact) —
 * 1. [specific change + why + what it fixes]
 * 2. [specific change + why + what it fixes]
 * 3. [specific change + why + what it fixes]
 *
 * — UI Fixes —
 * Typography:     [keep / replace with X because Y]
 * Colors:         [keep / replace with X because Y]
 * Layout:         [keep / adjust X because Y]
 * Motion:         [keep / add X because Y]
 * Signature:      [add: specific detail]
 *
 * — UX Fixes —
 * Navigation:     [keep / replace with X because Y]
 * Interactions:   [keep / replace with X because Y]
 * Feedback:       [keep / replace with X because Y]
 * Empty states:   [keep / rewrite because Y]
 *
 * — Voice Fixes —
 * CTAs:           [old → new]
 * Errors:         [old → new]
 * Empty:          [old → new]
 *
 * — The Departure —
 * [one new idea that transforms this from "improved" to "distinctive"]
 */
```

**Rules for the Improvement Brief:**
- **Be specific.** "Change the font" is useless. "Replace Inter with Libre Baskerville for display and Karla for body — it shifts the feel from generic SaaS to approachable authority" is useful.
- **Preserve what works.** Not everything is wrong. Name what's worth keeping and why.
- **Prioritize.** 3 high-impact changes beat 15 minor tweaks. What moves the needle most?
- **Include a Departure.** Even in audit mode, the result should include something original — one idea that elevates the design beyond "fixed" to "distinctive."
- **Respect constraints.** If the design is in production with a component library, don't propose a full rewrite. Propose changes that work within the existing architecture.

### Step A5 — Execute (if asked)

If the user wants the improvements implemented, switch to **Create Mode** but use the Improvement Brief as the design brief instead of starting from scratch. Read the relevant platform reference file and apply the changes.

The Improvement Brief replaces Phase 0 + Phase 1. Continue from Phase 3 (platform execution) → Phase 4 (anti-convergence audit) → Phase 5 (human critique).

---

## Principles

**Design is for humans, not for audits.** The protocol and audits exist to get you to the starting line, not the finish. A design that passes every check but doesn't feel like anything is a failure. A design that fails one check but makes someone smile is closer to the goal.

**Tension is the engine.** Without creative tension, you'll produce the most obvious interpretation of your archetype. The tension between two contradictory qualities is what forces original solutions. Lean into it.

**Archetypes are departure points.** The moment your design is indistinguishable from the archetype, you've reproduced instead of designed. Keep what works, discard what doesn't fit your user, add what's missing. The "Add" is the most important part.

**Voice is design.** An interface with beautiful typography and "An error occurred. Please try again." feels like a robot wearing a nice suit. Every word should sound like the same person who chose the colors and the fonts.

**Commit or don't.** A half-executed concept is worse than a safe one. If you pick Brutalist, go brutalist. If you pick Command-First navigation, remove the tab bar entirely — don't hedge with both.

**Context over rules.** A medical dashboard and a creative portfolio both deserve human design — but different kinds. The user's emotional context from Phase 0 overrides every other decision. When in doubt, go back to who you're designing for and how they feel.

**Iterate.** Human designers don't ship first drafts. If the critique in Phase 5 reveals something flat, change it. The protocol is a loop, not a waterfall.

**Restraint is not safety.** A deliberately minimal design with one extraordinary interaction detail and perfectly chosen words beats a maximalist design that tries too hard. Restraint is a creative choice, not avoidance.
