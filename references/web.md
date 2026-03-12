# Web UI Reference (React / Next.js / HTML+CSS)

## CSS Custom Properties — Required Structure

Always declare design tokens as CSS variables. Never hardcode color/spacing values inline.

```css
:root {
  /* Tokens from your DDP */
  --color-bg: #1C1917;
  --color-surface: #292524;
  --color-primary: #D97706;
  --color-accent: #FCD34D;
  --color-text: #E7E5E4;
  --color-text-muted: #A8A29E;

  /* Typography scale — break defaults */
  --font-display: 'Fragment Mono', monospace;
  --font-body: 'Source Serif 4', serif;
  --font-size-base: 17px;     /* Not 16px */
  --line-height-body: 1.65;   /* Not 1.5 */
  --letter-spacing-display: -0.03em;

  /* Spatial tokens */
  --space-xs: 6px;
  --space-sm: 14px;
  --space-md: 28px;
  --space-lg: 56px;
  --space-xl: 112px;   /* Generous — don't be afraid of it */

  /* Motion */
  --ease-snappy: cubic-bezier(0.4, 0, 0.2, 1);
  --ease-elastic: cubic-bezier(0.34, 1.56, 0.64, 1);
  --duration-fast: 120ms;
  --duration-base: 200ms;
  --duration-slow: 500ms;
}
```

## Google Fonts Loading (Next.js)

```tsx
// app/layout.tsx
import { Fragment_Mono, Source_Serif_4 } from 'next/font/google'

const displayFont = Fragment_Mono({
  weight: ['400'],
  subsets: ['latin'],
  variable: '--font-display',
})

const bodyFont = Source_Serif_4({
  weight: ['300', '400', '600'],
  subsets: ['latin'],
  variable: '--font-body',
})
```

## Anti-Pattern: The Generic Card

**Never do this:**
```tsx
<div className="rounded-xl border border-gray-200 p-6 shadow-sm bg-white">
```

**Do this instead** (pick ONE approach based on your DDP):

```tsx
{/* Brutalist: no radius, explicit border */}
<div style={{ border: '1.5px solid var(--color-primary)', padding: '20px 24px' }}>

{/* Editorial: asymmetric padding */}
<div style={{ padding: '32px 48px 32px 24px', borderLeft: '3px solid var(--color-accent)' }}>

{/* Luxury: generous space, no border */}
<div style={{ padding: '48px', background: 'var(--color-surface)' }}>

{/* Utilitarian: tight, tabular */}
<div style={{ padding: '12px 16px', borderBottom: '1px solid rgba(255,255,255,0.1)' }}>
```

## Typography Hierarchy Patterns

```css
/* Display — commanding, not polite */
.heading-display {
  font-family: var(--font-display);
  font-size: clamp(2.5rem, 6vw, 5rem);
  line-height: 0.95;
  letter-spacing: -0.04em;
  font-weight: 700;
}

/* Label — functional, precise */
.label-ui {
  font-family: var(--font-display);
  font-size: 11px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  opacity: 0.6;
}

/* Body — readable, warm */
.body-text {
  font-family: var(--font-body);
  font-size: var(--font-size-base);
  line-height: var(--line-height-body);
  font-weight: 300;
}
```

## Staggered List Animation (CSS)

```css
.list-item {
  opacity: 0;
  transform: translateY(8px);
  animation: enter var(--duration-base) var(--ease-snappy) forwards;
}

.list-item:nth-child(1) { animation-delay: 0ms; }
.list-item:nth-child(2) { animation-delay: 50ms; }
.list-item:nth-child(3) { animation-delay: 100ms; }
.list-item:nth-child(4) { animation-delay: 150ms; }
.list-item:nth-child(n+5) { animation-delay: 200ms; }

@keyframes enter {
  to { opacity: 1; transform: translateY(0); }
}
```

## Signature Details — Code Snippets

### Grain texture overlay
```css
.with-grain::after {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 9999;
  opacity: 0.4;
}
```

### Thin accent line under active nav
```css
.nav-item {
  position: relative;
  padding-bottom: 4px;
}
.nav-item.active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 1.5px;
  background: var(--color-accent);
  /* No transition — instant, physical */
}
```

### Live timestamp detail
```tsx
function LiveClock() {
  const [time, setTime] = useState(new Date())
  useEffect(() => {
    const t = setInterval(() => setTime(new Date()), 1000)
    return () => clearInterval(t)
  }, [])
  return (
    <span style={{ fontFamily: 'var(--font-display)', fontSize: 11, opacity: 0.4 }}>
      {time.toLocaleTimeString('en-US', { hour12: false })}
    </span>
  )
}
```

## Layout Breaks — Editorial Escapes

```css
/* Full-bleed element that escapes container */
.bleed-left {
  margin-left: calc(-1 * var(--space-lg));
  padding-left: var(--space-lg);
}

/* Asymmetric two-column that isn't 50/50 */
.split-editorial {
  display: grid;
  grid-template-columns: 2fr 5fr;  /* Not 1fr 1fr */
  gap: var(--space-lg);
}

/* Overlapping elements */
.overlap-card {
  position: relative;
  margin-top: -40px;
  z-index: 1;
}
```
