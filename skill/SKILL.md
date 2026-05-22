---
name: celebration-website
description: Build a beautiful, themed celebration website (anniversary, birthday, wedding, baby shower, etc.) with temporary hosting on Vercel. Use this skill whenever a user wants to create a personal tribute page, a surprise website for someone, a milestone celebration page, a love note website, or any emotionally meaningful single-page site with photos, animations, and a personal message. Trigger this skill even if the user doesn't say "website" explicitly — phrases like "I want to wish my friend", "make something special for", "create a page for our anniversary", or "surprise my partner online" are all strong triggers. Always use this skill for emotionally-driven web pages meant to delight a specific person.
---

# Celebration Website Skill

Build a polished, emotionally resonant single-page celebration website — deployable to Vercel for free — with a warm theme, photo gallery, animations, and personalized content.

## Workflow

### Step 1 — Gather context (ask before building)

Before writing any code, collect:

| Question | Why it matters |
|---|---|
| Names of the people being celebrated | Personalised hero text, footer |
| Occasion (anniversary, birthday, wedding, etc.) | Sets tone, timeline milestones |
| Key date (e.g. wedding date) | Powers the live counter |
| Theme/vibe preference | Drives color palette and animation style |
| Rough photo count | Determines gallery layout approach |
| Personal wish or message | Goes into the "A Little Note" section |

If any are missing after asking once, use sensible defaults and note them clearly in the README.

---

### Step 2 — Design decisions

Commit to a clear aesthetic before writing code. See `references/design-system.md` for the full palette and component guide.

**Theme presets** (pick one or blend):

| Vibe | Primary color | Accent | Mood |
|---|---|---|---|
| Warm & joyful | Marigold `#F4A614` | Rose `#E8556A` | Playful, floral, cheerful |
| Romantic & elegant | Deep rose `#C0395A` | Gold `#D4840A` | Luxurious, intimate |
| Modern & minimal | Slate `#4A5568` | Blush `#F9A8BE` | Clean, chic |
| Tropical & festive | Coral `#FF6B6B` | Teal `#38B2AC` | Energetic, bright |

---

### Step 3 — Build the page

A celebration website has these sections in order:

1. **Intro screen** — full-screen overlay before main page loads (see `references/intro-screen.md`)
2. **Hero** — names, flower/emoji, live anniversary counter (see `references/hero-counter.md`)
3. **Floral dividers** — emoji-based decorative separators
4. **Wish / Love Note** — personalised message card (see `references/wish-card.md`)
5. **Journey / Timeline** — milestone moments as a visual timeline (see `references/timeline.md`)
6. **Footer** — dark background, simple credit line
7. **Gallery** (at the bottom) — heart double-tap → swipe deck interaction (see `references/gallery-swipe.md`)
8. **Lightbox** — full-screen photo viewer overlay
9. **Falling petals** — ambient CSS animation layer (see `references/animations.md`)

**File output rules:**
- Everything in ONE `index.html` — no separate CSS or JS files
- A `photos/` folder with a `.gitkeep` placeholder
- A `vercel.json` for deployment config
- A `README.md` with photo-adding and Vercel deployment instructions

---

### Step 4 — Write the README

Always include deployment instructions. See `references/vercel-deploy.md` for the standard Vercel deployment guide to embed in the README.

---

### Step 5 — Package and present

```bash
zip -r celebration-site.zip <project-folder>/
```

Copy to `/mnt/user-data/outputs/` and call `present_files`.

---

## Key constraints

- **Single file**: all HTML, CSS, and JS in `index.html`. No external files except fonts (Google Fonts CDN) and nothing else.
- **No frameworks**: vanilla HTML/CSS/JS only. No React, no build step.
- **Responsive**: must work on mobile (320px+) and desktop.
- **Accessible**: use semantic HTML, `aria-label` on interactive elements, `role="dialog"` on overlays.
- **No breaking changes**: when making edits, preserve all existing functionality. Read the current file fully before editing.

---

## Reference files

Read these when building the relevant section:

- `references/design-system.md` — CSS variables, color palette, typography, spacing
- `references/animations.md` — Petals, sway, bounce, reveal-on-scroll
- `references/intro-screen.md` — Intro overlay, flower-to-hero transition
- `references/hero-counter.md` — Hero layout, live anniversary counter
- `references/wish-card.md` — Love note / wish card component
- `references/timeline.md` — Journey timeline component
- `references/gallery-swipe.md` — Heart double-tap + Tinder-style swipe deck
- `references/vercel-deploy.md` — Vercel deployment instructions for README
