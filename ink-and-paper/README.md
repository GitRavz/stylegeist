# OMS Design Spec — "Ink & Paper" (CMYK Print-Shop UI)

A portable, self-contained design system you can hand to another AI or developer to
recreate the same look-and-feel. Everything below is drop-in: paste the token block,
follow the layout shell, and reuse the component recipes.

---

## 0. Prompt preamble (paste this first)

> Build the UI using the **"Ink & Paper"** design system: a print-shop metaphor where a
> near-black **ink** sidebar frames white **paper** cards on a neutral light-gray page.
> CMYK process inks (cyan/magenta/yellow) are used **only** as semantic accents — never
> decoratively. One accent (cyan) drives all interactivity. Flat surfaces: a single
> hairline border plus one soft shadow, no heavy drop-shadows, no gradients except the
> one CMYK "registration strip" brand moment. Typeface is Plus Jakarta Sans throughout.
> Use the design tokens, layout shell, and component recipes exactly as specified.

---

## 1. Core concept

- **Ink sidebar, paper content.** Fixed dark sidebar (`#101014`), white cards float on a
  light-gray page (`#f3f4f6`, chroma 0 — a true neutral gray, *never* cream/beige).
- **CMYK inks are semantic.** Cyan = the single interactive accent. Magenta = alerts.
  Yellow = warnings only. Never use them just to decorate.
- **Flat elevation.** Cards get one hairline border + one very soft shadow. No drama.
- **One brand moment per screen:** the CMYK "registration strip" (a 4px bar split into
  C / M / Y / K quarters). Used once — under the logo or on the hero — never repeated.

---

## 2. Design tokens (drop-in CSS)

```css
:root {
  /* ── Ink / paper ── */
  --ink:      #101014;   /* sidebar bg, primary buttons, strongest text */
  --ink-2:    #1a1a20;   /* ink hover */
  --paper:    #ffffff;   /* cards, sheets, active nav pill */
  --bg:       #f3f4f6;   /* page background (neutral gray — never cream) */
  --line:     #e5e6ea;   /* hairline card borders */
  --line-2:   #eef0f3;   /* softer inner dividers / tinted rows */
  --text:     #16161a;   /* body text */
  --text-2:   #3a3c43;   /* secondary body */
  --muted:    #64676f;   /* labels, sublabels (>=4.5:1 on white) */
  --faint:    #9a9ca3;   /* placeholder / disabled / decorative */

  /* ── CMYK process inks (semantic, used sparingly) ── */
  --c:        #00aeef;   /* CYAN — the single interactive accent (fills, indicators) */
  --c-ink:    #006e9e;   /* cyan as TEXT on white (>=4.5:1) — links, ID numbers */
  --c-icon:   #0095cf;   /* cyan for active icons on the ink sidebar */
  --c-wash:   #e5f6fd;   /* cyan tint surface */
  --c-ring:   rgba(0,174,239,.14);  /* focus ring / soft fill */
  --m:        #ec008c;   /* MAGENTA — alert / attention fills */
  --m-deep:   #c0006c;   /* magenta badge bg (white text >=4.5:1) */
  --y:        #ffcf00;   /* YELLOW — warning moments only */

  /* ── Semantic status vocabulary (chip bg / chip text) ── */
  --st-approval-bg:#e5f6fd; --st-approval-tx:#006e9e; /* "For Approval" — cyan   */
  --st-pending-bg: #fbf3da; --st-pending-tx: #9a6200; /* "Pending"      — amber  */
  --st-process-bg: #e8f0fe; --st-process-tx: #1d4ed8; /* "In Process"   — blue   */
  --st-release-bg: #f1ecfe; --st-release-tx: #6d28d9; /* "For Release"  — violet */
  --st-done-bg:    #e7f6ec; --st-done-tx:    #15803d; /* "Completed"    — green  */
  --st-cancel-bg:  #fdecec; --st-cancel-tx:  #b91c1c; /* "Cancelled"    — red    */

  /* ── Due / deadline chips ── */
  --due-over-bg: #fdecec; --due-over-tx: #b91c1c;  /* overdue   */
  --due-today-bg:#fbf3da; --due-today-tx:#9a6200;  /* due today */
  --due-soon-bg: #fdeee3; --due-soon-tx: #c2410c;  /* due soon  */
  --due-ok-bg:   #e7f6ec; --due-ok-tx:   #15803d;  /* on time   */

  /* ── Money ── */
  --paid: #15803d; --paid-bg: #e7f6ec;   /* amount paid (green) */
  --due:  #b91c1c; --due-bg:  #fdecec;   /* balance due (red)   */

  /* ── Radii ── */
  --r-sm: 8px;  --r: 12px;  --r-lg: 16px;  --r-pill: 999px;
  --radius: 14px;            /* the card radius used on dashboards */

  /* ── Elevation (flat: hairline + one soft shadow) ── */
  --shadow:    0 1px 2px rgba(16,16,20,.05);
  --shadow-md: 0 4px 16px rgba(16,16,20,.08);

  /* ── Motion ── */
  --ease-out: cubic-bezier(.22,1,.36,1);   /* ease-out-quint */
  --t-fast: .15s;  --t: .2s;

  /* ── Type ── */
  --font: 'Plus Jakarta Sans', 'Segoe UI', system-ui, -apple-system, sans-serif;
  --mono: 'JetBrains Mono', ui-monospace, 'SFMono-Regular', Menlo, monospace;

  /* ── z-scale (semantic) ── */
  --z-sidebar:100; --z-dropdown:200; --z-sticky:300;
  --z-backdrop:400; --z-modal:500; --z-toast:600; --z-tooltip:700;
}

@media (prefers-reduced-motion: reduce) {
  :root { --t-fast: 0s; --t: 0s; }
}
```

