# How to host the preview & promote it to production

This document covers three things:

1. Running the preview **locally** so you can demo on your own laptop.
2. Sharing the preview with the client over the **internet** without touching the live site.
3. Promoting the preview to **production** once the client signs off (GitHub Pages today, optionally Cloudflare Pages).

The repo lives at `~/Documents/GitHub/see-consultancy`. All commands below assume your terminal is in that folder unless stated otherwise.

```bash
cd ~/Documents/GitHub/see-consultancy
```

---

## 1. Run the preview locally

Because the preview pages link back to vendor assets in the parent folder (e.g. `../css/bootstrap.min.css`, `../js/jquery.min.js`), you must start the server **from the repo root**, not from inside `preview/`. The URL you open just points at `/preview/`.

### Option A — Python (zero install on macOS)

```bash
cd ~/Documents/GitHub/see-consultancy
python3 -m http.server 8000
```

Then open: **http://localhost:8000/preview/**

To stop: `Ctrl + C`.

### Option B — Node "serve" (nicer UI)

```bash
# one-time install
npm install -g serve

# from repo root
cd ~/Documents/GitHub/see-consultancy
serve -p 8000 .
```

Open **http://localhost:8000/preview/**.

### Option C — VS Code "Live Server"

1. Open the repo folder in VS Code.
2. Install the *Live Server* extension (Ritwick Dey).
3. Right-click `preview/index.html` → **Open with Live Server**.
4. It auto-reloads on save, which is handy while iterating.

### Pages to walk the client through

| URL | What it shows |
|---|---|
| `/preview/index.html` | New home — hero, About SEE, What we do, capability grid, CTA |
| `/preview/about.html` | Story, Clients grid, 3-person team, Approach, 3 testimonials |
| `/preview/services.html` | 12 consultancy cards + 6 training cards |
| `/preview/expertise.html` | **NEW** page — 9 expertise pillars |
| `/preview/contact.html` | Email/LinkedIn cards, contact form, "Why choose us" panel |
| `/preview/privacy-policy.html` | Refreshed privacy page |
| `/preview/terms-of-service.html` | Refreshed terms page |
| `/preview/404.html` | New 404 page |

---

## 2. Share the preview with the client (without breaking production)

Pick whichever route fits how you usually share work.

### 2a. ngrok / Cloudflare Tunnel — quickest

Run the local server (Option A above) and expose it:

```bash
# Cloudflare option (no signup, no token for short sessions)
brew install cloudflared
cloudflared tunnel --url http://localhost:8000
```

Cloudflare prints a public URL like `https://random-name.trycloudflare.com`. Send the client `https://random-name.trycloudflare.com/preview/`. The tunnel dies when you `Ctrl + C` — ideal for a one-off review call.

### 2b. GitHub Pages — preview branch (Recommended for written feedback)

This keeps the live `see-energy.co.uk` site **untouched** while exposing the preview at a separate URL.

```bash
git checkout -b preview/revamp-2026
git add preview/ DESIGN_CHANGES.md   # if you also moved the design doc
git commit -m "Preview: 2026 site revamp"
git push -u origin preview/revamp-2026
```

Then in GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `preview/revamp-2026` / `(root)` → Save.**

It will publish to `https://<your-username>.github.io/see-consultancy/preview/` (or to the same custom domain *if* the CNAME file is on that branch — make sure it isn't, or you'll move the live site). The live site keeps building from `main` and `see-energy.co.uk` is unaffected.

Send the client the GitHub Pages URL → `…/preview/index.html`.

### 2c. Cloudflare Pages — preview project (Recommended if you're moving to Cloudflare anyway)

If you already plan to switch hosting to Cloudflare, set up a *separate* Pages project for the preview now — it doubles as a free staging environment forever.

```bash
# one-time
npm install -g wrangler
wrangler login
```

Then in the Cloudflare dashboard:

1. **Workers & Pages → Create → Pages → Connect to Git → see-consultancy**.
2. Production branch: `preview/revamp-2026`.
3. **Build command:** *(leave blank — static site)*.
4. **Build output directory:** `/` (or `preview` if you only want the preview folder served at the root URL).
5. Deploy.

You'll get `https://see-consultancy-preview.pages.dev/preview/`. Every push to `preview/revamp-2026` redeploys automatically. You can also add a custom subdomain like `preview.see-energy.co.uk` later (Pages → Custom domains).

