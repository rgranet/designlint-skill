# DesignLint — Design Decision Protocol

> Source: DesignLint v1.2 by Ruben Granet

## Two Modes

**Create Mode** → Build, design, or create an interface. Full 9-decision protocol.
**Audit Mode** → Review, critique, audit, fix, or improve an existing interface.

Read `designlint/SKILL.md` for the full protocol in both modes.

---

## Create Mode

**STOP before writing UI code.** Complete the Design Decision Protocol first.

### Step 1 — Understand the Human

- **User in context**: Who is this person and what is their emotional state? (one sentence)
- **Creative tension**: Pick TWO contradictory qualities to resolve (e.g., "Dense BUT calm")
- **Archetype**: Read `designlint/references/archetypes.md`. Pick one as a departure point — name what you KEEP, DISCARD, and ADD.

### Step 2 — Make 9 Decisions

Read `designlint/references/ux.md` for UX paradigms. Document in a comment block:

1. **Aesthetic Axis** — Mood + treatment. Justify WHY it serves the user.
2. **Typography** — Display + body font (NOT Inter, Roboto, Arial, system-ui, Poppins, Space Grotesk)
3. **Color System** — 5 tokens: bg / surface / primary / accent / text
4. **Spatial Grammar** — Asymmetric / Breathing room / Dense / Editorial bleed / Layered / Off-grid
5. **Motion Character** — Snappy / Elastic / Cinematic / Mechanical / Playful / None
6. **Signature Detail** — One unexpected, memorable element
7. **UX Paradigm** — Navigation, interaction, data entry, feedback, and onboarding models
8. **Voice & Tone** — Formality, warmth, confidence, brevity. Write actual CTA, empty state, and error text.
9. **The Departure** — ONE specific thing that exists in NO archetype in the reference library.

### Step 3 — Build, Audit, Critique

Read the platform reference file:
- Web → `designlint/references/web.md`
- iOS → `designlint/references/ios.md`
- Android → `designlint/references/compose.md`
- React Native → `designlint/references/react-native.md`
- Dashboards → `designlint/references/dashboards.md`

Adapt patterns — don't copy. Run anti-convergence audit. Run human critique (empathy, craft, honesty). Iterate if flat.

---

## Audit Mode

When asked to review, critique, or improve an existing interface:

1. **Capture** — Document current fonts, colors, layout, UX patterns, voice
2. **Diagnose** — Scan against UI, UX, and human convergence checklists from `designlint/SKILL.md`
3. **Score** — Rate 1-5 (1=Generic, 2=Safe, 3=Adequate, 4=Distinctive, 5=Human)
4. **Improvement Brief** — Top 3 highest-impact changes + specific UI/UX/voice fixes + one Departure
5. **Execute** if asked — Use the brief as design brief, continue with Create Mode from Phase 3

---

## Quick Start (Express Mode)

4 decisions minimum:
1. **User + emotional state** (one sentence)
2. **Archetype as departure** + ONE thing you'll do differently
3. **Palette** from `designlint/references/archetypes.md`
4. **UX paradigm** from `designlint/references/ux.md`
