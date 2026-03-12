# DesignLint

**Force distinctive, human-feeling UI/UX design before any AI agent writes code. Audit and improve existing interfaces.**

By [Ruben Granet](https://github.com/rgranet) · v1.2.0 · MIT License

---

## The Problem

AI coding agents converge. Left unconstrained, they always produce the same thing:

**UI:** Inter font · Purple/blue gradients · White background · `rounded-xl` cards · Opacity fade-ins

**UX:** Tab bar (5 icons) · List → Push detail · Modal for everything · Green toast on success · 3-screen onboarding carousel

**Voice:** "Submit" · "An error occurred" · "No items found" · "Success!" · (spinner)

This isn't a style preference — it's a structural failure. Every AI-generated interface looks, feels, and sounds like every other AI-generated interface.

**DesignLint** breaks that convergence with two modes:
- **Create** — Understand the user, make 9 deliberate design decisions, resolve a creative tension, and critique the result before shipping.
- **Audit** — Diagnose an existing interface against the same standards, score it, and produce a concrete improvement plan.

---

## Two Modes

### Create Mode
*"Build me a task management app"*

The agent stops before writing code. It identifies the user and their emotional state, picks a creative tension, selects an archetype as a departure point (not a template), makes 9 design decisions covering aesthetics through voice, and runs a human critique before shipping.

### Audit Mode
*"What's wrong with this UI?" / "Improve this interface" / "Review this design"*

The agent documents what exists, runs the full convergence scan (UI, UX, and human), scores the design 1–5, produces an improvement brief with the top 3 highest-impact changes, and optionally executes the improvements.

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
├── SKILL.md                        # Core protocol (Create + Audit modes)
├── AGENTS.md                       # Drop-in for OpenAI Codex
├── .cursorrules                    # Drop-in for Cursor
└── references/
    ├── archetypes.md               # Design vocabulary library
    ├── ux.md                       # UX paradigm library
    ├── web.md                      # React / Next.js / HTML patterns
    ├── ios.md                      # SwiftUI patterns
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

```bash
cp designlint/.cursorrules ./
cp -r designlint/ ./designlint/
```

### OpenAI Codex

```bash
cp designlint/AGENTS.md ./
cp -r designlint/ ./designlint/
```

### Manual (any agent)

Add the `designlint/` folder to your project and reference `SKILL.md` in whatever instruction mechanism your agent supports.

---

## How It Works

### Create Mode — 5 phases, 9 decisions

**Phase 0** — Understand the human (user context, creative tension, archetype as departure point)

**Phase 1** — 9 decisions:

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

**Phase 2** — Document the design brief (comment block, auditable)

**Phase 3** — Build with platform patterns (adapt, don't copy)

**Phase 4** — Anti-convergence audit (UI + UX + accessibility)

**Phase 5** — Human critique (empathy, craft, honesty — iterate if flat)

### Audit Mode — 5 steps

| Step | What happens |
|------|-------------|
| A1 | Capture what exists (fonts, colors, layout, UX, voice) |
| A2 | Convergence diagnosis (UI + UX + human scans) |
| A3 | Score 1–5 (Generic → Human) |
| A4 | Improvement brief (top 3 changes + UI/UX/voice fixes + Departure) |
| A5 | Execute if asked (brief → Create Mode Phase 3) |

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
| Windsurf | `.windsurfrules` (same as `.cursorrules`) | ✅ |
| Other agents | Manual system prompt | ✅ |

---

## Contributing

Issues and PRs welcome. The most impactful contributions are:

- **New archetypes** in `references/archetypes.md`
- **New UX paradigms** in `references/ux.md`
- **Platform references** (improvements to existing or new platforms)
- **Before/after examples** showing the skill's impact

---

## License

MIT — see [LICENSE](LICENSE)