---

## 3. Promote to production once the client signs off

### 3a. If you stay on GitHub Pages

```bash
# 1. Make sure your preview branch is up to date with main
git checkout preview/revamp-2026
git pull --rebase origin main

# 2. Move the new files to the root
mv -f preview/index.html              index.html
mv -f preview/about.html              about.html
mv -f preview/services.html           services.html
mv -f preview/expertise.html          expertise.html
mv -f preview/contact.html            contact.html
mv -f preview/privacy-policy.html     privacy-policy.html
mv -f preview/terms-of-service.html   terms-of-service.html
mv -f preview/404.html                404.html
mv -f preview/css/see-theme.css       css/see-theme.css

# 3. The promoted files use ../ paths — fix them so they resolve from the root.
#    macOS sed (BSD) needs an empty string after -i.
for f in index.html about.html services.html expertise.html contact.html privacy-policy.html terms-of-service.html 404.html; do
  sed -i '' \
    -e 's|href="\.\./|href="|g' \
    -e 's|src="\.\./|src="|g' \
    -e 's|href="css/see-theme.css"|href="css/see-theme.css"|g' \
    "$f"
done

# 4. Delete the now-empty preview/ scaffold
rm -rf preview

# 5. Update the sitemap to include /expertise.html and bump <lastmod>
#    (open sitemap.xml and add the new URL block)

# 6. Merge into main
git add -A
git commit -m "Revamp 2026: new content, palette, expertise page"
git checkout main
git merge --no-ff preview/revamp-2026
git push origin main
```

GitHub Pages picks up the change in ~1-2 minutes.

### 3b. If you switch to Cloudflare Pages

You can do this **without** taking down GitHub Pages. The DNS cutover is the only "moment of truth."

1. **Create the production Pages project** in Cloudflare → connect repo → production branch `main`, output dir `/`.
2. Verify the temporary `*.pages.dev` URL renders correctly.
3. **Pages → Custom domains → Set up custom domain → `see-energy.co.uk`** + `www.see-energy.co.uk`.
   - Cloudflare will tell you what DNS records to add. If the domain is already on Cloudflare DNS it does it automatically; otherwise update your DNS provider with the CNAME values it provides.
4. Wait for SSL certificate to provision (a few minutes).
5. Once `https://see-energy.co.uk` resolves to Cloudflare and looks correct, **disable GitHub Pages** for the repo (Settings → Pages → Source → None) so requests don't race.
6. Cloudflare Pages auto-deploys on every `git push`.

#### Why move to Cloudflare?

- Faster global CDN, automatic HTTP/3 and Brotli.
- Free SSL, free analytics, free preview deployments per branch.
- You can stop committing the `CNAME` file (Cloudflare manages the domain mapping in the dashboard, not via that file).

---

## 4. Quick troubleshooting

| Symptom | Cause / fix |
|---|---|
| "Page loads but no styling" | You started `python3 -m http.server` from inside `preview/` — restart it from the **repo root** so `../css/...` resolves. |
| Hero image not showing | The hero pulls from Unsplash by URL; you need internet. Replace with a local image once the client picks one. |
| Contact form errors | Form posts to `https://formspree.io/f/your-id` placeholder. Swap in your real Formspree (or other) endpoint, or wire it into the existing `js/contact.js` handler the live site uses. |
| Old logo too small / blurry | We're still using `favicon/header-logo.png`. Drop in a higher-res transparent PNG or SVG at the same path. |
| Cloudflare tunnel keeps disconnecting | Use `cloudflared tunnel --url http://localhost:8000 --no-autoupdate` and keep your laptop awake; or use ngrok with an account for longer sessions. |

---

## 5. Checklist before promoting to production

- [ ] Client has signed off on copy on every page.
- [ ] All three team headshots replaced (currently initials placeholders).
- [ ] Hero image replaced with a licensed image.
- [ ] Contact form endpoint pointed at the real handler.
- [ ] `sitemap.xml` updated to include `/expertise.html` and bumped dates.
- [ ] `robots.txt` reviewed (no change required, but worth a glance).
- [ ] Logo and favicon refreshed if a new asset has been supplied.
- [ ] Run `python3 -m http.server` from repo root one last time and click every nav link.
