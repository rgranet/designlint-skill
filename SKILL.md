---
name: designlint
version: 1.1.0
author: Ruben Granet
description: >
  Force distinctive, human-feeling UI/UX design before writing any code. Use this skill
  whenever building or designing any interface — web apps, landing pages, dashboards,
  iOS/SwiftUI screens, Android/Compose screens, or any UI component. Mandatory when the
  user says "build a UI", "create a screen", "design a component", "make it look good",
  "design the UX", or asks for any frontend/interface/experience work. This skill combats
  convergence at both the UI level (Inter+Tailwind+purple-gradient) AND the UX level
  (tab bar + modal + toast). It imposes a structured creative decision phase covering
  visual design AND interaction paradigms before any code is generated.
compatibility: claude-code, cursor, codex, copilot
---

# DesignLint

> **TL;DR** — AI agents converge on the same look and feel. This skill forces 7 explicit design decisions before any code is written. It covers both UI (visual) and UX (interaction) — because a beautiful app with generic interactions is still generic.

---

## The Problem This Skill Solves

AI coding agents converge — at both the UI and UX levels. Left unconstrained, they default to:

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

This skill breaks convergence on both fronts by forcing deliberate decisions **before** any code is written. No exceptions.

---

## Quick Start (Express Mode)

Short on time? Make these 3 decisions minimum. They cover 80% of the differentiation:

1. **Pick an archetype** from `references/archetypes.md` (e.g., "Industrial-Editorial", "Luxury/Maison + Bloomberg dense")
2. **Pick a palette** from the Palette Library in the same file (e.g., "Amber Night", "Terracotta Studio")
3. **Pick a UX paradigm** from `references/ux.md` (e.g., "Command-First nav + Optimistic UI feedback")

Document them in a comment block:
```
/* Quick DDP: Archetype=Industrial-Editorial | Palette=Amber Night | UX=Command-First + Optimistic UI */
```

Then write code. For the full 7-decision protocol (recommended for anything production-facing), continue below.

---

## Phase 0: STOP. Do not write code yet.

Before generating a single line of UI code, complete the **Design Decision Protocol** below. This is mandatory, not optional.

### Step 0a — Read the Archetypes Library

Open `references/archetypes.md`. This is your **primary design vocabulary**. It contains real product archetypes (Linear, Stripe, Vercel, Notion, Apple, Dior...), era archetypes, industry archetypes, art movements, typography-led systems, 8 ready-to-use palettes, and a combination matrix.

**Read at least 5–6 archetypes before choosing.** The root cause of generic AI output is not picking from a wide enough reference set. This library exists to fix that.

### Step 0b — Choose Your Archetype(s)

Based on the brief, select 1 primary archetype + optionally 1 secondary for contrast. Elimination is part of the process: rule out what clearly doesn't fit, then commit to what does.

Then ask:
> *"If a senior designer at the reference brand I just chose were handed this brief — what would they do that I would never do by default?"*

### Step 0c — Read the UX Reference

Open `references/ux.md`. This is your **UX vocabulary**. It contains alternative navigation paradigms, interaction models, data entry patterns, feedback systems, onboarding approaches, and information architecture patterns — all drawn from real products that solved the differentiation problem at the experience level.

Ask:
> *"What is the primary interaction model of this product? If I removed all visual styling, would the experience still feel different from every other app in its category?"*

---

## Phase 1: Design Decision Protocol (DDP)

Work through these 7 decisions **in order**. Document your choices in a comment block at the top of your code.

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

→ Pick your axis. Name it explicitly in your comment. E.g., `/* Aesthetic: Industrial-Editorial */`

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

**⚠️ Accessibility check**: Verify that your `--color-text` on `--color-bg` meets WCAG AA contrast ratio (4.5:1 for body text, 3:1 for large text). Muted text tokens must still meet 3:1 minimum. Use https://webaim.org/resources/contrastchecker/ mentally or verify in code. Non-standard palettes are encouraged, but illegible text is not differentiation — it's a bug.

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

---

## Phase 2: Generate the Design Comment Block

Before your code, write this block:

```
/*
 * UI/UX Design Brief — DesignLint v1.1
 * ──────────────────────────────────────────────
 * Archetype:   [Industrial-Editorial + Bloomberg dense]
 *
 * — UI —
 * Aesthetic:   [Industrial-Editorial]
 * Type:        [Fragment Mono display / Source Serif 4 body]
 * Palette:     [#1C1917 bg / #292524 surface / #D97706 primary / #FCD34D accent / #E7E5E4 text]
 * Contrast:    [text/bg=13.2:1 ✓ | muted/bg=4.8:1 ✓]
 * Spatial:     [Dense utility with editorial bleed on header]
 * Motion:      [Snappy at 150ms, staggered list entries]
 * Signature:   [Thin amber line under active nav item, no transition]
 *
 * — UX —
 * Navigation:  [Command-First — ⌘K palette, minimal visible nav]
 * Interaction: [Inline editing + contextual actions on hover]
 * Data entry:  [Progressive disclosure — title first, details expand]
 * Feedback:    [Optimistic UI + contextual indicators, no global toasts]
 * Onboarding:  [Template-first — start from populated example]
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

---

## Phase 4: Anti-Convergence Audit

Before delivering code, run this mental checklist:

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

## Principles

**UI and UX are inseparable.** A distinctive visual identity on a generic interaction model is decoration on a bad product. A brilliant interaction model with generic visuals is invisible. Both must be differentiated, together.

**Commit or don't.** A half-executed concept is worse than a safe one. If you pick Brutalist, go brutalist. If you pick Command-First navigation, remove the tab bar entirely — don't hedge with both.

**Context shapes everything.** A medical dashboard and a creative portfolio both deserve differentiation — but different kinds. The brief tells you what kind of different is appropriate.

**Accessible by default.** Distinctive palettes and spatial choices must still serve all users. Contrast ratios, focus states, and semantic structure are not optional — they're the floor, not the ceiling.

**The last question is the hardest.** "If you stripped all visual styling, would the UX still feel distinct?" This is the test that matters. An app can have beautiful typography and still navigate, interact, and feel exactly like every other app in its category.

**Restraint is not safety.** A deliberately minimal design with one extraordinary interaction detail beats a maximalist design that tries too hard. Restraint is a creative choice, not avoidance.
