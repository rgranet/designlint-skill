# Dashboard & Data UI Reference

## The Dashboard Convergence Trap

Dashboards are the worst offenders for AI convergence:
- Blue KPI cards in a 4-column grid
- Chart.js/Recharts with default color palettes
- Sidebar with icon + label rows
- Top bar with search, avatar, bell icon
- Metric cards with `.rounded-xl shadow-sm border`
- "Total Users", "Revenue", "Conversion Rate" in the same layout every time

A differentiated dashboard **treats data as design material**.

---

## Philosophy: Data as Typography

Numbers are the primary visual element of a dashboard. Treat them like type:

- **Size contrast**: One number should dominate. Not all metrics are equal.
- **Type mix**: Combine monospace (for data) with serif/sans (for labels)
- **Weight as hierarchy**: Bold the number, light the context
- **Color as meaning**: Not decoration — red means down, green means up, but your palette shouldn't be default Bootstrap red/green

---

## Layout Approaches (Break the 4-Column Grid)

### Editorial layout — dominant metric + supporting grid
```
┌────────────────────────────────────┬──────────────┐
│                                    │  Metric 2    │
│   DOMINANT METRIC                  ├──────────────┤
│   (large, commanding)              │  Metric 3    │
│                                    ├──────────────┤
│                                    │  Metric 4    │
├─────────────────┬──────────────────┴──────────────┤
│   Chart A       │   Chart B                        │
└─────────────────┴──────────────────────────────────┘
```

### Utilitarian layout — dense, tabular
```
METRIC   VALUE    CHANGE   TREND
──────   ─────    ──────   ─────
Users    84,291   ↑12.4%   ▁▃▅▇
Revenue  $142k    ↑8.1%    ▃▅▄▇
Sessions 291k     ↓2.3%    ▇▅▃▁
```

### Asymmetric layout — intentional imbalance
```
┌───────────────────────────────┬────────────────┐
│                               │                │
│   Primary Chart (wide)        │  KPIs (narrow) │
│                               │                │
│   ─────────────────────────── │  ──────────    │
│                               │  ──────────    │
│                               │  ──────────    │
└───────────────────────────────┴────────────────┘
```

---

## Metric Card Patterns

**BANNED: The default metric card**
```tsx
// Never do this
<div className="rounded-xl border border-gray-200 p-6 bg-white shadow-sm">
  <p className="text-sm text-gray-500">Total Revenue</p>
  <p className="text-3xl font-bold text-gray-900">$142,891</p>
  <p className="text-sm text-green-500">↑ 12.4% from last month</p>
</div>
```

**Brutalist metric:**
```tsx
<div style={{
  borderTop: '3px solid var(--color-primary)',
  padding: '20px 0',
}}>
  <div style={{ font: 'var(--font-mono)', fontSize: 10, opacity: 0.5, letterSpacing: '0.1em', textTransform: 'uppercase', marginBottom: 8 }}>
    TOTAL REVENUE
  </div>
  <div style={{ font: 'var(--font-display)', fontSize: 48, lineHeight: 1, fontWeight: 700 }}>
    $142k
  </div>
  <div style={{ font: 'var(--font-mono)', fontSize: 12, color: '#4ADE80', marginTop: 8 }}>
    ↑ 12.4%
  </div>
</div>
```

**Editorial metric (dominant):**
```tsx
<div style={{ padding: '48px 40px' }}>
  <span style={{ font: 'var(--font-body)', fontSize: 14, opacity: 0.6 }}>
    Active sessions right now
  </span>
  <div style={{ font: 'var(--font-display)', fontSize: 96, lineHeight: 0.9, letterSpacing: '-0.04em', fontWeight: 800, marginTop: 16 }}>
    291,047
  </div>
  <Sparkline data={sessionTrend} />
</div>
```

---

## Chart Styling — Breaking Recharts/Chart.js Defaults

### Color palettes for charts (never use defaults)

