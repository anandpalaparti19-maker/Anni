# Timeline / Journey Section Reference

A visual vertical timeline of milestone moments, centered on the page with an alternating left/right layout on desktop and a single-column layout on mobile.

## HTML

```html
<section id="journey">
  <p class="section-eyebrow reveal">Your journey</p>
  <h2 class="section-title reveal">Four Years of Love</h2>

  <div class="timeline">

    <div class="tl-item reveal">
      <div class="tl-dot">💍</div>
      <div class="tl-content">
        <p class="tl-year">23 May 2021</p>
        <p class="tl-desc">The day two lives became one beautiful story.</p>
      </div>
    </div>

    <div class="tl-item reveal">
      <div class="tl-dot">🏡</div>
      <div class="tl-content">
        <p class="tl-year">Year One</p>
        <p class="tl-desc">Learning each other's worlds and building a cozy home.</p>
      </div>
    </div>

    <!-- Add more .tl-item blocks as needed -->

    <div class="tl-item reveal">
      <div class="tl-dot">🌸</div>
      <div class="tl-content">
        <p class="tl-year">Today — Year Four!</p>
        <p class="tl-desc">Still growing, still glowing — Happy Anniversary! 🎉</p>
      </div>
    </div>

  </div>
</section>
```

## CSS

```css
.timeline {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
}

/* Vertical center line */
.timeline::before {
  content: '';
  position: absolute;
  left: 50%;
  top: 0; bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom, var(--rose-lt), var(--marigold), var(--rose-lt));
  transform: translateX(-50%);
}

.tl-item {
  display: flex;
  align-items: flex-start;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
  position: relative;
}

/* Alternate sides */
.tl-item:nth-child(even) { flex-direction: row-reverse; }

.tl-dot {
  flex-shrink: 0;
  width: 44px; height: 44px;
  border-radius: 50%;
  background: var(--rose);
  display: flex; align-items: center; justify-content: center;
  font-size: 1.3rem;
  box-shadow: 0 0 0 6px var(--rose-lt);
  z-index: 1;
}

.tl-content {
  background: #fff;
  border-radius: 16px;
  padding: 1rem 1.25rem;
  box-shadow: 0 4px 20px rgba(44,26,18,0.07);
  flex: 1;
}

.tl-year {
  font-family: 'Playfair Display', serif;
  font-size: 1.3rem;
  color: var(--rose);
  font-weight: 700;
}

.tl-desc {
  font-size: 0.88rem;
  color: var(--muted);
  margin-top: 0.25rem;
}

/* Mobile: single column, dot on the left */
@media (max-width: 600px) {
  .timeline::before { left: 22px; }
  .tl-item, .tl-item:nth-child(even) { flex-direction: row; }
  .tl-dot { width: 38px; height: 38px; font-size: 1rem; }
}
```

## Milestone content guidelines

### Anniversary milestones
| Year | Emoji | Label | Description idea |
|---|---|---|---|
| Wedding day | 💍 | `23 May 2021` | "The day two lives became one beautiful story." |
| Year 1 | 🏡 | `Year One` | "Learning each other's worlds and building a cozy home." |
| Year 2 | 🌿 | `Year Two` | "Adventures, little rituals, and growing roots together." |
| Year 3 | 🌟 | `Year Three` | "Deeper bonds, shared dreams, and a thousand small joys." |
| Year 4 | 🌸 | `Today — Year Four!` | "Still growing, still glowing — Happy Anniversary! 🎉" |

### Birthday milestones (example)
| Milestone | Emoji | Description idea |
|---|---|---|
| Birth | 🌟 | "A star entered the world." |
| Childhood | 🎨 | "Creative, curious, and full of wonder." |
| School years | 📚 | "Growing, learning, making memories." |
| Today | 🎂 | "Here you are — remarkable as ever." |

### Rules
- Keep `.tl-desc` to 1–2 short sentences
- `.tl-year` can be a real date or a label like "Year One"
- Emoji in `.tl-dot` should feel thematically matched to the milestone
- Always end with a "Today / Now" milestone as the final item
- Aim for 4–6 items total — enough to tell a story, not overwhelming
