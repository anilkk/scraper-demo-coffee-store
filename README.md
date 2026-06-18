# Northbound Coffee: demo store (Vercel + GitHub Action version switch)

[![Switch store version](https://github.com/anilkk/scraper-demo-coffee-store/actions/workflows/switch-version.yml/badge.svg)](https://github.com/anilkk/scraper-demo-coffee-store/actions/workflows/switch-version.yml)
[![Live version](https://img.shields.io/badge/live-v1%20original-16a34a)](https://github.com/anilkk/scraper-demo-coffee-store/blob/main/index.html)
[![Deploy](https://img.shields.io/badge/deploy-Vercel-black?logo=vercel)](https://vercel.com)

> **Currently live: `v1` (original layout).** This reflects what is committed to `index.html`. Flip it with the GitHub Action (see below).

A tiny static store for the Scraper Studio Self-Healing video. The **same live URL**
serves either the original layout (`v1`) or the "redesigned" layout (`v2`). You flip
between them on camera by running a one-click GitHub Action. Vercel auto-redeploys the
same URL, so the site appears to "change" live.

Each version shows a color-coded flag in the top-right corner so it is obvious on camera which one is live: a green `v1 · original` badge or an orange `v2 · redesign` badge. The flag is decorative and sits outside the product cards, so it does not affect what your scraper extracts.

```
index.html              ← the page Vercel serves (starts as v1)
versions/v1.html        ← original layout (clean class names)
versions/v2.html        ← redesigned layout (renamed classes → breaks scrapers)
.github/workflows/switch-version.yml  ← one-click version switch
```

---

## One-time setup (~5 min)

### 1. Put this folder on GitHub (account: anilkk)
From inside this `scraper-demo-coffee-store` folder:
```bash
git init
git add .
git commit -m "Demo coffee store"
git branch -M main
# create an empty repo named e.g. "scraper-demo-coffee-store" at github.com/new (Public), then:
git remote add origin https://github.com/anilkk/scraper-demo-coffee-store.git
git push -u origin main
```
(Or use the GitHub website: New repo → upload all these files.)

> The repo can be Public or Private. Vercel works with both. Keep it Public if you want viewers to be able to peek.

### 2. Connect it to Vercel
1. Go to vercel.com → **Add New → Project**.
2. Import the `scraper-demo-coffee-store` repo (authorize Vercel for GitHub if prompted; you do this step).
3. Framework preset: **Other** (it's plain static HTML). No build command, no settings to change.
4. Deploy. You'll get a public URL like `https://scraper-demo-coffee-store-anilkk.vercel.app`.

That URL serves whatever is in `index.html`. Right now that is **v1**.

> Vercel auto-redeploys on every push to `main`, which is what makes the Action work.

---

## How to flip the version on camera

1. On GitHub, open the repo → **Actions** tab → **Switch store version** → **Run workflow**.
2. Pick `v2` (the redesign) → **Run workflow**.
3. The Action swaps `index.html` to v2 and pushes; Vercel redeploys in about 20 to 40 seconds.
4. Refresh your Vercel URL: same address, new layout. Your scraper now breaks.

To reset for the next take, run it again and pick `v1`.

> **Filming tip:** the redeploy takes a few seconds. Either trigger `v2` just before you start the "the site redesigned" beat, or cut the wait in Descript. The viewer sees: same URL → refresh → broken scraper.

---

## Demo recap (matches the simple transcript)

1. Build a Scraper Studio scraper on your Vercel URL (serving **v1**) → name + price → clean JSON.
2. Run the **Switch store version** Action → `v2`.
3. Refresh / re-run in Scraper Studio → it breaks.
4. Click **Self-Healing** → it recovers.

Public data only, a store you own. Honest and repeatable.
