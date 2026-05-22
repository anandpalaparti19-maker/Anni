# Wish Card / Love Note Reference

A warm, decorated card containing a personalised message for the couple or person being celebrated.

## HTML

```html
<section id="wish">
  <p class="section-eyebrow reveal">With all our love</p>
  <h2 class="section-title reveal">A Little Note</h2>

  <div class="wish-section reveal">
    <p class="wish-quote">
      "Govardhan &amp; Swapna — four beautiful years of choosing each other,
      every single day. May your love keep blooming brighter,
      your laughter grow louder, and your life together
      <span>sweeter with every passing season.</span>
      Here's to a lifetime more! 🥂"
    </p>
    <p class="wish-sig">— With love &amp; warmest wishes 💛</p>
  </div>
</section>
```

The `<span>` inside `.wish-quote` gets colored via CSS to highlight a key phrase.

## CSS

```css
.wish-section {
  background: linear-gradient(135deg, #FFF3DC 0%, #FDEEF0 100%);
  border-radius: 32px;
  padding: 4rem 3rem;
  text-align: center;
  max-width: 780px;
  margin: 0 auto;
  border: 1.5px solid #F9D9C3;
  position: relative;
  overflow: hidden;
}

/* Decorative large emoji watermarks */
.wish-section::before,
.wish-section::after {
  content: '🌸';
  position: absolute;
  font-size: 6rem;
  opacity: 0.12;
}
.wish-section::before { top: -20px; left: -20px; }
.wish-section::after  { bottom: -20px; right: -20px; }

.wish-quote {
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.3rem, 3vw, 1.9rem);
  font-style: italic;
  color: var(--text);
  line-height: 1.7;
  margin-bottom: 2rem;
}
.wish-quote span { color: var(--rose); }

.wish-sig {
  font-size: 0.85rem;
  color: var(--muted);
  letter-spacing: 0.05em;
}
```

## Writing the wish message

Guidelines for a great wish:
- Open by addressing the couple/person by name
- Reference how long they've been together or a specific milestone
- Use warm, specific imagery (blooming, growing, seasons) that matches the floral theme
- End with a toast or forward-looking phrase
- Keep it 3–5 sentences — readable in one glance
- Sign off with "— With love" or the gift-giver's name if known

### Template

```
"[Name(s)] — [X] beautiful years of [verb phrase]. 
May your [quality] keep [action], 
your [quality] grow [direction], and your [shared thing]
[positive outcome]. Here's to [forward phrase]! [emoji]"
```

### Example (anniversary, 4 years)

```
"Govardhan & Swapna — four beautiful years of choosing each other,
every single day. May your love keep blooming brighter,
your laughter grow louder, and your life together
sweeter with every passing season. Here's to a lifetime more! 🥂"
```

### Example (birthday)

```
"Priya — another year wiser, warmer, and more wonderful than ever.
May this new chapter bring you everything you've been dreaming of,
surrounded by the people who love you most. Happy Birthday! 🎂"
```
