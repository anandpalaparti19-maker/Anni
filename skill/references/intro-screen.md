# Intro Screen Reference

A full-screen overlay that greets the visitor before revealing the main page. Uses the same flower emoji as the hero, animated from center-screen to its final hero position on click.

## HTML structure

Place this as the **first child of `<body>`**, before all other content.

```html
<!-- Intro screen -->
<div id="intro-screen" role="dialog" aria-label="Welcome screen">
  <div id="intro-flower">🌸</div>
  <p id="intro-msg">Something special below</p>
  <button id="intro-btn" onclick="startIntroTransition()">Click Me</button>
</div>

<!-- Main content wrapper — hidden until intro completes -->
<div id="main-content">
  <!-- ... all page content ... -->
</div>
```

## CSS

```css
/* Intro overlay */
#intro-screen {
  position: fixed; inset: 0;
  z-index: 9000;
  background: radial-gradient(ellipse 80% 70% at 50% 40%, #fff3dc 0%, var(--cream) 100%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 2rem;
  transition: opacity 0.8s ease, transform 0.8s ease;
}
#intro-screen.fade-out {
  opacity: 0;
  pointer-events: none;
}

/* Intro flower — large, centered, then animates to hero position */
#intro-flower {
  font-size: clamp(5rem, 15vw, 9rem);
  line-height: 1;
  animation: sway 3s ease-in-out infinite alternate;
  transform-origin: center bottom;
  transition: font-size 0.7s cubic-bezier(0.4,0,0.2,1),
              transform 0.7s cubic-bezier(0.4,0,0.2,1),
              opacity 0.3s ease 0.55s;
  will-change: font-size, margin;
}

/* Message + button */
#intro-msg {
  margin-top: 1.5rem;
  font-family: 'Playfair Display', serif;
  font-size: clamp(1.2rem, 3vw, 1.7rem);
  font-style: italic;
  color: var(--muted);
  transition: opacity 0.4s ease;
}
#intro-btn {
  margin-top: 2rem;
  padding: 0.85rem 2.5rem;
  border: 2.5px solid var(--rose);
  border-radius: 50px;
  background: transparent;
  color: var(--rose);
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  cursor: pointer;
  transition: background 0.25s ease, color 0.25s ease, transform 0.15s ease, opacity 0.4s ease;
}
#intro-btn:hover { background: var(--rose); color: #fff; transform: scale(1.04); }
#intro-btn:active { transform: scale(0.97); }

/* Main page hidden until intro done */
#main-content { opacity: 0; transition: opacity 0.7s ease 0.2s; }
#main-content.visible { opacity: 1; }
```

## JS — transition logic

```js
function startIntroTransition() {
  const introFlower = document.getElementById('intro-flower');
  const introMsg    = document.getElementById('intro-msg');
  const introBtn    = document.getElementById('intro-btn');
  const introScreen = document.getElementById('intro-screen');
  const mainContent = document.getElementById('main-content');
  const heroWreath  = document.querySelector('.hero-wreath');

  // Step 1: fade out text & button
  introMsg.style.opacity = '0';
  introBtn.style.opacity = '0';
  introBtn.style.pointerEvents = 'none';

  // Step 2: measure positions for FLIP animation
  const targetRect = heroWreath.getBoundingClientRect();
  const flowerRect = introFlower.getBoundingClientRect();
  const scaleRatio = targetRect.width / flowerRect.width;

  // Step 3: animate intro flower to hero-wreath position
  introFlower.style.transition = 'font-size 0.75s cubic-bezier(0.4,0,0.2,1), transform 0.75s cubic-bezier(0.4,0,0.2,1), opacity 0.3s ease 0.55s';
  const dx = targetRect.left - flowerRect.left + (targetRect.width - flowerRect.width) / 2;
  const dy = targetRect.top  - flowerRect.top  + (targetRect.height - flowerRect.height) / 2;
  introFlower.style.transform = `translate(${dx}px, ${dy}px) scale(${scaleRatio})`;
  introFlower.style.opacity = '0';

  // Step 4: reveal main page, then remove intro overlay
  setTimeout(() => {
    mainContent.classList.add('visible');
    // Show any sections that were hidden (e.g. gallery)
    document.getElementById('gallery-section').style.display = 'block';
    setTimeout(() => {
      introScreen.classList.add('fade-out');
      setTimeout(() => {
        introScreen.style.display = 'none';
        // Re-trigger scroll reveal for newly visible elements
        document.querySelectorAll('.reveal:not(.visible)').forEach(el => obs.observe(el));
      }, 850);
    }, 100);
  }, 400);
}
```

## Notes

- The `obs` variable (IntersectionObserver) must be declared before `startIntroTransition` is called — define it at script init time.
- `gallery-section` is a `<div>` wrapper around the gallery `<section>`, set to `display:none` initially, revealed during transition. Adjust the ID if you use a different name.
- The flower emoji used in `#intro-flower` must match `.hero-wreath` exactly so the visual continuity is seamless.
- The FLIP technique (measuring `getBoundingClientRect()` before and after, then animating the delta) requires the hero to already be rendered in the DOM — which it is, since it's inside `#main-content` even when opacity:0.
