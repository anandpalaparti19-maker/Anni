# Hero Section & Anniversary Counter Reference

## Hero HTML

```html
<div class="hero">
  <div class="hero-wreath">🌸</div>
  <p class="hero-wish">Happy Anniversary</p>
  <h1 class="hero-names">
    Govardhan<br><span class="amp">&amp;</span><br>Swapna
  </h1>
  <p class="hero-date">Married on 23 · May · 2021</p>

  <div class="counter-row" id="counter" aria-label="Years, months and days since wedding"></div>

  <p class="scroll-hint">↓ scroll to celebrate ↓</p>
</div>
```

Adapt `.hero-wish` text to the occasion:
- Anniversary → "Happy Anniversary"
- Birthday → "Happy Birthday"
- Wedding → "Congratulations"
- Baby shower → "A New Chapter Begins"

## Hero CSS

```css
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 4rem 2rem;
  background: radial-gradient(ellipse 80% 70% at 50% 30%, #fff3dc 0%, var(--cream) 100%);
  overflow: hidden;
  z-index: 1;
}

.hero-wreath {
  font-size: clamp(3rem, 8vw, 5.5rem);
  line-height: 1;
  margin-bottom: 0.5rem;
  animation: sway 3s ease-in-out infinite alternate;
}

.hero-wish {
  font-size: clamp(0.85rem, 2vw, 1rem);
  letter-spacing: 0.35em;
  text-transform: uppercase;
  color: var(--rose);
  font-weight: 500;
  margin-bottom: 1.2rem;
}

.hero-names {
  font-family: 'Playfair Display', serif;
  font-size: clamp(3rem, 9vw, 6.5rem);
  font-weight: 700;
  line-height: 1.05;
  color: var(--text);
}

.hero-names .amp {
  font-style: italic;
  color: var(--rose);
}

.hero-date {
  margin-top: 1.5rem;
  font-size: clamp(0.85rem, 1.5vw, 1rem);
  letter-spacing: 0.2em;
  color: var(--muted);
  text-transform: uppercase;
}

.scroll-hint {
  margin-top: 3.5rem;
  color: var(--muted);
  font-size: 0.8rem;
  letter-spacing: 0.1em;
  animation: bounce 2s ease-in-out infinite;
}
```

## Counter boxes CSS

```css
.counter-row {
  display: flex;
  gap: 1.5rem;
  margin-top: 2.5rem;
  justify-content: center;
  flex-wrap: wrap;
}
.counter-box {
  background: #fff;
  border: 2px solid var(--rose-lt);
  border-radius: 16px;
  padding: 1rem 1.5rem;
  min-width: 90px;
  text-align: center;
  box-shadow: 0 4px 20px rgba(232,85,106,0.08);
}
.counter-num {
  font-family: 'Playfair Display', serif;
  font-size: 2.4rem;
  font-weight: 700;
  color: var(--rose);
  line-height: 1;
}
.counter-label {
  font-size: 0.72rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
  margin-top: 4px;
}
```

## Counter JS

```js
function updateCounter() {
  const wed = new Date('2021-05-23'); // ← update to wedding/event date
  const now = new Date();
  let years  = now.getFullYear() - wed.getFullYear();
  let months = now.getMonth()    - wed.getMonth();
  let days   = now.getDate()     - wed.getDate();
  if (days < 0)   { months--; const prev = new Date(now.getFullYear(), now.getMonth(), 0); days += prev.getDate(); }
  if (months < 0) { years--; months += 12; }
  const boxes = [
    { num: years,  label: 'Years'  },
    { num: months, label: 'Months' },
    { num: days,   label: 'Days'   },
  ];
  const el = document.getElementById('counter');
  el.innerHTML = boxes.map(b => `
    <div class="counter-box">
      <div class="counter-num">${b.num}</div>
      <div class="counter-label">${b.label}</div>
    </div>`).join('');
}
updateCounter();
```

### Counter variants

For a **birthday**, count years of age instead:

```js
const born = new Date('1990-06-15');
const age  = now.getFullYear() - born.getFullYear()
           - (now < new Date(now.getFullYear(), born.getMonth(), born.getDate()) ? 1 : 0);
// Show single box: "32 Years"
```

For a **days-since** counter only:

```js
const diff = Math.floor((now - eventDate) / (1000 * 60 * 60 * 24));
// Show single box: "1234 Days Together"
```
