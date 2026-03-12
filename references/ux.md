# UX Differentiation Reference

The same convergence problem that plagues UI affects UX. AI defaults to:
- Tab bar + list + detail navigation (always)
- Modal for every secondary action
- Form → Submit → Success toast (always)
- Empty state with centered illustration + CTA
- Infinite scroll or pagination (never anything else)
- Sidebar navigation for dashboards (always)
- Search bar at the top (always)
- Onboarding carousel with 3 screens (always)

This file documents alternative UX paradigms, interaction models, and flows
drawn from products that solved differentiation at the experience level.

---

## Table of Contents

1. [Navigation Paradigms](#1-navigation-paradigms)
2. [Interaction Models](#2-interaction-models)
3. [Data Entry Patterns](#3-data-entry-patterns)
4. [Feedback & State Patterns](#4-feedback--state-patterns)
5. [Onboarding Paradigms](#5-onboarding-paradigms)
6. [Information Architecture Patterns](#6-information-architecture-patterns)
7. [UX Archetypes by Product Type](#7-ux-archetypes-by-product-type)
8. [UX × UI Archetype Pairing Matrix](#8-ux--ui-archetype-pairing-matrix)

---

## 1. Navigation Paradigms

### BANNED: The Default Stack
- Tab bar (5 icons, labels below) → List → Push detail
- Sidebar (icon + label) → Content area → Modal for actions
- Top nav → Dropdown menus → Pages

These are not wrong — they're invisible. When everyone uses them, they stop communicating anything.

---

### Paradigm A — Command-First (Linear, Raycast, Superhuman)
**Concept**: Primary navigation is a command palette, not a visible structure.
**How it works**:
- `⌘K` opens a fuzzy-search command palette for everything
- The visible UI is minimal — just current context
- Navigation happens through intent, not through browsing structure
- Recent actions surface as shortcuts

**When to use**: Power users, productivity tools, developer tools, anything where the user knows what they want
**iOS equivalent**: Spotlight-like search bar as primary entry point, not supplementary
**Implementation signal**: Invest in search/command quality, not navigation chrome

```
UX Pattern: Command-First
Primary: ⌘K palette / search
Secondary: Recent / pinned items
Tertiary: Browse structure (de-emphasized)
```

---

### Paradigm B — Spatial / Canvas (Figma, Miro, Linear Roadmap)
**Concept**: Content lives on a 2D canvas. Navigation is panning and zooming.
**How it works**:
- No traditional nav — you move through space
- Zoom out = overview, zoom in = detail
- Related items are spatially proximate
- History = "where you've been on the canvas"

**When to use**: Planning tools, design tools, relationship mapping, timeline views
**iOS equivalent**: Zoomable scrollview with semantic levels (overview → detail on tap/pinch)

---

### Paradigm C — Progressive Disclosure Stack (Craft, Things 3)
**Concept**: One level visible at a time, but hierarchy is gestural not tab-based.
**How it works**:
- Swipe right = go deeper into context
- Swipe left = go back up
- No persistent navigation — context IS navigation
- Breadcrumb replaces back button

**When to use**: Deep hierarchical content (notes, tasks, documents)
**Signature**: The current level fills the screen. Nothing else competes.

---

### Paradigm D — Feed + Context Panel (Slack, Linear, Notion)
**Concept**: Primary = chronological or prioritized feed. Secondary = contextual panel that slides in without replacing.
**How it works**:
- Left: feed or list (primary content stream)
- Right: detail panel appears alongside, doesn't push
- No full-screen modal for detail views
- Context never fully disappears

**When to use**: Communication tools, issue trackers, CRMs, anything with a list + detail pattern
**Key distinction**: Panel slides IN, doesn't REPLACE. You always see the list.

---

### Paradigm E — Mode-Based (Camera app, Sketch, Final Cut)
**Concept**: The app has distinct modes. Switching modes changes the entire UI paradigm.
**How it works**:
- Each mode has its own toolbar, affordances, shortcuts
- Mode switching is explicit (not buried in settings)
- Current mode is always visible in the UI
- No mode confusion — the UI changes dramatically

**When to use**: Creative tools, multi-workflow apps, anything where the user's intent changes fundamentally between tasks

---

### Paradigm F — Ambient / Glanceable (Apple Watch, widgets, status apps)
**Concept**: The primary interaction is passive. You glance, not navigate.
**How it works**:
- Information is always visible, always current
- Actions are minimal (one or two max)
- No navigation — everything fits in one view
- Complications and contextual data replace navigation

**When to use**: Health trackers, habit apps, dashboards, monitoring tools, companion apps

---

## 2. Interaction Models

### BANNED: The Default Interactions
- Tap → Push → Back (always)
- Long press → Action sheet (always)
- Swipe left → Delete (always, and only delete)
- Pull to refresh (always, even when real-time)
- Tap → Modal → Form → Save → Dismiss (always)

---

### Model A — Inline Editing (Notion, Linear, Craft)
**Concept**: Content IS the editor. No separate "edit mode."
**Signature**: Tap any text to edit it. No edit button, no form, no modal.
**UX principle**: Reduce the distance between reading and writing to zero.
**Implementation**:
- `contenteditable` on web / `TextEditor` on SwiftUI
- Auto-save, never explicit Save button
- Changes persist optimistically (update UI immediately, sync in background)
- Undo is ⌘Z / shake, not a cancel button

---

### Model B — Swipe Vocabulary (Tweetbot, Reeder, Spark)
**Concept**: Swipe gestures have a full vocabulary beyond just "delete."
**Swipe actions map to user's most common actions:**
```
Swipe right (short): Primary positive action (Archive, Mark done, Like)
Swipe right (full):  Secondary positive action (Mark unread, Snooze)
Swipe left (short):  Primary negative action (Delete, Dismiss)
Swipe left (full):   Destructive action (with confirmation haptic)
```
**Key**: The vocabulary is consistent throughout the entire app. One gesture = one meaning, everywhere.

---

### Model C — Drag & Drop as Primary (Things 3, Trello, Keewordz)
**Concept**: Drag is not a power-user feature — it's the primary organizational interaction.
**Design implications**:
- All draggable items have visible drag handles (or discoverable ones)
- Drop targets highlight on hover/drag-over
- Snap behavior is precise and satisfying
- Undo is instant (⌘Z or shake)
- Mobile: long-press to lift, drag to position

---

### Model D — Contextual Actions (macOS right-click, iOS context menu)
**Concept**: Actions appear where the content is, not in a toolbar.
**Implementation**:
- 3D Touch / long press reveals context menu with relevant actions
- Actions are context-specific (not a generic list)
- Destructive actions always at the bottom, red
- Preview in context menu where possible (Peek & Pop paradigm)

**iOS SwiftUI:**
```swift
.contextMenu {
    Button { archive(item) } label: {
        Label("Archive", systemImage: "archivebox")
    }
    Button(role: .destructive) { delete(item) } label: {
        Label("Delete", systemImage: "trash")
    }
}
```

---

### Model E — Progressive Actions (Lasso, Craft)
**Concept**: Actions reveal themselves based on what the user selects or does.
**How it works**:
- Default state: minimal chrome, no action buttons
- On selection: relevant actions float up (toolbar appears)
- On multi-selection: actions adapt to the selection
- Nothing visible that isn't currently relevant

**Opposite of**: Giant toolbars with 20 icons visible at all times.

---

### Model F — Gesture-Native (Reeder 5, Apollo, Clear)
**Concept**: The entire app is controlled through gestures. Buttons are fallbacks.
**Gesture vocabulary example (Clear, the task app):**
```
Pull down from top: Create new item
Swipe right on item: Complete
Swipe left on item: Delete  
Pinch in on list: Go up a level
Pinch out on item: Expand / go deeper
Pull down on list: Reveal hidden items
```
**UX principle**: Every action has a physical metaphor. The app feels like a physical object.

---

## 3. Data Entry Patterns

### BANNED: The Generic Form
```
[Label]
[Text Input]
[Label]  
[Text Input]
[Dropdown]
[Submit Button]
```
This is appropriate for tax forms. Not for modern products.

---

### Pattern A — Conversational / Step-by-Step (Typeform, Stripe Onboarding)
**Concept**: One question at a time. The UI adapts to the answer.
**How it works**:
- One field visible at a time, full screen
- Pressing Enter / Continue reveals the next
- Progress is shown, but not as a long progress bar
- The tone is conversational ("What should we call you?" not "First Name:")
- Smart defaults pre-fill what you can infer

---

### Pattern B — Inline Progressive Form (Linear issue creation)
**Concept**: Start with the minimum, reveal more as needed.
**How it works**:
- First interaction: just a text field ("What needs to be done?")
- After title entered: secondary fields appear (assignee, priority, label)
- Advanced options: collapsed behind "More options"
- Never show the full form upfront

---

### Pattern C — Direct Manipulation (Color pickers, date selectors, sliders)
**Concept**: Input through manipulation, not through typing.
**Examples**:
- Drag a timeline bar instead of typing start/end dates
- Tap a color swatch instead of entering hex
- Slide a confidence level instead of selecting from a dropdown
- Draw a signature instead of typing a name
**Key**: The manipulation IS the input. No intermediate representation.

---

### Pattern D — AI-Assisted Entry (Notion AI, Linear, GitHub Copilot)
**Concept**: The AI fills in most fields; the user corrects.
**How it works**:
- User provides a rough input (natural language, a paste, a drag)
- System proposes structured data
- User reviews and corrects, doesn't create from scratch
- Acceptance is one tap/click

---

### Pattern E — Bulk / Import-First (Airtable, Notion database)
**Concept**: Start from existing data, not from a blank form.
**How it works**:
- Drag & drop a spreadsheet / CSV to create a database
- Paste a list of items to create tasks
- Import from connected tools as default, manual entry as fallback
**Key UX insight**: Users never have truly empty states. They have data elsewhere.

---

## 4. Feedback & State Patterns

### BANNED: The Generic Feedback Pattern
- Success toast at bottom of screen (green, checkmark, 3 seconds)
- Error toast (red, X, 3 seconds)  
- Loading spinner (centered, always)
- Empty state (centered illustration, one CTA)
- Skeleton loaders that look identical everywhere

---

### Pattern A — Optimistic UI (Linear, Twitter/X likes)
**Concept**: Update the UI immediately. Sync in the background. Roll back on failure.
**User experience**: Actions feel instant. No waiting.
**Implementation**:
- Update local state before API call
- Show subtle "syncing" indicator (not a blocking spinner)
- On error: roll back + show contextual error at the affected element
- Never block the user during a network operation

**Signal to use**: Any action that changes data the user just interacted with.

---

### Pattern B — Contextual Feedback (Stripe, Linear)
**Concept**: Feedback appears where the action happened, not in a global toast.
**Examples**:
- After saving a field: a subtle checkmark appears next to that field, not a global toast
- After sending a message: the message itself shows a sent indicator
- After completing a task: the task strikes through and fades out
- Error on a specific field: the error appears below that field, not at the top

**Principle**: Feedback is spatially proximate to its cause.

---

### Pattern C — Ambient Loading (Stripe Dashboard, Linear)
**Concept**: Loading states are ambient and non-blocking.
**How it works**:
- Skeleton loaders match the exact layout of loaded content (not generic rectangles)
- A thin progress bar at the top of the screen (like YouTube/GitHub) replaces spinners
- Already-loaded content is usable while other content loads
- Never a full-screen spinner that blocks everything

**iOS:**
```swift
// Skeleton that matches content layout
if isLoading {
    SkeletonView()  // Custom, matches real layout
        .redacted(reason: .placeholder)
        .shimmering()  // Custom shimmer animation
} else {
    RealContent()
}
```

---

### Pattern D — Undo Over Confirmation (Gmail, Slack, Things 3)
**Concept**: Never ask "Are you sure?" — let the user undo instead.
**How it works**:
- Destructive action executes immediately
- A brief undo window appears (3-5 seconds)
- After the window: action is permanent
- Undo is always accessible in history

**Why it's better**: Confirmation dialogs interrupt flow. Undo doesn't.
**Exception**: Truly irreversible actions (deleting account, sending money) still warrant confirmation.

---

### Pattern E — Error Prevention Over Error Messages (Apple HIG)
**Concept**: Design to make errors impossible, not to explain them after they happen.
**Techniques**:
- Disable buttons that would cause an error, don't wait for the submit to fail
- Format inputs as the user types (phone numbers, dates, credit cards)
- Validate inline, not on submit
- Constrain inputs to valid values (date picker vs date text field)
- Show character counts before limits, not after exceeding them

---

### Pattern F — Empty States as Onboarding (Notion, Linear, Slack)
**Concept**: The empty state is the first experience. It should teach AND delight.
**Bad empty state**: Centered illustration, "No items yet", "+ Add item" button
**Good empty state**:
- Shows example content (grayed out or templated) so the user understands the context
- Provides 2-3 smart starter actions (not just one generic CTA)
- Has personality — a moment of brand expression
- Disappears gracefully as real content fills in

---

## 5. Onboarding Paradigms

### BANNED: The Carousel Onboarding
3 screens with illustrations explaining features. Users skip it. Always. It teaches nothing.

---

### Paradigm A — Progressive Onboarding (Slack, Duolingo)
**Concept**: Teach through doing, not through explaining.
**How it works**:
- User starts using the product immediately
- Tooltips appear contextually when a feature becomes relevant
- No upfront education
- "First run" experiences are indistinguishable from "nth run"

---

### Paradigm B — Template-First (Notion, Airtable, Linear)
**Concept**: Start from a populated template, not a blank state.
**How it works**:
- After signup: "Pick a template" as the first screen
- Templates are real, useful examples
- User immediately sees value (populated UI > empty UI)
- Customization happens after value is demonstrated

---

### Paradigm C — Job-to-Be-Done Onboarding (Intercom, Typeform)
**Concept**: Ask the user what they're trying to accomplish, then tailor everything.
**How it works**:
- 2-3 questions about role, use case, team size
- The product configures itself based on answers
- Feels like a concierge, not a form
- Each question has immediate visual feedback

---

### Paradigm D — Zero-Friction Immediate Value (Figma, Canva, Excalidraw)
**Concept**: No onboarding. You're in the product immediately.
**How it works**:
- No signup required to try
- No tutorial before use
- Help is available but never pushed
- The product is self-evident

**When to use**: Products with a clear, demonstrable value that's immediately visible.

---

### Paradigm E — Social Proof Onboarding (Superhuman, Linear waitlist era)
**Concept**: Exclusivity and peer validation as the first experience.
**How it works**:
- Waitlist → invite-only creates desire before the product is seen
- First login features content from real users (not examples)
- Activity from teammates is immediately visible

---

## 6. Information Architecture Patterns

### BANNED: The Default IA
- Dashboard → Section → List → Detail
- Everything reachable from the sidebar in 2 clicks
- Settings as a separate top-level destination
- Notifications as a separate tab

---

### Pattern A — Inbox Zero Model (Superhuman, HEY email)
**Concept**: Primary interaction is processing a queue, not browsing a collection.
**IA structure**:
- Inbox (primary): items awaiting action
- Done/Archive: processed items (searchable, not browsable)
- Compose/Create: always accessible
- Settings: minimal, rarely needed

**Principle**: The IA reflects a workflow, not a data structure.

---

### Pattern B — Today-First (Things 3, Fantastical, Streaks)
**Concept**: The home screen is always "now." History and future are secondary.
**IA structure**:
- Today (home): what matters right now
- Upcoming: what's coming
- Logbook/Archive: what's done
- Projects/Areas: organizational structure (accessed occasionally)

---

### Pattern C — Everything Search (Raycast, Spotlight, Notion)
**Concept**: Search is the primary navigation. IA is flat — everything is one search away.
**IA structure**:
- Search (home / ⌘K)
- Recent (surfaces automatically)
- Favorites/Pinned (manual, minimal)
- Browse (fallback, not primary)

---

### Pattern D — Stream + Context (Twitter/X, Slack, iMessage)
**Concept**: Chronological stream is primary. Everything else is context.
**IA structure**:
- Stream (primary): chronological, real-time
- Threads/Channels: context containers within the stream
- Profile/Settings: secondary destinations

---

## 7. UX Archetypes by Product Type

### Landing Page / Marketing
**Default (bad)**: Hero → Features (3 columns) → Social proof → CTA → Footer
**Differentiated options**:
- **Narrative scroll**: One continuous story, no sections. Scroll = story progress.
- **Interactive demo first**: Product is live in the hero. Copy explains what you're seeing.
- **Problem-first**: Lead with the pain, not the solution. Solution revealed through scroll.
- **Bold statement + proof**: One enormous claim, immediately followed by evidence.
- **Comparison table hero**: Lead with the competitor comparison. Confidence as UX.

---

### Dashboard / Internal Tool
**Default (bad)**: Sidebar nav + KPI cards (4-col grid) + charts + table
**Differentiated options**:
- **Ops room**: Full-screen, ambient. No navigation — you monitor, not navigate.
- **Inbox model**: Alerts/anomalies as a queue. Normal = nothing to see.
- **Story dashboard**: Data tells a story from top to bottom. Not widgets, but narrative.
- **Command center**: Search + ⌘K primary. Widgets are saved queries, not static layout.

---

### iOS App
**Default (bad)**: Tab bar (5 tabs) + NavigationStack + List + Detail
**Differentiated options**:
- **Single-screen depth**: One screen, but with deep contextual panels (Things 3)
- **Gesture-native**: Full gesture vocabulary, no tab bar (Clear, Reeder)
- **Widget-first**: Home screen widget IS the primary interface. App = settings + history.
- **Camera-first**: The camera/capture is the primary UI. Everything else is management.
- **Today widget**: Glanceable primary. App = detail + settings.

---

### Web App (SaaS)
**Default (bad)**: Top nav + sidebar + main content area + modal for everything
**Differentiated options**:
- **Workspace model**: Canvas-based, spatial, zoom levels (Figma, Miro)
- **Feed model**: Chronological primary, context panel secondary (Linear, Notion)
- **Command-first**: ⌘K primary. Visible UI is minimal context (Raycast for the web)
- **Document model**: The document IS the interface. Nav is minimal chrome (Notion, Craft)

---

## 8. UX × UI Archetype Pairing Matrix

| UX Paradigm | UI Archetype | Product Feeling | Example |
|-------------|-------------|-----------------|---------|
| Command-First | The Linear (UI) | Speed, power, control | Raycast, Linear |
| Gesture-Native | Apple | Physical, fluid, native | Clear, Reeder |
| Narrative Scroll | Editorial | Cinematic, engaging | Great landing pages |
| Template-First | Notion (UI) | Warm, approachable | Notion, Craft |
| Ops Room | Bloomberg dense | Authority, precision | Trading tools |
| Inline Editing | Vercel minimal | Invisible UI, content-first | Notion, Linear |
| Optimistic UI | Swiss/Structured | Trustworthy, fast | Stripe, Linear |
| Today-First | Luxury/Maison | Calm, focused | Things 3 |
| Swipe Vocabulary | Apple | Intuitive, gestural | Tweetbot, Spark |
| Progressive Form | Conversational | Human, guided | Typeform, Stripe |

---

## How to Apply UX Differentiation

### In the Design Decision Protocol, add a 7th decision:

**Decision 7 — UX Paradigm**

Ask:
> *"What is the primary interaction model of this product? How does the user navigate, enter data, receive feedback, and recover from errors?"*

Then document in your comment block:
```
/* UX Paradigm:
 * Navigation:   Command-First (⌘K palette, minimal visible nav)
 * Interaction:  Inline editing, swipe vocabulary
 * Data entry:   Progressive disclosure form
 * Feedback:     Optimistic UI + contextual (no global toasts)
 * Empty states: Template-first with personality
 * Onboarding:   Progressive (learn by doing)
 */
```

### The UX Anti-Convergence Check

Before delivering, verify:
```
[ ] Navigation: Is there a tab bar with 5 generic icons?
    → If yes: reconsider the navigation paradigm.

[ ] Data entry: Is there a full form with a Submit button?
    → If yes: consider progressive disclosure or inline editing.

[ ] Feedback: Are there global success/error toasts?
    → If yes: replace with contextual, optimistic feedback.

[ ] Empty states: Is there a centered illustration with one CTA?
    → If yes: add template content, personality, or multiple smart actions.

[ ] Onboarding: Is there a feature carousel?
    → If yes: replace with progressive or template-first onboarding.

[ ] Interactions: Is every action a tap → modal → form → save?
    → If yes: introduce at least one gesture or direct manipulation.
```
