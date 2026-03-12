# DesignLint

**Force distinctive, human-feeling UI/UX design before any AI agent writes code.**

By [Ruben Granet](https://github.com/rgranet) · v1.2.0 · MIT License

---

## The Problem

AI coding agents converge. Left unconstrained, they always produce the same thing:

**UI:** Inter font · Purple/blue gradients · White background · `rounded-xl` cards · Opacity fade-ins

**UX:** Tab bar (5 icons) · List → Push detail · Modal for everything · Green toast on success · 3-screen onboarding carousel

**Voice:** "Submit" · "An error occurred" · "No items found" · "Success!" · (spinner)

This isn't a style preference — it's a structural failure. Every AI-generated interface looks, feels, and sounds like every other AI-generated interface.

**DesignLint** breaks that convergence by forcing AI agents to understand the user, make 9 deliberate design decisions, resolve a creative tension, and critique the result — before any code is generated.

---

## Before / After

Without this skill, an AI agent asked to "build a task management app" produces:

```
UI:  Inter · #7C3AED primary · white bg · rounded-xl cards · fade-in
UX:  Tab bar (Home, Tasks, Calendar, Search, Profile) → List → Modal form → Toast
Copy: "Submit" · "No tasks found" · "Task created successfully"
```

With this skill, the same prompt first produces a design brief:

```
User:       Freelance designer juggling clients — overwhelmed, needs calm control
Tension:    Dense BUT calm
Archetype:  Things 3 — Keep: today-first, Discard: system blue, Add: warm editorial type
Palette:    Chalk & Ink (#F5F0E8 bg / #1A1209 text / #C85A38 accent)
Type:       Cormorant Garamond display / Karla body
UX:         Today-First nav · Inline editing · Optimistic UI · Progressive onboarding
Voice:      Warm + brief. CTA="Done" · Empty="A clear day — nice." · Error="Lost that one. Undo?"
Departure:  Priority indicated by type weight (light→bold), not color badges
```

The code that follows is intentional, empathetic, and distinctive.

---

## What's Inside

```
designlint/
├── SKILL.md                        # Core protocol (9 decisions, 5 phases)
├── AGENTS.md                       # Drop-in for OpenAI Codex
├── .cursorrules                    # Drop-in for Cursor
└── references/
    ├── archetypes.md               # Design vocabulary library
    │                               #   → 8 product archetypes (Linear, Apple, Stripe, Vercel…)
    │                               #   → Era archetypes (Y2K, Swiss, Bauhaus, Brutalist…)
    │                               #   → Industry archetypes (Luxury/Maison, Fintech, Agency…)
    │                               #   → 8 ready-to-use color palettes
    │                               #   → Combination matrix
    ├── ux.md                       # UX paradigm library
    │                               #   → 6 navigation paradigms
    │                               #   → 6 interaction models
    │                               #   → 5 data entry patterns
    │                               #   → 6 feedback & state patterns
    │                               #   → 5 onboarding paradigms
    │                               #   → UX × UI pairing matrix
    ├── web.md                      # React / Next.js / HTML implementation patterns
    ├── ios.md                      # SwiftUI implementation patterns
    ├── compose.md                  # Android / Jetpack Compose patterns
    ├── react-native.md             # React Native + Reanimated patterns
    └── dashboards.md               # Data UI & dashboard patterns
```

---
## Quick install
```bash
npx skills add rgranet/designlint-skill
```

## Install

### Claude Code (native)

```bash
claude skill install designlint.skill
```

### Cursor

Copy `.cursorrules` to your project root. It's already configured to reference `SKILL.md` and the reference files.

```bash
cp designlint/.cursorrules ./
cp -r designlint/ ./designlint/
```

Or add to your existing `.cursorrules`:

```
When building any UI or UX, read and follow designlint/SKILL.md before writing code.
Read references from designlint/references/ as directed by SKILL.md.
```

### OpenAI Codex

Copy `AGENTS.md` to your project root:

```bash
cp designlint/AGENTS.md ./
cp -r designlint/ ./designlint/
```

Codex reads `AGENTS.md` automatically — no additional configuration needed.

### Manual (any agent)

Add the `designlint/` folder to your project and reference `SKILL.md` in whatever instruction mechanism your agent supports.

---

## How It Works

The skill enforces **5 phases** and **9 design decisions** before code ships:

### Phase 0 — Understand the human
Define the user's emotional context, pick a creative tension, and select an archetype as a departure point (not a template).

### Phase 1 — 9 decisions

| # | Decision | What it breaks |
|---|----------|----------------|
| 1 | Aesthetic Axis | Generic "Modern SaaS" tone |
| 2 | Typography Contract | Inter, Roboto, system-ui |
| 3 | Color System | Purple gradients, safe blues |
| 4 | Spatial Grammar | Centered column, uniform padding |
| 5 | Motion Character | Uniform 300ms opacity fades |
| 6 | Signature Detail | Forgettable, invisible interfaces |
| 7 | UX Paradigm | Tab bar, modals, global toasts |
| 8 | Voice & Tone | "Submit", "An error occurred", robot-speak |
| 9 | The Departure | Reproducing archetypes instead of designing |

### Phase 2 — Document the design brief
All 9 decisions in a comment block at the top of the code — explicit and auditable.

### Phase 3 — Build with platform patterns
Implementation references for Web, iOS, Android, React Native, and dashboards.

### Phase 4 — Anti-convergence audit
Checklist for UI, UX, and accessibility anti-patterns.

### Phase 5 — Human critique
Empathy check (does the user feel understood?), craft check (is there a moment of delight?), and honesty check (is the creative tension actually resolved?). If anything is flat — iterate.

There's also a **Quick Start** (Express Mode) for speed: 4 decisions, one comment line, then code.

---

## Example Output

```
/*
 * UI/UX Design Brief — DesignLint v1.2
 * ──────────────────────────────────────────────
 *
 * — Context —
 * User:        Freelance designer juggling clients — overwhelmed, needs calm control
 * Tension:     Dense BUT calm
 * Archetype:   Things 3 — Keep: today-first, Discard: system blue, Add: editorial type
 *
 * — UI —
 * Aesthetic:   Neo-classical Utilitarian — calm authority for an overwhelmed user
 * Type:        Cormorant Garamond display / Karla body
 * Palette:     #F5F0E8 bg / #EDE8DE surface / #C85A38 primary / #1A1209 text
 * Spatial:     Breathing room + dense task rows (tension resolved)
 * Motion:      Snappy at 150ms, cinematic 600ms on day transitions
 * Signature:   Priority = type weight (light→bold), no color badges
 *
 * — UX —
 * Navigation:  Today-First — today is home, everything else secondary
 * Interaction: Inline editing, swipe to complete
 * Data entry:  Progressive — title only, details expand on tap
 * Feedback:    Optimistic UI + undo, no toasts
 * Onboarding:  Template-first — pre-populated "Sample Project"
 *
 * — Voice —
 * Tone:        Warm + brief + gentle
 * CTA:         "Done"
 * Empty:       "A clear day — nice."
 * Error:       "Lost that one. Undo?"
 *
 * — Departure —
 * Priority as type weight, not color. No badges, no icons — just
 * font-weight 300→700 to signal urgency. Doesn't exist in any reference.
 *
 * — Anti-pattern check —
 * UI: ✗ No Inter/Roboto  ✗ No purple gradient  ✗ No centered column
 * UX: ✗ No tab bar       ✗ No modal forms      ✗ No success toasts
 * A11y: ✓ AA contrast     ✓ Focus indicators    ✓ Semantic markup
 */
```

---

## Platform Coverage

| Platform | Reference file | Status |
|----------|---------------|--------|
| Web (React/Next.js/HTML) | `references/web.md` | ✅ Full |
| iOS (SwiftUI) | `references/ios.md` | ✅ Full |
| React Native | `references/react-native.md` | ✅ Full |
| Android (Jetpack Compose) | `references/compose.md` | ✅ Core |
| Dashboards / Data UIs | `references/dashboards.md` | ✅ Full |

## Agent Compatibility

| Agent | Install method | Status |
|-------|---------------|--------|
| Claude Code | Native `.skill` install | ✅ |
| Cursor | `.cursorrules` | ✅ |
| OpenAI Codex | `AGENTS.md` | ✅ |
| Windsurf | `.windsurfrules` (same format as `.cursorrules`) | ✅ |
| Other agents | Manual system prompt | ✅ |

---

## Contributing

Issues and PRs welcome. The most impactful contributions are:

- **New archetypes** in `references/archetypes.md` (real products or design movements with documented tokens)
- **New UX paradigms** in `references/ux.md` (real interaction patterns from shipped products)
- **Platform references** (improvements to existing or new platforms)
- **Before/after examples** showing the skill's impact on generated code

---

## License

MIT — see [LICENSE](LICENSE)