> **Font note:** Load Plus Jakarta Sans (Google Fonts) in the `<head>`. It is the one
> family everywhere. (Some internal token files list `Inter` as a fallback default, but
> the shipped UI uses **Plus Jakarta Sans** — treat that as canonical.)

---

## 3. Typography

- **Family:** Plus Jakarta Sans everywhere. Fallback Segoe UI / system-ui.
- **Scale** (ratio ~1.2):
  | Role | Size | Weight | Notes |
  |------|------|--------|-------|
  | Micro label | 11px | 700 | UPPERCASE, `letter-spacing: .04–.06em` |
  | Table / body | 12–13px | 400–600 | |
  | Nav item | 14px | 500 (700 active) | |
  | Card title | 15–16px | 700 | |
  | Page title | 24px | 800 | `letter-spacing: -.02em` |
  | Stat / KPI value | 21–32px | 800 | |
- **All numbers** (money, counts, IDs, dates): `font-variant-numeric: tabular-nums;`
- Tight negative tracking on big bold text (`-.01em` to `-.02em`); positive tracking on
  tiny uppercase labels.

---

## 4. Layout shell (the app frame)

Fixed ink sidebar on the left, scrollable paper content on the right.

```
┌────────────┬──────────────────────────────────────────┐
│  SIDEBAR   │  CONTENT (bg = #f3f4f6)                   │
│  260px     │  .container-fluid: max-width 1400px,      │
│  #101014   │  centered, padding 28px 24px              │
│  fixed     │                                            │
│            │  [ hero / banner ]                         │
│  logo +    │  [ header + filters ]                      │
│  CMYK strip│  [ stat cards grid ]                       │
│            │  [ 2-col main grid: 1fr / 300px ]          │
│  nav items │                                            │
│            │                                            │
│  footer:   │                                            │
│  user +    │                                            │
│  logout    │                                            │
└────────────┴──────────────────────────────────────────┘
```

Key rules:

- `body { margin-left: 260px; background: var(--bg); font-family: var(--font); }`
- `.sidebar { position: fixed; left:0; top:0; width:260px; height:100vh; background: var(--ink); display:flex; flex-direction:column; z-index:100; }`
- Content wrapper: `.container-fluid { max-width:1400px; margin:0 auto; padding:28px 24px; }`
- **Mobile (<=768px):** sidebar slides off-canvas (`transform: translateX(-100%)`),
  `body { margin-left:0; }`, a 42px hamburger toggle (top-left, ink) opens it, and a
  dark scrim (`rgba(10,10,14,.5)`) dims + locks the page behind the drawer.

### Dashboard grids

