# Design Archetypes Library

This is the core reference library that addresses the root cause of AI convergence:
**lack of varied design references**. Each archetype is a named, documented visual
direction drawn from real products, design movements, and cultural aesthetics.

When executing the Design Decision Protocol, pick an archetype (or combine two)
and implement it faithfully. Do not dilute. Do not hedge.

---

## Table of Contents

1. [Product Archetypes](#1-product-archetypes) — Real products as reference
2. [Era Archetypes](#2-era-archetypes) — Decade-specific aesthetics
3. [Industry Archetypes](#3-industry-archetypes) — Sector-specific visual languages
4. [Art Movement Archetypes](#4-art-movement-archetypes) — Fine art translated to UI
5. [Typography-Led Archetypes](#5-typography-led-archetypes) — Type as primary design element
6. [Palette Library](#6-palette-library) — Ready-to-use non-generic color systems
7. [Combination Matrix](#7-combination-matrix) — Unexpected archetype pairings

---

## 1. Product Archetypes

Real products that have solved the differentiation problem. Study and adapt — never copy.

### The Linear
**Reference**: Linear.app
**Character**: Extreme speed, keyboard-first, dark by default, monospace data
**Signature moves**:
- Near-black backgrounds (#0F0F0F range), not dark gray
- Very high contrast text (close to white, never gray)
- Keyboard shortcuts displayed inline
- Dense information, no wasted space
- Subtle but precise border treatment (1px, low opacity)
- Commands > clicks

**Type**: Geist Mono / Geist Sans or equivalents
**Palette**: #0F0F0F / #1A1A1A / #7C7C7C / #FFFFFF / one accent (blue or purple — but precise, not generic)
**Spatial**: Dense, tabular, consistent 8px rhythm but tight
**Motion**: Instant. Near-zero transitions. Speed IS the UX.

---

### The Stripe
**Reference**: Stripe.com (marketing) / Stripe Dashboard
**Character**: Financial trust, editorial confidence, gradients used structurally
**Signature moves**:
- Gradient backgrounds that feel *built*, not slapped on
- Strong serif in marketing headers
- Precise grid, generous padding
- Subtle drop shadows with color tint (not gray)
- Illustrated diagrams as UI elements
- Blue used precisely and sparingly

**Type**: Sohne (substitute: DM Serif Display + DM Sans)
**Palette**: #0A2540 (dark navy) / #425466 / #7A5AF8 (accent) / #FFFFFF / #F6F9FC (off-white)
**Spatial**: Structured, generous, 120px sections
**Motion**: Smooth, 400ms, easeOut. Scroll-triggered reveals.

---

### The Vercel
**Reference**: Vercel.com
**Character**: Radical minimalism, monochrome-first, type as decoration
**Signature moves**:
- Pure black / pure white — minimal mid-tones
- Typography scale with extreme size contrast (tiny labels, huge display)
- Borders as structure (1px white/10% opacity)
- Grid lines visible as decoration
- Code snippets as design elements
- Almost no color — one electric accent max

**Type**: Geist (or: monospace + geometric sans)
**Palette**: #000000 / #111111 / #888888 / #FFFFFF / one accent (#00FF00 or #FF4D4D or similar electric)
**Spatial**: Vast negative space, full-width sections, deliberate emptiness
**Motion**: None, or very precise. Deliberate restraint.

---

### The Notion
**Reference**: Notion.so
**Character**: Document-first, warm neutrals, human-scale
**Signature moves**:
- Cream/parchment backgrounds (not white)
- Emoji/icon as visual anchor
- Serif for content areas
- Block-based, modular
- Very low contrast UI chrome (so content dominates)
- Hover states that feel physical (background appears)

**Type**: Custom (substitute: Source Serif 4 + Inter — but use sparingly)
**Palette**: #FFFDF7 / #F1EFE9 / #191919 / #E9E9E7 / one muted accent
**Spatial**: Document-like, left-aligned, content-width (680px max)
**Motion**: Gentle, 200ms ease. Hover reveals.

---

### The Loom
**Reference**: Loom.com (2021-2023 era)
**Character**: Warm, expressive, human — the anti-SaaS
**Signature moves**:
- Gradient orbs / blobs as background elements
- Warm purples, pinks, amber — but soft, dusty
- Rounded everything (but intentional, not generic)
- Personality in microcopy
- Faces/avatars as UI elements
- Playful but professional

**Type**: Aeonik (substitute: Cabinet Grotesk + Fraunces for display)
**Palette**: #1A0533 (deep purple) / #5B21B6 / #EC4899 / #FCD34D / #FFFFFF
**Spatial**: Generous, centered, breathing room
**Motion**: Bouncy, spring-based, 350ms

---

### The Figma
**Reference**: Figma.com (marketing)
**Character**: Creative tool energy, bold color blocks, geometric
**Signature moves**:
- Solid color sections (not gradient)
- Component grid as visual motif
- Bold geometric shapes as decoration
- Developer + designer tension as aesthetic
- Color as wayfinding

**Type**: Figma's custom (substitute: Space Mono for tech sections + Libre Franklin for body)
**Palette**: Rotating section colors — each section has its own palette
**Spatial**: Full-bleed sections, tight gutters inside, max contrast between sections
**Motion**: Playful, interactive, scroll-driven

---

### The Arc Browser
**Reference**: Arc browser / The Browser Company
**Character**: Personal software, opinionated, emotional
**Signature moves**:
- Gradient orbs that feel alive
- Ultra-rounded UI (24px+ radius)
- Vibrant but harmonious palettes
- Personality-first copy
- Sidebar as primary navigation paradigm
- Blur/glass effects used meaningfully

**Type**: Custom display + system (substitute: Fraunces + system-ui here is OK)
**Palette**: User-defined — but always vibrant, never muted
**Spatial**: Compact sidebar, generous content area
**Motion**: Fluid, spring-based, gesture-driven feel

---

### The Apple
**Reference**: Apple.com, macOS, iOS Human Interface Guidelines
**Character**: Clarity through reduction. Every pixel earns its place. Hardware and software as one.
**Signature moves**:
- SF Pro / SF Compact as the system — but replace with equivalents outside Apple ecosystem
- Frosted glass (`.regularMaterial`, `backdrop-filter: blur`) used structurally, not decoratively
- Depth as hierarchy: layers blur behind layers
- Photography and product renders as primary visual content — UI chrome disappears
- Gradients so subtle you're not sure they're there
- Rounded rectangles at mathematically precise radii (Squircle, not circle)
- Dark mode and light mode as equal citizens — never an afterthought
- SF Symbols / system icons for perfect optical weight matching
- Transitions that feel like physics: spring-based, gesture-driven, interruptible
- "Breathing room" in product pages — vast whitespace, one thing at a time

**Type**: SF Pro (system) outside Apple: use **Mona Sans**, **Geist**, or **Satoshi** — BUT at Apple-like scale: tiny labels at 11px/tracking +0.1em, large display at 56-80px/tracking -0.03em. The type scale is extreme, never medium. (Note: Inter is banned by this skill's typography contract — use the substitutes above.)
**Palette**:
```
Light:  #FFFFFF / #F5F5F7 / #1D1D1F / #0066CC (Apple blue) / #86868B (muted)
Dark:   #000000 / #1C1C1E / #FFFFFF / #0A84FF (adapted blue) / #636366
Glass:  rgba(255,255,255,0.72) with backdrop-filter: blur(20px) saturate(180%)
```
**Spatial**: Asymmetric vertically (sections breathe differently), symmetric horizontally. Max-width 980px on marketing, but full-bleed for immersive sections. 40px minimum horizontal margin on mobile.
**Motion**: Spring physics, always. `response: 0.35, damping: 0.75` as baseline. Parallax on scroll. Hero elements scale subtly on scroll (scale 1.0 → 0.95). Page transitions: push/pop, never fade.

**What Apple NEVER does**:
- Drop shadows with gray (always colored or none)
- Borders on cards (depth via blur/transparency instead)
- Purple gradients
- Generic rounded corners (squircle or nothing)
- Center-aligning body text
- Using bold weight for body copy

**Web implementation of glass:**
```css
.glass-panel {
  background: rgba(255, 255, 255, 0.72);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 0.5px solid rgba(255, 255, 255, 0.3);
  /* No box-shadow — depth comes from blur, not shadow */
}

/* Dark mode glass */
.glass-panel-dark {
  background: rgba(28, 28, 30, 0.72);
  backdrop-filter: blur(20px) saturate(180%);
  border: 0.5px solid rgba(255, 255, 255, 0.08);
}
```

**SwiftUI implementation:**
```swift
// Correct Apple-style materials
.background(.regularMaterial)           // frosted glass
.background(.ultraThinMaterial)        // more transparent
.background(.thickMaterial)            // more opaque

// Squircle — Apple's actual corner radius formula
// Use .continuous curve, not .circular
RoundedRectangle(cornerRadius: 20, style: .continuous)
  .fill(.regularMaterial)

// Spring that feels like Apple
.animation(.spring(response: 0.35, dampingFraction: 0.75), value: state)

// SF Pro size scale — commit to extremes
Text("Title").font(.system(size: 56, weight: .bold, design: .default))
  .tracking(-1.5)  // tight at large sizes
Text("LABEL").font(.system(size: 11, weight: .medium))
  .tracking(0.8)   // wide at small sizes
  .textCase(.uppercase)
```

---

## 2. Era Archetypes

### Y2K (1998–2003)
**Visual language**: Chrome, gradients, beveled edges, star bursts, pixel fonts
**Key elements**:
- Metallic gradients (silver to chrome)
- Beveled/embossed UI elements
- Tight sans-serif, often condensed
- Blinking, animated GIF sensibility (use sparingly)
- Translucency (early glass effects)

**Type**: Bebas Neue or Tungsten for display / VCR OSD Mono for accent
**Palette**: #C0C0C0 (chrome) / #000080 (deep blue) / #FF00FF (magenta) / #00FFFF (cyan) / #1A1A2E
**Usage**: Landing pages for nostalgic brands, creative portfolios, music apps

---

### Swiss/International Style (1950s–1970s)
**Visual language**: Grid-absolute, Helvetica, photography, geometric order
**Key elements**:
- Strict column grid (always visible in structure)
- Red / black / white — or primary colors only
- Photography as content, never decoration
- Flush-left alignment, no centering
- White space as structure
- Borders and lines as grammar

**Type**: Helvetica Neue (this is the ONE exception to the banned list — if you're doing Swiss) / Aktiv Grotesk
**Palette**: #FFFFFF / #000000 / #E4032E (Swiss red) — or: CMYK primary colors
**Spatial**: The grid IS the design. 12-column, explicit
**Usage**: Design agencies, editorial sites, portfolio

---

### Brutalist Web (2015–present)
**Visual language**: Anti-design, raw HTML aesthetics, visible structure
**Key elements**:
- Visible borders (sometimes all elements bordered)
- Default fonts or deliberately ugly fonts as statement
- No shadows, no gradients
- Forms that look like forms
- Tables that look like tables
- Everything aligned to a hard edge

**Type**: Arial (deliberately) / Times New Roman (deliberately) / or Courier
**Palette**: #FFFFFF / #000000 / one electric color maximum
**Spatial**: No padding, or extreme padding. Nothing in between.
**Usage**: Art projects, experimental products, cultural institutions

---

### Bauhaus (1919–1933)
**Visual language**: Form follows function, geometric shapes, primary colors
**Key elements**:
- Circle, square, triangle as decorative vocabulary
- Primary colors (red, blue, yellow) + black/white
- No decoration that isn't structural
- Typography as architecture
- Asymmetric balance

**Type**: Futura (or: Jost, Nunito — geometric sans)
**Palette**: #E8231A (Bauhaus red) / #0A3270 (Bauhaus blue) / #F5C400 (Bauhaus yellow) / #000000 / #FFFFFF
**Spatial**: Geometric, modular, precise
**Usage**: Design tools, educational platforms, architecture

---

### 90s Print Magazine
**Visual language**: Grunge, distressed, layered, confrontational
**Key elements**:
- Overlapping type and image
- Distressed textures
- Rule-breaking layouts
- Mixed typefaces intentionally
- High visual tension

**Type**: Mix of a heavy slab (Rockwell) + a distressed font + a sans
**Palette**: Saturated CMYK + black / newsprint yellow / muted grunge
**Usage**: Cultural/music brands, zines, streetwear

---

## 3. Industry Archetypes

### Luxury / Maison
**Reference**: Dior.com, Chanel, Hermès digital
**Character**: Restraint is wealth. Space is value.
**Key elements**:
- Serif typography — always (Didot, Garamond, Cormorant)
- Cream/ivory backgrounds (#FAFAF7, #F5F0E8)
- Gold as accent (not yellow — gold: #C9A84C, #B8953A)
- Photography dominates
- Minimal navigation (almost hidden)
- No gradients, no rounded corners
- Generous, almost excessive white space

**Type**: Cormorant Garamond / Playfair Display (display) + Lora / EB Garamond (body)
**Palette**: #FAFAF7 / #E8E2D5 / #1A1A18 / #C9A84C / #8B7355
**Spatial**: Editorial, asymmetric, breathing
**Motion**: Slow, cinematic (600-800ms). Fade only.

---

### Financial / Fintech
**Reference**: Bloomberg Terminal (ultra-dense) or Robinhood (clean)
**Character**: Trust, precision, density
**Key elements** (Bloomberg-inspired):
- Maximum density — no wasted pixels
- Monospace for all numbers
- Color used semantically only (green=up, red=down)
- Tabular layouts
- Dark by default

**Key elements** (Robinhood-inspired):
- High contrast, simple
- Big numbers, small labels
- Positive color palette (greens, blues)
- Minimalist charts

**Type**: Tabular numerals are mandatory. Berkeley Mono / IBM Plex Mono for numbers.
**Palette** (dark fintech): #0D0D0D / #141414 / #1DB954 (green) / #EF4444 (red) / #F5F5F5
**Palette** (light fintech): #FFFFFF / #F0F4FF / #00C805 / #FF3B30 / #1A1A2E

---

### Medical / Health
**Reference**: Modern health apps, clinical tools
**Character**: Calm authority, trust, clarity
**Key elements**:
- Cool whites and light blues
- Never aggressive or alarming colors (except for actual alerts)
- Data visualizations that communicate clearly, not decoratively
- Clear hierarchy — patients and clinicians need it
- Accessible by default (WCAG AA minimum)

**Type**: Readable serif or humanist sans. Source Serif 4 / Libre Baskerville
**Palette**: #F0F9FF / #E0F2FE / #0284C7 / #065F46 / #1E293B
**Spatial**: Generous, structured, never cramped

---

### Creative / Agency
**Reference**: Awwwards-winning agencies, Pentagram, Collins
**Character**: Ideas > execution. Concept first.
**Key elements**:
- One bold concept executed consistently
- Often breaks convention deliberately
- Type as image
- Negative space as design element
- Portfolio-as-product

**Type**: Anything unexpected. The font IS the concept.
**Palette**: Often 2-color max, or full-spectrum, never in-between
**Spatial**: Dictated by concept

---

## 4. Art Movement Archetypes

### De Stijl / Neo-Plasticism
**Reference**: Piet Mondrian, Gerrit Rietveld
**Key elements**: Horizontal/vertical lines only, primary colors, black grid lines
**Type**: Geometric sans, flush left
**Palette**: #FFFFFF / #000000 / #E4032E / #0A3270 / #F5C400

### Art Nouveau
**Reference**: Mucha, Klimt, organic ornament
**Key elements**: Organic curves, floral patterns as borders, warm gold
**Type**: Display serif with swashes (Bodoni / Didot)
**Palette**: #2D1B0E / #8B6914 / #C4A882 / #4A7C59 / #F5DEB3

### Memphis Design (1980s)
**Reference**: Sottsass, bold geometric patterns, playful
**Key elements**: Geometric patterns as backgrounds, bold solid colors, deliberate ugliness
**Type**: Bold slab serif or compressed sans
**Palette**: Pastel + electric: #FF6B9D / #FFE566 / #4ECDC4 / #FF6B35 / #F7F7F7

### Constructivism (Russian, 1920s)
**Reference**: Rodchenko, Lissitzky propaganda posters
**Key elements**: Diagonal composition, red/black/white, bold sans, photomontage
**Type**: Condensed bold sans (Bebas, Oswald)
**Palette**: #CC0000 / #000000 / #FFFFFF — nothing else

---

## 5. Typography-Led Archetypes

These archetypes are defined primarily by their typographic choices.

### The Slab Statement
**Concept**: Heavy slab serif as primary visual weight
**Type**: Rockwell Extra Bold / Alfa Slab One / Zilla Slab Highlight
**Works for**: Product launches, strong brand statements
**Pattern**: Giant slab headline, tiny light sans body. Maximum contrast.

### The Mono Everything
**Concept**: Monospace for all text — creates a technical, precise feel
**Type**: Fragment Mono / Berkeley Mono / IBM Plex Mono
**Works for**: Dev tools, dashboards, data products
**Pattern**: Tabular layout, all text mono, vary size not style

### The Optical Contrast
**Concept**: Extreme size difference between display and body
**Type**: Any serif for display at 80-120px, any sans for body at 15-16px
**Works for**: Editorial, storytelling, marketing
**Pattern**: One word at enormous size, paragraph text almost invisible below

### The Variable Font
**Concept**: Use a variable font and vary weight/width for hierarchy
**Type**: Fraunces (optical sizing) / Recursive / Anybody
**Works for**: Creative portfolios, expressive brands
**Pattern**: Same font family, but weight from 100 to 900 in the same headline

---

## 6. Palette Library

Ready-to-use color systems. Each is named and documented.

### Amber Night
Dark background, warm amber primary. Cozy, focused.
```
bg:      #1C1917  (warm black)
surface: #292524  (dark stone)
primary: #D97706  (amber)
accent:  #FCD34D  (gold)
text:    #E7E5E4  (warm white)
muted:   #78716C  (stone)
```

### Nordic Slate
Cool, desaturated, Scandinavian restraint.
```
bg:      #0F172A  (deep navy)
surface: #1E293B  (slate)
primary: #38BDF8  (sky blue)
accent:  #F0F9FF  (ice white)
text:    #CBD5E1  (cool gray-white)
muted:   #475569  (slate)
```

### Terracotta Studio
Warm, earthy, tactile. Creative and approachable.
```
bg:      #FDF8F3  (parchment)
surface: #F5ECE0  (warm cream)
primary: #C85A38  (terracotta)
accent:  #2D5A27  (forest green)
text:    #1A1209  (warm black)
muted:   #8B7355  (tan)
```

### Forest Dusk
Deep greens, mysterious, editorial.
```
bg:      #0D1F0D  (deep forest)
surface: #1A2E1A  (forest)
primary: #4ADE80  (bright green)
accent:  #FCD34D  (gold)
text:    #F0FDF4  (mint white)
muted:   #4B7A4B  (muted green)
```

### Chalk & Ink
High contrast, print-like, editorial authority.
```
bg:      #F5F0E8  (aged paper)
surface: #EDE8DE  (cream)
primary: #1A1209  (near black)
accent:  #C85A38  (vermillion)
text:    #1A1209  (near black)
muted:   #8B7355  (tan)
```

### Electric Dusk
Vibrant yet refined. Digital native, confident.
```
bg:      #0A0015  (deep purple-black)
surface: #130024  (dark purple)
primary: #7C3AED  (BUT: pure, confident — not washed out)
accent:  #22D3EE  (electric cyan)
text:    #F5F3FF  (purple-white)
muted:   #7C6BA0  (muted purple)
```
⚠️ This is the ONE case where purple is acceptable — when committed fully, not mixed with white backgrounds.

### Sand & Steel
Industrial, precise, masculine.
```
bg:      #F2F0EC  (warm sand)
surface: #E8E4DC  (sand)
primary: #2D3436  (dark steel)
accent:  #E17055  (rust)
text:    #2D3436  (dark steel)
muted:   #B2BEC3  (cool gray)
```

### Obsidian + Gold
Luxury, refined, commanding.
```
bg:      #0A0A08  (near black)
surface: #141410  (dark warm)
primary: #B8953A  (antique gold)
accent:  #F5F0E8  (ivory)
text:    #E8E0CE  (warm cream)
muted:   #6B5E3A  (dark gold)
```

---

## 7. Combination Matrix

Unexpected archetype combinations that work:

| Primary | Secondary | Result |
|---------|-----------|--------|
| Swiss International | Amber Night palette | Cold structure, warm mood |
| Luxury/Maison | Bloomberg density | Premium data product |
| Y2K | Nordic Slate | Nostalgic dark mode |
| Bauhaus | Terracotta Studio | Geometric warmth |
| Mono Everything | Luxury/Maison | High-end developer tool |
| Constructivism | Fintech | Bold, trustworthy urgency |
| Memphis + Chalk & Ink | | Retro playfulness on print |
| Arc Browser feel | Swiss grid | Personal + precise |

**How to combine**: Take the spatial grammar and motion from one archetype, the palette and typography from another. The tension between them creates originality.

---

## How to Use This Library

1. **Read the user's brief** carefully — what is the product, who uses it, what feeling should it evoke?

2. **Eliminate archetypes** that don't fit the context. A medical app shouldn't use Y2K. A creative portfolio can't use pure Fintech density.

3. **Select 1–2 archetypes** (or one from the Combination Matrix). Name them explicitly in your Design Decision Protocol comment.

4. **Extract the specific tokens**: Pull type, palette, spatial, and motion from the archetype directly into your DDP comment block.

5. **Execute faithfully**. The failure mode is always dilution — picking an archetype but softening everything until it looks generic again.

> **The test**: If you removed the archetype label from your code, could someone identify which one you used just by looking at the UI? If yes, you executed it well.
