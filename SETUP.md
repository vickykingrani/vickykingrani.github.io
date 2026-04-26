# Setup guide — Live portfolio at https://vickykingrani.github.io

Total time: ~20 min. Total cost: £0/month forever.

---

## What you'll have when done

- Live portfolio at **https://vickykingrani.github.io**
- Updates: edit a file, run `git push` → live in ~1 minute
- Analytics dashboard showing per-slide views, dwell time, TOC clicks, country / browser breakdowns
- Belt-and-braces analytics: Cloudflare (always works) + Umami (rich per-slide events)

---

## Part 1 — Sign up for analytics (5 min)

You're adding TWO trackers so you have firewall-resilient coverage. Both are free.

### A) Umami Cloud — per-slide event tracking

1. Go to **[cloud.umami.is](https://cloud.umami.is)** and sign up (free).
2. Click **"Add website"**.
3. Fill in:
   - Name: `Vicky Kingrani Portfolio`
   - Domain: `vickykingrani.github.io`
4. Click **"Save"**.
5. Click the menu (`···`) on your new website → **"Edit"**.
6. Copy the **"Website ID"** (UUID format like `abcd1234-...`).

### B) Cloudflare Web Analytics — page-level fallback

1. Go to **[one.dash.cloudflare.com](https://one.dash.cloudflare.com)** and sign up (free).
2. Left sidebar → **"Analytics & Logs"** → **"Web Analytics"**.
3. Click **"Add a site"** (free option, doesn't require domain in Cloudflare).
4. Hostname: `vickykingrani.github.io`
5. After saving, you'll see a JS snippet. **Copy just the token** — it's the JSON object inside `data-cf-beacon='{...}'`.

---

## Part 2 — Paste your analytics IDs into `index.html` (2 min)

1. Open `_deploy/index.html` in any text editor (Notepad, VS Code, anything).
2. Find this line near the top:
   ```html
   <script defer src="https://cloud.umami.is/script.js" data-website-id="YOUR_UMAMI_WEBSITE_ID"></script>
   ```
   Replace `YOUR_UMAMI_WEBSITE_ID` with your Umami Website ID from Part 1A.

3. Find this line near the bottom (just before `</body>`):
   ```html
   <script defer src='https://static.cloudflareinsights.com/beacon.min.js' data-cf-beacon='{"token": "YOUR_CLOUDFLARE_TOKEN"}'></script>
   ```
   Replace `YOUR_CLOUDFLARE_TOKEN` with your Cloudflare token from Part 1B.

4. Save.

---

## Part 3 — Push to GitHub Pages (10 min)

You already have a GitHub account: **github.com/vickykingrani** ✓

### Create the repo

1. Go to **[github.com/new](https://github.com/new)**.
2. Repository name: **`vickykingrani.github.io`** (must match your username exactly — this is the special name that makes it live at username.github.io).
3. **Public** (required for free GitHub Pages).
4. Don't tick "Add a README" or ".gitignore" — we have our own.
5. Click **"Create repository"**.

### Upload the files

You have two options:

**Option A — Web upload (easiest, no terminal)**

1. On the new empty repo page, click **"uploading an existing file"** link (or drag-drop area).
2. **Drag the entire contents of `D:\Work\Portfolio\_deploy\` onto the page** — make sure to drag the FILES INSIDE _deploy, not the _deploy folder itself.
3. Wait for upload to finish (~2 min for 23MB).
4. Scroll down → **"Commit changes"** → click **"Commit changes"**.

**Option B — Git command line (if you have git installed)**

```bash
cd D:/Work/Portfolio/_deploy
git init
git add .
git commit -m "Initial portfolio commit"
git branch -M main
git remote add origin https://github.com/vickykingrani/vickykingrani.github.io.git
git push -u origin main
```

### Enable GitHub Pages

1. On your repo page → **"Settings"** (top tabs) → **"Pages"** (left sidebar).
2. Source: **"Deploy from a branch"**
3. Branch: **`main`** · Folder: **`/ (root)`**
4. Click **"Save"**.
5. Wait 1-2 minutes — your site is now LIVE at:

> **https://vickykingrani.github.io**

---

## Part 4 — Verify everything works (3 min)

1. Visit **https://vickykingrani.github.io** — your portfolio should load.
2. Scroll through a few slides. Click a TOC entry.
3. Wait 2 minutes.
4. Check **[cloud.umami.is](https://cloud.umami.is)** dashboard:
   - **Pageviews** counter ticking up
   - **Events** showing `slide-view`, `slide-dwell`, `toc-click`, `scroll-depth`
5. Check **[one.dash.cloudflare.com](https://one.dash.cloudflare.com)** → Web Analytics:
   - Page views, visitors, country breakdown

---

## Updating the site later

### Web upload route

1. Edit any file (or replace) on your local machine.
2. Go to your repo → click the file → pencil icon → upload new version → commit.

### Git route

```bash
cd D:/Work/Portfolio/_deploy
# make your edits
git add .
git commit -m "describe what changed"
git push
```

Live in ~1 minute.

---

## Where to put the link

- **CV / resume:** Header line. Already in `Vicky_Kingrani_Resume.pdf`. Update to https://vickykingrani.github.io if you want the GitHub URL specifically.
- **LinkedIn:** "Featured" section + "Contact info" → website.
- **Email signature:** "Portfolio: https://vickykingrani.github.io"
- **Application emails:** "You can view my work at https://vickykingrani.github.io"

---

## Firewall-resilience expectations

- **github.io domain**: Almost universally allowed at corporate firewalls (developer infrastructure category)
- **Cloudflare Web Analytics tracker**: `static.cloudflareinsights.com` — rarely blocked
- **Umami tracker**: `cloud.umami.is` — sometimes blocked at strict regulated FS firms (HSBC, Barclays compliance teams)

If a recruiter at a strict bank says "I can't access the link," **the page itself almost certainly will load** because github.io is fine — only the analytics may be partially blocked. Your viewer count from Cloudflare will still be accurate; you'll just lose per-slide events for those viewers.

---

## What you'll see in analytics

After a few weeks of sharing the link, the Umami dashboard will tell you:

- **Daily / weekly visitors** — how many recruiters / hiring managers opened it
- **Per-slide views** — which case studies got read (look for: high views on Cases 01/02 = strong; low views on Cases 04/05 = drop-off, signal to revisit)
- **Per-slide dwell time** — which slides got read carefully (>10s = good signal)
- **TOC clicks** — which case study a recruiter clicked first (their first interest)
- **Scroll depth** — what % of viewers reached the closing slide
- **Referrers** — where viewers came from (LinkedIn, direct share, job board)
- **Countries** — UK / US / international breakdown

Cloudflare gives you the same page-level data as a backup.