```css
.stat-cards-row   { display:grid; grid-template-columns:repeat(3,1fr); gap:16px; }
.status-cards-grid{ display:grid; grid-template-columns:repeat(auto-fit,minmax(170px,1fr)); gap:14px; }
.main-grid        { display:grid; grid-template-columns:1fr 300px; gap:20px; align-items:start; }
/* collapse main-grid to 1 column <=1100px; stat row to 1 column <=900px */
```

---

## 5. Component recipes

### Card (base surface)
```css
background: var(--paper);
border: 1px solid var(--line);
border-radius: var(--radius);          /* 14px */
box-shadow: var(--shadow);             /* 0 1px 2px rgba(16,16,20,.05) */
```
No hover lift on non-clickable cards. Clickable cards lift `translateY(-2px)` + accent
border + `box-shadow: 0 6px 16px rgba(16,16,20,.08)`.

### Sidebar nav item
- Base: muted text (`#b4b6bf`), icon `#8d8f99`, `padding:11px 14px`, `border-radius:10px`.
- Hover: `background: rgba(255,255,255,.06); color:#fff;`
- **Active = white "paper" pill:** `background: var(--paper); color: var(--ink); font-weight:700;`
  with a **cyan icon** (`var(--c-icon)`). No side-stripe indicators.
- Section titles: 11px 700 uppercase, `letter-spacing:1.2px`, color `#8b8b90`.

### Sidebar logo + CMYK registration strip (the brand moment — use ONCE)
White logo sits directly on the ink (no plate). Underneath, a 4px bar:
```css
background: linear-gradient(to right,
  var(--c) 0 25%, var(--m) 25% 50%, var(--y) 50% 75%,
  rgba(255,255,255,.92) 75% 100%);   /* K quarter is paper-white on the ink bg */
```

### Primary button
```css
background: var(--ink); color:#fff; border:none;
border-radius: var(--r-sm);            /* 8px */
padding: 8–11px 14–20px; font-weight:700;
```
Hover → `background: var(--ink-2)`. Text links use `var(--c-ink)`.

### Status chip / due chip
Pill, 11px 700, tinted bg + dark text from the vocabulary in §2:
```css
display:inline-flex; padding:3px 10px; border-radius:999px;
font-size:11px; font-weight:700; white-space:nowrap;
/* e.g. .completed { background:var(--st-done-bg); color:var(--st-done-tx); } */
```

### Alert badge (counts)
```css
background: var(--m-deep); color:#fff; font:800 11px;
min-width:20px; height:20px; border-radius:999px; padding:0 6px;
```
Optional pulse ring animation; disabled under reduced motion.

### Tabs
13px 600, muted; active = ink text + 2px cyan bottom-border (`border-bottom:2px solid var(--c)`).

### Segmented range control (date filters etc.)
Bordered button group, `overflow:hidden`, `border-radius:8px`; active segment =
`background: var(--ink); color:#fff;`.

### Table
- Header: `#fafafb` bg, 11px 700 uppercase muted text, `letter-spacing:.06em`.
- Cells: 12–13px, `border-bottom:1px solid #f1f2f4`, `vertical-align:middle`.
- Row hover: `background:#fafafb`. Numbers use tabular-nums.

### Hero / banner (ink card)
Dark card (`var(--ink)`) with white text, a subtle halftone dot field masked to fade in
from one side, the CMYK strip along the bottom edge, and a white paper CTA button.
```css
/* halftone field */
background-image: radial-gradient(rgba(255,255,255,.07) 1px, transparent 1.6px);
background-size: 14px 14px;
mask-image: linear-gradient(105deg, transparent 40%, #000 100%);
```

---

## 6. Motion

- 150–200ms `ease-out` on hover / focus / state changes only. No entrance choreography.
- `@media (prefers-reduced-motion: reduce)` turns all transitions/animations off.

---

## 7. Charts (if using Chart.js or similar)

- Font: Plus Jakarta Sans.
- Current-period line: ink `#101014`. Comparison line: light cyan `#7cccee`, dashed.
- Area fills: <=12% alpha cyan. Tooltips: ink bg, white text. Tick labels: `#8b8e96`.

---

## 8. Accessibility

- All muted text meets >=4.5:1 on white (that's why `--c-ink` exists for cyan-as-text —
  never use the bright `--c` #00aeef for text on white).
- Focus ring everywhere: `outline: 2px solid var(--c); outline-offset: 2px;`
- Status is never encoded by color alone — always paired with a text label.
