# Design System Reference

## CSS Variables (`:root`)

```css
:root {
  --rose:     #E8556A;   /* primary CTA, hearts, accents */
  --rose-lt:  #FDEEF0;   /* light rose backgrounds */
  --marigold: #F4A614;   /* floral dividers, highlights */
  --gold:     #D4840A;   /* deeper gold accents */
  --cream:    #FFF8EE;   /* page background */
  --blush:    #FDF0E8;   /* alternate warm background */
  --sage:     #6B9E6C;   /* green petal variant */
  --sage-lt:  #E4F1E4;   /* light sage backgrounds */
  --text:     #2C1A12;   /* primary text, footer bg */
  --muted:    #7A5C4A;   /* secondary text, labels */
}
```

Adjust these per theme. For example, for a "Modern & minimal" theme swap cream → `#F8F8F8` and rose → `#C0395A`.

---

## Color palette by theme

### Warm & joyful (default)
- Background: `#FFF8EE` (cream)
- Primary: `#E8556A` (rose)
- Accent: `#F4A614` (marigold)
- Text: `#2C1A12`
- Petal colors: `['#F4A614','#E8556A','#F9C74F','#F8A5B0','#6B9E6C','#FFCBA4']`

### Romantic & elegant
- Background: `#FDF5F7`
- Primary: `#C0395A`
- Accent: `#D4840A`
- Text: `#1A0A10`
- Petal colors: `['#C0395A','#D4840A','#F0C0CA','#8B1A3A','#FFD700','#F8B4C8']`

### Modern & minimal
- Background: `#F9FAFB`
- Primary: `#4A5568`
- Accent: `#F9A8BE`
- Text: `#1A202C`
- Petal colors: `['#F9A8BE','#4A5568','#CBD5E0','#FEB2B2','#9AE6B4','#FED7D7']`

---

## Typography

```css
/* Import in <head> */
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,500;0,700;1,500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
```

| Role | Font | Size | Weight |
|---|---|---|---|
| Display / names | Playfair Display | `clamp(3rem, 9vw, 6.5rem)` | 700 |
| Italic accents | Playfair Display italic | varies | 500 |
| Body / UI | DM Sans | 1rem | 400 |
| Labels / eyebrows | DM Sans | 0.78–0.85rem | 500 |
| Muted / captions | DM Sans | 0.8–0.88rem | 300–400 |

Never use Arial, Inter, Roboto, or system fonts. These two fonts cover all use cases.

---

## Spacing & layout

```css
section {
  position: relative;
  z-index: 1;
  padding: 4rem 2rem;
  max-width: 1100px;
  margin: 0 auto;
}
```

- Section padding: `4rem 2rem`
- Max content width: `1100px`
- Card border-radius: `16–24px`
- Button border-radius: `50px` (pill)
- Gap between grid items: `1.25rem`

---

## Section eyebrow + title pattern

```html
<p class="section-eyebrow reveal">Subtitle label</p>
<h2 class="section-title reveal">Main Heading</h2>
```

```css
.section-eyebrow {
  text-align: center;
  font-size: 0.78rem;
  letter-spacing: 0.3em;
  text-transform: uppercase;
  color: var(--rose);
  font-weight: 500;
  margin-bottom: 0.7rem;
}
.section-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(2rem, 4vw, 3rem);
  text-align: center;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 3rem;
}
```

---

## Floral divider

```html
<div class="floral-divider" aria-hidden="true">🌻 ❀ 🌷 ❀ 🌻</div>
```

```css
.floral-divider {
  text-align: center;
  font-size: 2rem;
  padding: 1.5rem 0;
  color: var(--marigold);
  letter-spacing: 0.5rem;
}
```

Vary the emoji combo between dividers: `🌹 ❀ 🌼 ❀ 🌹`, `🌻 ❀ 🌸 ❀ 🌻`, etc.

---

## Responsive breakpoint

```css
@media (max-width: 600px) {
  /* timeline adjustments */
  .timeline::before { left: 22px; }
  .tl-item, .tl-item:nth-child(even) { flex-direction: row; }
  .tl-dot { width: 38px; height: 38px; font-size: 1rem; }
  /* card adjustments */
  .wish-section { padding: 2.5rem 1.5rem; }
  .counter-box { min-width: 70px; padding: 0.75rem 1rem; }
}
```
