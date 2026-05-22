# Animations Reference

## 1. Falling petals (ambient background)

A fixed-position layer of colored organic shapes that fall continuously. Always present, never obstructs interaction (`pointer-events: none`).

### CSS

```css
.petal-layer {
  position: fixed; inset: 0;
  pointer-events: none;
  z-index: 0;
  overflow: hidden;
}
.petal {
  position: absolute;
  top: -60px;
  width: 18px; height: 22px;
  border-radius: 60% 40% 60% 40% / 60% 40% 60% 40%;
  opacity: 0;
  animation: fall linear infinite;
}
@keyframes fall {
  0%   { transform: translateY(0) rotate(0deg); opacity: 0.85; }
  80%  { opacity: 0.7; }
  100% { transform: translateY(110vh) rotate(480deg); opacity: 0; }
}
```

### HTML

```html
<div class="petal-layer" id="petals" aria-hidden="true"></div>
```

### JS — spawn petals

```js
const petalColors = ['#F4A614','#E8556A','#F9C74F','#F8A5B0','#6B9E6C','#FFCBA4'];
const container = document.getElementById('petals');
for (let i = 0; i < 28; i++) {
  const p = document.createElement('div');
  p.className = 'petal';
  p.style.left = Math.random() * 100 + 'vw';
  p.style.background = petalColors[Math.floor(Math.random() * petalColors.length)];
  p.style.width  = (12 + Math.random() * 14) + 'px';
  p.style.height = (16 + Math.random() * 18) + 'px';
  p.style.animationDuration = (6 + Math.random() * 10) + 's';
  p.style.animationDelay   = (Math.random() * 12) + 's';
  p.style.borderRadius = Math.random() > 0.5
    ? '60% 40% 60% 40% / 60% 40% 60% 40%'
    : '40% 60% 40% 60% / 40% 60% 40% 60%';
  container.appendChild(p);
}
```

Adjust count (`28`) and color array per theme.

---

## 2. Sway animation

Used on hero flowers/emoji and intro screen flower.

```css
@keyframes sway {
  from { transform: rotate(-3deg); }
  to   { transform: rotate(3deg); }
}
.hero-wreath {
  animation: sway 3s ease-in-out infinite alternate;
}
```

---

## 3. Bounce animation

Used on scroll hint arrow.

```css
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50%       { transform: translateY(8px); }
}
.scroll-hint {
  animation: bounce 2s ease-in-out infinite;
}
```

---

## 4. Scroll reveal

Elements fade + slide up when they enter the viewport. Add `.reveal` class to any element, the JS observer handles the rest.

### CSS

```css
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

### JS

```js
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      obs.unobserve(e.target);
    }
  });
}, { threshold: 0.15 });
document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
```

**Important**: when sections are hidden (e.g. gallery behind intro screen), re-run `obs.observe()` on newly visible `.reveal` elements after they appear:

```js
document.querySelectorAll('.reveal:not(.visible)').forEach(el => obs.observe(el));
```

---

## 5. Heart pulse + glow (gallery trigger)

```css
.heart-wrapper.pulse { animation: heartPulse 0.5s ease; }
@keyframes heartPulse {
  0%   { transform: scale(1); }
  30%  { transform: scale(1.22); }
  60%  { transform: scale(0.95); }
  100% { transform: scale(1); }
}
.heart-wrapper.glow .heart-svg {
  filter: drop-shadow(0 0 28px rgba(232,85,106,0.6));
}
```

Trigger by adding both classes to the wrapper element on double-tap.
