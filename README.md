# DesignLint

**Force distinctive, human-feeling UI/UX design before any AI agent writes code.**

By [Ruben Granet](https://github.com/rgranet) · v1.1.0 · MIT License

---

## The Problem

AI coding agents converge. Left unconstrained, they always produce the same thing:

**UI:** Inter font · Purple/blue gradients · White background · `rounded-xl` cards · Opacity fade-ins

**UX:** Tab bar (5 icons) · List → Push detail · Modal for everything · Green toast on success · 3-screen onboarding carousel

This isn't a style preference — it's a structural failure. Every AI-generated interface looks like every other AI-generated interface, regardless of context, brand, or audience.

**designlint** breaks that convergence by imposing a structured **Design Decision Protocol** (7 decisions, 4 phases) covering both visual design and interaction paradigms — before any code is generated.

---

## Before / After

Without this skill, an AI agent asked to "build a task management app" produces:

```
UI:  Inter · #7C3AED primary · white bg · rounded-xl cards · fade-in
UX:  Tab bar (Home, Tasks, Calendar, Search, Profile) → List → Modal form → Toast
```

With this skill, the same prompt first produces a design brief:

```
Archetype:  Things 3 × Luxury/Maison
Palette:    Chalk & Ink (#F5F0E8 bg / #1A1209 text / #C85A38 accent)
Type:       Cormorant Garamond display / Karla body
UX:         Today-First nav · Inline editing · Optimistic UI · Progressive onboarding
Signature:  Vermillion dot (3px) marks today's tasks, no other color in the list
```

The code that follows is intentional, auditable, and distinctive.

---

## What's Inside

```
designlint/
├── SKILL.md                        # Core protocol (7 decisions, 4 phases)
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

The skill enforces a **7-decision protocol** before any code is written:

| # | Decision | What it breaks |
|---|----------|----------------|
| 1 | Aesthetic Axis | Generic "Modern SaaS" tone |
| 2 | Typography Contract | Inter, Roboto, system-ui |
| 3 | Color System | Purple gradients, safe blues |
| 4 | Spatial Grammar | Centered column, uniform padding |
| 5 | Motion Character | Uniform 300ms opacity fades |
| 6 | Signature Detail | Forgettable, invisible interfaces |
| 7 | UX Paradigm | Tab bar, modals, global toasts |

The AI must document all 7 decisions in a comment block at the top of the code — making choices explicit and auditable.

There's also a **Quick Start** (Express Mode) for when you need speed: pick an archetype, a palette, and a UX paradigm. 3 decisions, one comment line, then code.

---

## Example Output

```
/*
 * UI/UX Design Brief — designlint v1.1
 * ──────────────────────────────────────────────
 * Archetype:   Industrial-Editorial + Bloomberg dense
 *
 * — UI —
 * Aesthetic:   Industrial-Editorial
 * Type:        Fragment Mono display / Source Serif 4 body
 * Palette:     #1C1917 bg / #292524 surface / #D97706 primary / #FCD34D accent / #E7E5E4 text
 * Contrast:    text/bg=13.2:1 ✓ | muted/bg=4.8:1 ✓
 * Spatial:     Dense utility with editorial bleed on header
 * Motion:      Snappy at 150ms, staggered list entries
 * Signature:   Thin amber line under active nav item, no transition
 *
 * — UX —
 * Navigation:  Command-First — ⌘K palette, minimal visible nav
 * Interaction: Inline editing + contextual actions on hover
 * Data entry:  Progressive disclosure — title first, details expand
 * Feedback:    Optimistic UI + contextual indicators, no global toasts
 * Onboarding:  Template-first — start from populated example
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
