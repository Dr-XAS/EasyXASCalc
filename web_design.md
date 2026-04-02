# Web Design Style Guide — EasyXASCalc / Dr. XAS

A reference for replicating the visual language of this project in other apps.

---

## Theme & Mode

- **Color mode:** Light theme (warm off-white background, not pure white)
- **Feel:** Clean scientific tool — minimal, professional, slightly soft. Not stark white, not dark mode.

---

## Color Palette

| Role | Variable | Hex |
|---|---|---|
| Page background | `--bg-color` | `#faf8f5` — warm off-white |
| Card background | `--card-bg` | `#ffffff` |
| Primary text | `--text-primary` | `#1e293b` — slate-800 |
| Secondary / muted text | `--text-secondary` / `--text-muted` | `#64748b` — slate-500 |
| Accent / primary action | `--accent-color` / `--primary` | `#9478ac` — muted purple |
| Accent hover | `--accent-hover` / `--primary-hover` | `#7c6396` — darker purple |
| Border | `--border-color` | `#e2e8f0` — slate-200 |
| Active indicator | `--active-element` | `#10b981` — emerald-500 |
| Inactive indicator | `--inactive-element` | `#cbd5e1` — slate-300 |
| Danger / error | — | `#ef4444` — red-500 |
| Alert / warning | — | `#de425b` — rose-red |
| Error background tint | — | `rgba(248, 113, 113, 0.1)` |

### Logo title gradient
```css
background: linear-gradient(to right, #60a5fa, #a78bfa);
/* blue-400 → violet-400 */
```

### Tooltip
- Background: `#1e293b` (dark slate), white text — appears above hovered element with a CSS arrow.

---

## Typography

- **Font stack:** `'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif`
- **Base weight:** 400; buttons 500; headings 600
- **Heading letter-spacing:** `-0.025em` (tight)
- **Label size:** `0.8rem`, muted color, `font-weight: 500`
- **Body / input size:** `0.9em`
- **Anti-aliasing:** `-webkit-font-smoothing: antialiased`

---

## Layout

- **Max content width:** `1600px`, centered with `margin: 0 auto`
- **Main grid:** Two-column — fixed `400px` controls panel on the left, fluid results panel on the right
  ```css
  grid-template-columns: 400px 1fr;
  gap: 2rem;
  ```
- **Breakpoint:** Collapses to single column at `≤ 1024px`
- **Controls panel:** `flex-direction: column; gap: 1.5rem`
- **Results panel:** `flex-direction: column; gap: 2rem; min-height: 500px`

---

## Cards

```css
background: var(--card-bg);        /* #ffffff */
backdrop-filter: blur(12px);
border: none;
border-radius: 16px;
padding: 1.5rem;
box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
transition: transform 0.2s;
```

- **Highlight cards** (e.g. Calculation Mode, Measurement Edges): add `border: 1px solid var(--accent-color)` for a subtle purple border accent.
- **Plot cards:** lighter shadow — `0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -1px rgba(0,0,0,0.06)`, no border.
- **Section header inside card:** bottom border `1px solid var(--border-color)`, `padding-bottom: 0.5rem`, icon + `h2` (`1.1rem`, `font-weight: 600`) + optional action button on the right.

---

## Buttons

### Primary (call-to-action)
```css
background-color: var(--primary);   /* #9478ac */
border-color: var(--primary);
color: white;
border-radius: 8px;
font-weight: 500;
transition: all 0.2s;
```
Hover: `background-color: var(--primary-hover)` (`#7c6396`)

The main Calculate button also gets:
```css
width: 100%;
padding: 1rem;
font-size: 1.1rem;
box-shadow: 0 0 20px rgba(59, 130, 246, 0.3);  /* blue glow */
```

### Default button (ghost)
```css
background-color: rgba(0, 0, 0, 0.05);
border: 1px solid var(--border);
color: var(--text-primary);
border-radius: 8px;
```
Hover: `border-color: var(--primary)`, `background: rgba(59,130,246,0.1)`, `color: var(--primary)`

### Danger button
```css
color: #ef4444;
border-color: rgba(239, 68, 68, 0.3);
background: transparent;
```
Hover: `background: rgba(239,68,68,0.1)`, `border-color: #ef4444`

