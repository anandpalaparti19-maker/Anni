# Gallery — Heart Double-Tap & Swipe Deck Reference

The gallery section lives at the **bottom** of the page, wrapped in a `div#gallery-section` that starts hidden and is revealed during the intro transition. It has two states:

1. **Heart stage** — a centered outlined heart with "Double Tap" text
2. **Swipe deck** — Tinder-style stacked photo cards, shown after double-tap

## HTML structure

```html
<!-- Outer wrapper: hidden on load, revealed by intro transition -->
<div id="gallery-section" style="display:none; position:relative; z-index:1;">
  <div class="floral-divider" aria-hidden="true">🌹 ❀ 🌼 ❀ 🌹</div>
  <section id="gallery" style="max-width:1100px; margin:0 auto; padding:4rem 2rem;">

    <p class="section-eyebrow reveal">Cherished moments</p>
    <h2 class="section-title reveal">Your Beautiful Story</h2>

    <!-- State 1: Heart -->
    <div class="heart-stage" id="heart-stage">
      <div class="heart-wrapper" id="heartBtn" aria-label="Double tap to open photos">
        <svg class="heart-svg" viewBox="0 0 100 90" xmlns="http://www.w3.org/2000/svg">
          <path class="heart-outline" d="M50 85 C50 85 5 55 5 28 C5 14 16 5 28 5 C36 5 44 10 50 18 C56 10 64 5 72 5 C84 5 95 14 95 28 C95 55 50 85 50 85 Z"/>
        </svg>
        <div class="heart-label" id="heartLabel">Double Tap</div>
      </div>
      <p class="heart-hint">double tap the heart to reveal</p>
    </div>

    <!-- State 2: Swipe deck -->
    <div id="swipe-deck">
      <p class="deck-title">Swipe through your memories 💛</p>
      <div class="swipe-stack" id="swipeStack"></div>
      <div class="swipe-hints">
        <span>👈 swipe left</span>
        <span>swipe right 👉</span>
      </div>
      <div class="deck-done" id="deckDone">
        <div class="done-emoji">🌸</div>
        <p>Every photo, a beautiful memory!</p>
        <button class="deck-replay" onclick="resetDeck()">Replay ↺</button>
      </div>
    </div>

  </section>
</div>
```

## CSS

