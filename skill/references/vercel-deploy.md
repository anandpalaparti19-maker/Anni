# Vercel Deployment Reference

Standard deployment guide to embed in every celebration website README.

## vercel.json (always include)

```json
{
  "cleanUrls": true,
  "trailingSlash": false,
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Cache-Control", "value": "public, max-age=3600" }
      ]
    }
  ]
}
```

## README deployment section (copy-paste into project README)

```markdown
## 🚀 Deploying to Vercel (Free Hosting)

### Option A — Drag & Drop (Easiest, no account needed)

1. Go to **https://vercel.com/new**
2. Click **"Deploy without Git"** → drag the entire project folder onto the page.
3. Vercel gives you a free URL like `https://your-site.vercel.app` in ~30 seconds!

### Option B — Vercel CLI

\`\`\`bash
npm install -g vercel
cd your-project-folder
vercel
# Follow the prompts — choose defaults
\`\`\`

### Option C — GitHub (Best for updates)

1. Push this folder to a GitHub repo.
2. Go to **vercel.com → New Project → Import Git Repository**.
3. Select your repo — Vercel auto-deploys every time you push changes.
```

## Adding photos after deployment

If the user adds photos after deploying, they need to redeploy:
- **Drag & Drop**: repeat the drag-and-drop with the updated folder
- **CLI**: run `vercel --prod` from the project folder again
- **GitHub**: commit and push — Vercel auto-deploys

## Custom domain (optional)

Vercel free tier supports one free `.vercel.app` subdomain. Custom domains (e.g. `govardhan-swapna.com`) cost ~$10-20/yr from a registrar like Namecheap, then can be pointed to Vercel for free.

## Alternatives to Vercel

| Platform | Free tier | Ease |
|---|---|---|
| Vercel | ✅ Unlimited | ⭐⭐⭐ Easiest |
| Netlify | ✅ 100GB/month | ⭐⭐⭐ Also very easy |
| GitHub Pages | ✅ Unlimited | ⭐⭐ Needs GitHub account |
| Cloudflare Pages | ✅ Unlimited | ⭐⭐ Good for scale |

For celebration sites (low traffic, one-time use), Vercel is the recommended default.
