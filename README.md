# 🌸 Govardhan & Swapna — Anniversary Website

A warm, joyful anniversary website with a floral theme, photo gallery, and love counter.

---

## 📁 File Structure

```
anniversary-site/
├── index.html        ← Main website file
├── vercel.json       ← Vercel deployment config
├── photos/           ← Put ALL your photos here
│   ├── photo1.jpg
│   ├── photo2.jpg
│   └── ...
└── README.md
```

---

## 🖼️ Adding Photos

1. Copy your photos into the `photos/` folder.
2. Name them: `photo1.jpg`, `photo2.jpg`, `photo3.jpg` etc. (or any name you like).
3. Open `index.html` and find the **Gallery section** (look for `<!-- GALLERY -->`).
4. For each photo, add or update a card block:

```html
<div class="photo-card reveal" onclick="openLightbox(this)">
  <img src="photos/YOUR_PHOTO_NAME.jpg" alt="Govardhan and Swapna" loading="lazy" />
  <p class="photo-caption">Your caption here 💛</p>
</div>
```

5. Remove the placeholder "upload" card once you have your photos in place.

---

## 🚀 Deploying to Vercel (Free Hosting)

### Option A — Drag & Drop (Easiest, no account needed)

1. Go to **https://vercel.com/new**
2. Click **"Deploy without Git"** → drag the entire `anniversary-site` folder onto the page.
3. Vercel gives you a free URL like `https://anniversary-xyz.vercel.app` in ~30 seconds!

### Option B — Vercel CLI

```bash
npm install -g vercel
cd anniversary-site
vercel
# Follow the prompts — choose defaults
```

### Option C — GitHub (Best for updates)

1. Push this folder to a GitHub repo.
2. Go to **vercel.com → New Project → Import Git Repository**.
3. Select your repo — Vercel auto-deploys every time you push changes.

---

## ✏️ Personalising Further

| What                       | Where in index.html                        |
|----------------------------|--------------------------------------------|
| Wish message               | Look for `wish-quote` section              |
| Timeline milestones        | Look for `tl-item` blocks in `#journey`   |
| Petal count / speed        | `const container` script block at bottom  |
| Background colours         | `:root` CSS variables at the top           |

---

Made with 💛 — Happy Anniversary Govardhan & Swapna!