```ts
// Warm palette (for dark backgrounds)
const WARM = ['#D97706', '#F59E0B', '#FCD34D', '#78716C', '#44403C']

// Dusty palette
const DUSTY = ['#87A878', '#C85A38', '#6B7FAB', '#C9A84C', '#8B6E8B']

// Monochromatic with accent
const MONO = ['#E7E5E4', '#A8A29E', '#78716C', '#44403C', '#1C1917']
// Add one accent: '#D97706'
```

### Recharts — stripped down, intentional

```tsx
<AreaChart data={data} margin={{ top: 0, right: 0, left: 0, bottom: 0 }}>
  <defs>
    <linearGradient id="fill" x1="0" y1="0" x2="0" y2="1">
      <stop offset="5%" stopColor="var(--color-primary)" stopOpacity={0.3} />
      <stop offset="95%" stopColor="var(--color-primary)" stopOpacity={0} />
    </linearGradient>
  </defs>
  {/* No CartesianGrid by default — add only if needed */}
  <XAxis
    tick={{ fontFamily: 'var(--font-display)', fontSize: 10, fill: 'var(--color-text-muted)' }}
    axisLine={false}
    tickLine={false}
  />
  <YAxis hide={true} /> {/* Often better hidden */}
  <Area
    type="monotone"
    dataKey="value"
    stroke="var(--color-primary)"
    strokeWidth={2}
    fill="url(#fill)"
    dot={false}
    activeDot={{ r: 4, fill: 'var(--color-accent)' }}
  />
</AreaChart>
```

### Sparklines — inline data in text

```tsx
function Sparkline({ data, color }: { data: number[], color: string }) {
  const max = Math.max(...data)
  const min = Math.min(...data)
  const normalize = (v: number) => ((v - min) / (max - min)) * 24
  
  return (
    <svg width={data.length * 4} height={28} style={{ display: 'inline-block', verticalAlign: 'middle' }}>
      {data.map((v, i) => (
        <rect
          key={i}
          x={i * 4}
          y={28 - normalize(v)}
          width={3}
          height={normalize(v)}
          fill={color}
          opacity={i === data.length - 1 ? 1 : 0.4 + (i / data.length) * 0.4}
        />
      ))}
    </svg>
  )
}
```

---

## Sidebar Alternatives

**BANNED: icon + label rows with system blue active state**

```tsx
// Alternative 1: Top nav with underline tabs (no sidebar at all)
// Alternative 2: Minimal left strip — icons only, tooltip on hover
// Alternative 3: Full-width collapsible header sections
// Alternative 4: Command palette as primary navigation (⌘K)

// Minimal icon sidebar
<nav style={{ 
  width: 48, 
  background: 'var(--color-surface)',
  borderRight: '1px solid rgba(255,255,255,0.06)',
  display: 'flex',
  flexDirection: 'column',
  alignItems: 'center',
  padding: '16px 0',
  gap: 4
}}>
  {navItems.map(item => (
    <NavIcon key={item.id} item={item} active={current === item.id} />
  ))}
</nav>
```

---

## Signature Details for Dashboards

### Real-time update indicator (not a spinner)
```tsx
function LiveIndicator() {
  return (
    <span style={{ display: 'flex', alignItems: 'center', gap: 6, font: 'var(--font-display)', fontSize: 10, opacity: 0.6 }}>
      <span style={{
        width: 6,
        height: 6,
        borderRadius: '50%',
        background: '#4ADE80',
        animation: 'pulse 2s infinite',
      }} />
      LIVE
    </span>
  )
}
```

### Data timestamp (always show when data was last updated)
```tsx
<span style={{ fontFamily: 'var(--font-display)', fontSize: 10, opacity: 0.35 }}>
  Updated {formatDistanceToNow(lastUpdated)} ago
</span>
```

### Percentage change with direction
```tsx
function Delta({ value }: { value: number }) {
  const positive = value >= 0
  return (
    <span style={{
      fontFamily: 'var(--font-display)',
      fontSize: 12,
      color: positive ? '#4ADE80' : '#F87171',
      letterSpacing: '0.02em'
    }}>
      {positive ? '↑' : '↓'} {Math.abs(value).toFixed(1)}%
    </span>
  )
}
```