```css
/* ── Heart stage ── */
.heart-stage {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 3rem 1rem;
  min-height: 340px;
}
.heart-wrapper {
  position: relative;
  width: 180px; height: 170px;
  cursor: pointer;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
}
.heart-svg {
  width: 100%; height: 100%;
  overflow: visible;
  filter: drop-shadow(0 4px 18px rgba(232,85,106,0.15));
  transition: filter 0.4s ease;
}
.heart-outline {
  fill: none;
  stroke: var(--rose);
  stroke-width: 3;
  transition: fill 0.6s ease, stroke 0.4s ease;
}
.heart-wrapper.filled .heart-outline { fill: var(--rose); stroke: var(--rose); }
.heart-wrapper.pulse { animation: heartPulse 0.5s ease; }
@keyframes heartPulse {
  0%   { transform: scale(1); }
  30%  { transform: scale(1.22); }
  60%  { transform: scale(0.95); }
  100% { transform: scale(1); }
}
.heart-wrapper.glow .heart-svg { filter: drop-shadow(0 0 28px rgba(232,85,106,0.6)); }
.heart-label {
  position: absolute;
  inset: 0;
  display: flex; align-items: center; justify-content: center;
  font-size: 0.85rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  color: var(--rose);
  pointer-events: none;
  transition: color 0.5s ease;
}
.heart-wrapper.filled .heart-label { color: #fff; }
.heart-hint { margin-top: 1.2rem; font-size: 0.78rem; color: var(--muted); letter-spacing: 0.08em; }

/* ── Swipe deck ── */
#swipe-deck {
  display: none;
  flex-direction: column;
  align-items: center;
  padding: 2rem 1rem 3rem;
  min-height: 520px;
}
#swipe-deck.active { display: flex; }
.deck-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.4rem;
  color: var(--text);
  margin-bottom: 2rem;
  text-align: center;
}
.swipe-stack {
  position: relative;
  width: min(320px, 88vw);
  height: 420px;
}
.swipe-card {
  position: absolute; inset: 0;
  border-radius: 24px;
  overflow: hidden;
  background: #fff;
  box-shadow: 0 8px 32px rgba(44,26,18,0.13);
  cursor: grab;
  user-select: none; -webkit-user-select: none;
  touch-action: none;
  transition: box-shadow 0.2s ease;
  will-change: transform;
}
.swipe-card:active { cursor: grabbing; }
.swipe-card img { width: 100%; height: 100%; object-fit: cover; display: block; pointer-events: none; }
.swipe-card .sc-caption {
  position: absolute; bottom: 0; left: 0; right: 0;
  padding: 1.2rem 1rem 0.9rem;
  background: linear-gradient(to top, rgba(44,26,18,0.7) 0%, transparent 100%);
  color: #fff; font-style: italic; font-size: 0.88rem; text-align: center;
}
.swipe-card .swipe-indicator {
  position: absolute; top: 1.2rem;
  font-size: 1.8rem; font-weight: 700;
  border: 3px solid; border-radius: 8px;
  padding: 2px 10px; opacity: 0;
  transition: opacity 0.15s ease; pointer-events: none;
}
.swipe-card .ind-like  { left: 1.2rem;  color: #4CAF50; border-color: #4CAF50; }
.swipe-card .ind-nope  { right: 1.2rem; color: var(--rose); border-color: var(--rose); }
.swipe-card.placeholder {
  background: var(--rose-lt);
  display: flex; align-items: center; justify-content: center;
  flex-direction: column; gap: 0.5rem; cursor: default;
}
.swipe-card.placeholder span { font-size: 2rem; }
.swipe-card.placeholder p { color: var(--rose); font-size: 0.88rem; font-weight: 500; text-align: center; padding: 0 1.5rem; }
.swipe-hints { display: flex; gap: 2rem; margin-top: 1.5rem; font-size: 0.78rem; color: var(--muted); letter-spacing: 0.06em; }
.swipe-hints span { display: flex; align-items: center; gap: 0.3rem; }
.deck-done { display: none; flex-direction: column; align-items: center; gap: 1rem; padding: 2rem; text-align: center; }
.deck-done.show { display: flex; }
.deck-done .done-emoji { font-size: 3rem; }
.deck-done p { font-family: 'Playfair Display', serif; font-size: 1.3rem; color: var(--text); font-style: italic; }
.deck-replay {
  margin-top: 0.5rem; padding: 0.65rem 1.8rem;
  border: 2px solid var(--rose); border-radius: 50px;
  background: transparent; color: var(--rose);
  font-size: 0.88rem; cursor: pointer;
  transition: background 0.2s ease, color 0.2s ease;
}
.deck-replay:hover { background: var(--rose); color: #fff; }
```

## JS — Heart double-tap

```js
const heartBtn   = document.getElementById('heartBtn');
const heartStage = document.getElementById('heart-stage');
const swipeDeck  = document.getElementById('swipe-deck');
let lastTap = 0;

function triggerHeartReveal() {
  if (heartBtn.classList.contains('filled')) return;
  heartBtn.classList.add('filled', 'pulse', 'glow');
  document.getElementById('heartLabel').textContent = '♥';
  setTimeout(() => {
    heartStage.style.transition = 'opacity 0.5s ease';
    heartStage.style.opacity = '0';
    setTimeout(() => {
      heartStage.style.display = 'none';
      swipeDeck.classList.add('active');
      buildDeck();
    }, 500);
  }, 800);
}

// Desktop: double-click
heartBtn.addEventListener('dblclick', triggerHeartReveal);
// Mobile: double-tap (two clicks within 350ms)
heartBtn.addEventListener('click', () => {
  const now = Date.now();
  if (now - lastTap < 350) triggerHeartReveal();
  lastTap = now;
});
```

## JS — Swipe deck

