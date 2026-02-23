# EasyXASCalc - UI Design & Architecture Guide

This guide summarizes the UI design principles, technology stack, color variables, and layout structures used in the **EasyXASCalc Web** project. You can use this as a reference or a template to build new projects with a similar premium, modern, and accessible aesthetic.

## 1. Technology Stack

* **Frameworks:** React 19 + Vite
* **Language:** JavaScript (ES Modules, JSX)
* **Styling:** Vanilla CSS configured with global CSS variables (`index.css`, `App.css`).
* **Iconography:** `lucide-react` (Clean, modern SVG icons with adjustable stroke widths).
* **Animations:** `framer-motion` (Used for mounting/unmounting elements, smooth height transitions, and stagger effects).
* **Data Visualization:** `react-plotly.js` (Customized to match the app's clean light-theme aesthetic).
* **Math Rendering:** `react-katex` (For rendering chemical formulas and math equations beautifully).

## 2. Color Palette & Theming

The UI employs a clean **Light Theme** with soft "glassmorphic" elements, slate-colored typography, and muted purple/blue accents to ensure high readability and a premium scientific feel.

### Global CSS Variables

Define these in your `:root` selector:

```css
:root {
  /* Backgrounds */
  --bg-color: #faf8f5;        /* Soft off-white canvas */
  --card-bg: #ffffff;         /* Pure white for foreground cards */
  
  /* Typography */
  --text-primary: #1e293b;    /* Slate 800: High contrast for readability */
  --text-secondary: #64748b;  /* Slate 500: For labels, muted text, hints */
  
  /* Brand / Accents */
  --accent-color: #9478ac;    /* Muted sophisticated purple */
  --accent-hover: #7c6396;    /* Darker purple for hover states */
  --border-color: #e2e8f0;    /* Slate 200: Subtle borders */
  
  /* Status Colors */
  --active-element: #10b981;  /* Emerald: Success/Active states */
  --inactive-element: #cbd5e1;/* Slate 300: Disabled states */
  
  /* Aliases (for simpler class writing) */
  --primary: var(--accent-color);
  --primary-hover: var(--accent-hover);
  --bg-card: var(--card-bg);
  --border: var(--border-color);
  --text-muted: var(--text-secondary);
}
```

### Gradients

The logo/header uses a modern text gradient to draw attention without being overwhelming:

* **Text Gradient:** `linear-gradient(to right, #60a5fa, #a78bfa)` (Blue-400 to Purple-400).

## 3. Typography

* **Font Family:** `'Inter', system-ui, -apple-system, sans-serif`
* **Weights:**
  * **400 (Regular):** Body text, inputs.
  * **500 (Medium):** Button text, small section labels.
  * **600 (Semi-bold):** Headers (h1, h2, h3).

## 4. UI Components & Layouts

### Layout Architecture

* **Page Container (`.app-container`):** Constrained to a max-width of `1600px` to prevent stretching on ultrawide monitors, centrally aligned with `margin: 0 auto` and `1rem` padding.
* **Grid Layout (`.panels-grid`):**
  * A responsive two-column CSS Grid format: `grid-template-columns: 400px 1fr;`
  * Left column (fixed width) contains input controls and configuration cards.
  * Right column (flexible) contains the results/plots.
  * On small screens (`< 1024px`), it collapses to a single column (`grid-template-columns: 1fr;`).

### Cards & Glassmorphism

Elements are placed inside visually distinct cards to separate concerns.

```css
.card {
  background: var(--bg-card);
  backdrop-filter: blur(12px); /* Slight glassmorphic effect */
  border-radius: 16px;
  padding: 1.5rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3); /* Provides depth */
}
```

### Buttons

Buttons avoid harsh solid colors unless primary.

* **Default Button:** Transparent with a subtle grey background (`rgba(0,0,0,0.05)`) and slate text. Hovering changes border to primary color and background to a very light blue tint.
* **Primary Button:** Uses `--primary` background. Includes a soft blue drop shadow (`box-shadow: 0 0 20px rgba(59, 130, 246, 0.3)`) to make it pop.
* **Icon Buttons:** Minimalist; transparent background initially, turning to a faint solid on hover.
* **Border Radius:** Soft `8px` rounding.

### Inputs & Selects

* Background: Slightly transparent white (`rgba(255, 255, 255, 0.6)`).
* Border: Defined by `--border-color` (`#e2e8f0`).
* Focus State: Uses a primary colored outline ring (`box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.2)`).

### List Rows

Repeating items (like components or edges) are wrapped in `.item-row`:

* Background: `rgba(0, 0, 0, 0.03)`
* Border: `1px solid var(--border-color)`
* Border Radius: `8px`
* Layout: Flexbox (`display: flex; gap: 1rem; align-items: center;`)

## 5. Animations & Micro-interactions

Using `framer-motion` adds horizontal and vertical flow to the UI, making it feel "alive".

* **List Items:** Wrap repeating items in `<AnimatePresence>`.
  * *Initial state:* `opacity: 0, height: 0`
  * *Animate state:* `opacity: 1, height: 'auto'`
  * *Exit state:* `opacity: 0, height: 0`
* **Result Cards:** Staggered load effect. As multiple plots load, use `transition={{ delay: index * 0.1 }}` with a slide-up motion (`y: 20` to `y: 0`).
* **CSS Keyframes:** A simple `@keyframes fadeIn` is used as a fallback for standard `.animate-fade-in` utility classes.

## 6. Plotly Configuration

To make `react-plotly.js` match the React theme perfectly, specific layout overrides are passed via props:

```javascript
layout={{
  paper_bgcolor: '#ffffff',
  plot_bgcolor: '#ffffff',
  font: { color: '#1e293b' }, // matches --text-primary
  xaxis: { gridcolor: '#e2e8f0', color: '#64748b' }, // matches --border-color and --text-secondary
  yaxis: { gridcolor: '#e2e8f0', color: '#64748b' },
  legend: { bgcolor: 'rgba(255,255,255,0.7)' } // slight transparency
}}
```
