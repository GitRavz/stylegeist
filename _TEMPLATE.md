# <System Name> Design Spec — "<Short Tagline / Theme>"

A portable, self-contained design system you can hand to another AI or developer to
recreate the same look-and-feel. Paste the token block, follow the layout shell, and
reuse the component recipes.

> **How to use this template:** copy this file to `<system-name>/README.md`, fill in every
> `<...>` placeholder, delete any section that doesn't apply, then add a row to the table
> in the top-level [`README.md`](README.md).

---

## 0. Prompt preamble (paste this first)

> Build the UI using the **"<System Name>"** design system: <one or two sentences that
> capture the whole vibe — the metaphor, the mood, the one rule that matters most>.
> Use the design tokens, layout shell, and component recipes exactly as specified.

---

## 1. Core concept

- **<Big idea #1>** — <what it means in practice>.
- **<Big idea #2>** — <e.g. how accent colors are used / restraint rules>.
- **<Big idea #3>** — <elevation / texture / density philosophy>.
- **One signature moment:** <the single memorable brand detail, used sparingly>.

---

## 2. Design tokens (drop-in CSS)

```css
:root {
  /* ── Surfaces ── */
  --bg:       <#______>;   /* page background */
  --surface:  <#______>;   /* cards / panels */
  --line:     <#______>;   /* hairline borders */

  /* ── Text ── */
  --text:     <#______>;   /* body text */
  --muted:    <#______>;   /* labels / secondary (>=4.5:1 on surface) */

  /* ── Accents ── */
  --accent:     <#______>; /* the single interactive accent (fills/indicators) */
  --accent-ink: <#______>; /* accent as TEXT on light bg (>=4.5:1) — links */

  /* ── Status vocabulary (chip bg / chip text) ── */
  --st-ok-bg:    <#______>; --st-ok-tx:    <#______>; /* success */
  --st-warn-bg:  <#______>; --st-warn-tx:  <#______>; /* warning */
  --st-info-bg:  <#______>; --st-info-tx:  <#______>; /* info    */
  --st-danger-bg:<#______>; --st-danger-tx:<#______>; /* danger  */

  /* ── Radii ── */
  --r-sm: <8px>;  --r: <12px>;  --r-lg: <16px>;  --r-pill: 999px;

  /* ── Elevation ── */
  --shadow:    <0 1px 2px rgba(0,0,0,.05)>;
  --shadow-md: <0 4px 16px rgba(0,0,0,.08)>;

  /* ── Motion ── */
  --ease-out: <cubic-bezier(.22,1,.36,1)>;
  --t-fast: .15s;  --t: .2s;

  /* ── Type ── */
  --font: '<Primary Font>', system-ui, -apple-system, sans-serif;
  --mono: '<Mono Font>', ui-monospace, Menlo, monospace;
}

@media (prefers-reduced-motion: reduce) {
  :root { --t-fast: 0s; --t: 0s; }
}
```

> **Font note:** load `<Primary Font>` in the `<head>`. It is the one family everywhere.

---

## 3. Typography

- **Family:** `<Primary Font>`, fallback system-ui.
- **Scale** (ratio ~<1.2>):
  | Role | Size | Weight | Notes |
  |------|------|--------|-------|
  | Micro label | <11px> | <700> | UPPERCASE, `letter-spacing: <.05em>` |
  | Body / table | <13px> | <400–600> | |
  | Card title | <16px> | <700> | |
  | Page title | <24px> | <800> | `letter-spacing: <-.02em>` |
  | Stat value | <32px> | <800> | |
- **All numbers:** `font-variant-numeric: tabular-nums;`

---

## 4. Layout shell (the app frame)

<Describe the frame: sidebar? top bar? content max-width? Sketch it.>

```
<ASCII sketch of the shell>
```

Key rules:

- `body { <base rules> }`
- Content wrapper: `.container { max-width: <____px>; margin: 0 auto; padding: <__ __>; }`
- **Mobile (<=768px):** <how the shell collapses>.

### Core grids

```css
.stat-row  { display:grid; grid-template-columns: repeat(<n>, 1fr); gap: <16px>; }
.main-grid { display:grid; grid-template-columns: 1fr <300px>; gap: <20px>; }
/* <collapse rules at breakpoints> */
```

---

## 5. Component recipes

### Card (base surface)
```css
background: var(--surface);
border: 1px solid var(--line);
border-radius: var(--r);
box-shadow: var(--shadow);
```

### Primary button
```css
background: <var(--accent) | var(--ink)>; color: #fff; border: none;
border-radius: var(--r-sm); padding: <__ __>; font-weight: 700;
```

### Status / chip
```css
display:inline-flex; padding: 3px 10px; border-radius: 999px;
font-size: 11px; font-weight: 700;
/* e.g. .ok { background: var(--st-ok-bg); color: var(--st-ok-tx); } */
```

### <Other signature components>
<Nav item, tabs, table, badge, hero, modal — document whatever this system needs.>

---

## 6. Motion

- <150–200ms> `ease-out` on hover / focus / state only. <No entrance choreography, etc.>
- `@media (prefers-reduced-motion: reduce)` turns all transitions/animations off.

---

## 7. Charts (if applicable)

- Font: `<Primary Font>`. Series colors: <primary>, <comparison>. Tooltips: <style>.

---

## 8. Accessibility

- Muted text meets >=4.5:1 on its background (use `--accent-ink` for accent-as-text).
- Focus ring everywhere: `outline: 2px solid var(--accent); outline-offset: 2px;`
- Never encode status by color alone — always pair with a text label.