```js
// Define photos — update src paths and captions
const photos = [
  { src: 'photos/photo1.jpg', caption: 'The beginning of forever 💛' },
  { src: 'photos/photo2.jpg', caption: 'Together always 🌸' },
  { src: 'photos/photo3.jpg', caption: 'Two hearts, one home 🏡' },
  // { src: 'photos/photo4.jpg', caption: 'Your caption here' },
];

let deckCards = [];

function buildDeck() {
  const stack = document.getElementById('swipeStack');
  stack.innerHTML = '';
  document.getElementById('deckDone').classList.remove('show');
  deckCards = [];

  [...photos].reverse().forEach((photo, ri) => {
    const card = document.createElement('div');
    card.className = 'swipe-card';
    card.style.transform = `scale(${1 - ri * 0.04}) translateY(${ri * 10}px)`;
    card.style.zIndex = photos.length - ri;
    card.style.transition = 'transform 0.3s ease, box-shadow 0.2s ease';

    const img = document.createElement('img');
    img.src = photo.src;
    img.alt = 'Photo';
    img.loading = 'lazy';
    img.onerror = () => {
      card.classList.add('placeholder');
      card.innerHTML = `<span>📷</span><p>${photo.caption}<br><small style="opacity:0.7">Add photo to photos/ folder</small></p>`;
    };
    card.appendChild(img);

    const caption = document.createElement('div');
    caption.className = 'sc-caption';
    caption.textContent = photo.caption;
    card.appendChild(caption);

    ['ind-like ♥', 'ind-nope ✕'].forEach(s => {
      const [cls, txt] = s.split(' ');
      const ind = document.createElement('div');
      ind.className = `swipe-indicator ${cls}`;
      ind.textContent = txt;
      card.appendChild(ind);
    });

    makeDraggable(card);
    stack.appendChild(card);
    deckCards.unshift(card);
  });
}

function makeDraggable(card) {
  let startX, curX = 0, isDragging = false;

  const onStart = x => { startX = x; isDragging = true; card.style.transition = 'none'; };
  const onMove  = x => {
    if (!isDragging) return;
    curX = x - startX;
    card.style.transform = `translateX(${curX}px) rotate(${curX * 0.08}deg)`;
    const r = Math.min(Math.abs(curX) / 80, 1);
    card.querySelector('.ind-like').style.opacity = curX > 0 ? r : 0;
    card.querySelector('.ind-nope').style.opacity = curX < 0 ? r : 0;
  };
  const onEnd = () => {
    if (!isDragging) return;
    isDragging = false;
    card.style.transition = 'transform 0.4s cubic-bezier(0.25,0.46,0.45,0.94), opacity 0.4s ease';
    if (Math.abs(curX) > 90) {
      const dir = curX > 0 ? 1 : -1;
      card.style.transform = `translateX(${dir * 120}vw) rotate(${dir * 30}deg)`;
      card.style.opacity = '0';
      setTimeout(() => {
        card.remove(); deckCards.shift(); updateStackPositions();
        if (deckCards.length === 0) document.getElementById('deckDone').classList.add('show');
      }, 400);
    } else {
      card.style.transform = 'scale(1) translateY(0)';
      curX = 0;
      card.querySelectorAll('.swipe-indicator').forEach(i => i.style.opacity = 0);
      updateStackPositions();
    }
  };

  card.addEventListener('mousedown', e => { e.preventDefault(); onStart(e.clientX); });
  document.addEventListener('mousemove', e => onMove(e.clientX));
  document.addEventListener('mouseup', onEnd);
  card.addEventListener('touchstart', e => onStart(e.touches[0].clientX), { passive: true });
  card.addEventListener('touchmove',  e => { e.preventDefault(); onMove(e.touches[0].clientX); }, { passive: false });
  card.addEventListener('touchend', onEnd);
}

function updateStackPositions() {
  deckCards.forEach((c, i) => {
    c.style.transition = 'transform 0.35s cubic-bezier(0.4,0,0.2,1)';
    c.style.zIndex = deckCards.length - i;
    c.style.transform = i === 0 ? 'scale(1) translateY(0)' : `scale(${1 - i * 0.04}) translateY(${i * 10}px)`;
  });
}

function resetDeck() {
  document.getElementById('deckDone').classList.remove('show');
  buildDeck();
}
```

## Photo management

Tell the user to:
1. Copy photos to the `photos/` folder
2. Name them `photo1.jpg`, `photo2.jpg`, etc. (or any name)
3. Update the `photos` array in the JS with the correct `src` and `caption` for each photo
4. Add as many entries as needed — the deck automatically handles any count

Photos that fail to load (`onerror`) gracefully degrade to a placeholder card with the caption text.