### Icon button (small square)
```css
padding: 0.4rem;
border-radius: 6px;
background: transparent;
border: 1px solid transparent;
color: var(--text-muted);
```
Hover: `background: rgba(255,255,255,0.1)`, `color: white`

### Toggle button group (mode switcher)
- Wrapper: `background: var(--bg-color)`, `border-radius: 8px`, `padding: 4px`
- Active tab: `background: var(--primary)`, `color: white`, `border-radius: 6px`
- Inactive: transparent background, inherit color
- `font-size: 0.85rem`, `font-weight: 600`, `transition: all 0.2s`

---

## Inputs & Selects

```css
padding: 0.6em;
border-radius: 6px;
border: 1px solid var(--border-color);
background: rgba(255, 255, 255, 0.6);
color: var(--text-primary);
font-size: 0.9em;
width: 100%;
```
Focus ring: `border-color: var(--primary)`, `box-shadow: 0 0 0 2px rgba(59,130,246,0.2)`

---

## Item Rows (list entries)

```css
padding: 0.8rem;
background: rgba(0, 0, 0, 0.03);
border-radius: 8px;
border: 1px solid var(--border-color);
margin-bottom: 0.8rem;
```

---

## Animations

All animated with **Framer Motion** (`motion.div`).

| Interaction | Animation |
|---|---|
| List item enter/exit | `opacity: 0→1`, `height: 0→auto` |
| Result cards enter | `opacity: 0→1`, `y: 20→0`, staggered by `idx * 0.1s` |
| Mode panel expand/collapse | `AnimatePresence` with height + opacity |

CSS keyframe animations:
```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes pop {        /* like button */
  0%  { transform: scale(1); }
  50% { transform: scale(1.2); }
  100%{ transform: scale(1); }
}

@keyframes fadeUp {     /* like count */
  from { opacity: 0; transform: translateY(5px); }
  to   { opacity: 1; transform: translateY(0); }
}
```

---

## Tooltips

Pure CSS, triggered on `:hover` via `data-tooltip` attribute:
- Dark background `#1e293b`, white text, `border-radius: 6px`, max-width `300px`
- Positioned above the element with a CSS arrow pointing down
- Fade in with `opacity: 0 → 1` over `0.2s`
- Labels with tooltips: dotted underline (`text-decoration-style: dotted`), `cursor: help`

---

## Icons

Library: **Lucide React** (`lucide-react`)  
Size used: `16px` for inline/action icons, `18px` for section headers, `48px` for placeholder states.

---

## Header

- Flex row, space-between, `border-bottom: 1px solid var(--border)`
- Logo: image (32px tall) + vertical divider (`2px` wide, `--border-color`) + `h1` with blue→violet gradient text
- `margin-bottom: 2rem`

---

## Footer

- `border-top: 1px solid var(--border-color)`, `padding: 1.5rem 0`, centered flex row
- Secondary text color (`--text-secondary`), `0.9rem`
- Links: accent color (`#9478ac`), no underline by default → underline on hover
- Social icons: `opacity: 0.7` default → `1.0` on hover, `transition: 0.2s`
- Like button: circular (`border-radius: 50%`), filled accent on active, pop animation on click

---

## Plotly Charts

```js
paper_bgcolor: '#ffffff'
plot_bgcolor:  '#ffffff'
font: { color: '#1e293b' }
xaxis/yaxis: { gridcolor: '#e2e8f0', color: '#64748b' }
legend: { bgcolor: 'rgba(255,255,255,0.7)' }
height: 450
config: { responsive: true, displaylogo: false }
```

---

## Summary Checklist for a New Project

- [ ] Light mode, warm off-white page background (`#faf8f5`)
- [ ] Muted purple accent (`#9478ac`) for primary actions and highlights
- [ ] Inter font, tight headings, anti-aliased
- [ ] Cards with `border-radius: 16px` and soft deep shadow
- [ ] Two-column grid layout (fixed sidebar + fluid content), collapses at 1024px
- [ ] Framer Motion for list/panel enter/exit transitions
- [ ] Lucide React icons
- [ ] CSS `data-tooltip` tooltips (dark pill above element)
- [ ] Danger style for destructive actions (red `#ef4444`)
- [ ] Alert color `#de425b` for out-of-range values, paired with `<AlertTriangle>` icon
