# DesignLint — Design Decision Protocol

> Source: DesignLint v1.2 by Ruben Granet

## When This Applies

Whenever you are asked to build, design, create, or modify any user interface — including web apps, landing pages, dashboards, iOS/SwiftUI screens, Android/Compose screens, React Native apps, or any UI component.

## What To Do

**STOP before writing UI code.** Complete the Design Decision Protocol first.

### Step 1 — Understand the Human

- Read `designlint/SKILL.md` for the full protocol.
- **User in context**: Who is this person and what is their emotional state? (one sentence)
- **Creative tension**: Pick TWO contradictory qualities to resolve (e.g., "Dense BUT calm")
- **Archetype**: Read `designlint/references/archetypes.md`. Pick one as a departure point — name what you KEEP, DISCARD, and ADD.

### Step 2 — Make 9 Decisions

Read `designlint/references/ux.md` for UX paradigms. Then document these in a comment block at the top of your code:

1. **Aesthetic Axis** — Mood + treatment. Justify WHY it serves the user.
2. **Typography** — Display + body font (NOT Inter, Roboto, Arial, system-ui, Poppins, Space Grotesk)
3. **Color System** — 5 tokens: bg / surface / primary / accent / text (NOT purple gradients, NOT default blues)
4. **Spatial Grammar** — Asymmetric / Breathing room / Dense / Editorial bleed / Layered / Off-grid
5. **Motion Character** — Snappy / Elastic / Cinematic / Mechanical / Playful / None
6. **Signature Detail** — One unexpected, memorable element
7. **UX Paradigm** — Navigation, interaction, data entry, feedback, and onboarding models
8. **Voice & Tone** — Formality, warmth, confidence, brevity. Write actual CTA, empty state, and error text.
9. **The Departure** — ONE specific thing in your design that exists in NO archetype in the reference library.

### Step 3 — Write Code

Only after documenting all 9 decisions. Read the platform reference file:
- Web → `designlint/references/web.md`
- iOS → `designlint/references/ios.md`
- Android → `designlint/references/compose.md`
- React Native → `designlint/references/react-native.md`
- Dashboards → `designlint/references/dashboards.md`

Adapt patterns — don't copy them.

### Step 4 — Audit

Verify:
- No Inter/Roboto as primary font
- No purple/blue gradient on white backgrounds
- No tab bar with 5 generic icons as the only navigation
- No modal for every secondary action
- No global toasts for success/error feedback
- No 3-screen onboarding carousel
- No "Submit" / "An error occurred" / "No items found" generic copy
- WCAG AA contrast ratios met (4.5:1 body text, 3:1 large text)

### Step 5 — Human Critique

Before shipping, verify:
- Would the user feel understood by this interface?
- Is there a moment of delight?
- Does the voice sound human?
- Is the creative tension resolved in the design?
- If anything is flat — iterate. Don't ship first drafts.

## Quick Start (Express Mode)

4 decisions minimum:
1. **User + emotional state** (one sentence)
2. **Archetype as departure** + ONE thing you'll do differently
3. **Palette** from `designlint/references/archetypes.md`
4. **UX paradigm** from `designlint/references/ux.md`

Document as: `/* Quick DDP: User=[who, state] | Archetype=[X] (but [Y]) | Palette=[Z] | UX=[W] */`
