# PrimeBite Fishing Website

This repository is the live website repo for PrimeBite Fishing. Netlify deploys from this repo to:

- `https://www.primebitefishing.com/`

## Public Site Files

- `index.html` — site home (includes the Transparency section linking to species pages)
- `baseline.html` — general baseline transparency page
- `yellowfin.html` — Yellowfin Tuna transparency page
- `bigeye.html` — Bigeye Tuna transparency page
- `mahi.html` — Mahi-mahi transparency page
- `blackmarlin.html` — Black Marlin transparency page
- `walleye.html` — Walleye transparency page
- `muskie.html` — Muskie transparency page
- `pike.html` — Northern Pike transparency page
- `largemouth-bass.html` — Largemouth Bass transparency page
- `privacy.html` — privacy policy
- `terms.html` — terms of use
- `_redirects` — Netlify redirects
- `images/` — public image assets

## Safe Update Workflow

Use this workflow to avoid the two biggest website-update mistakes:

1. Update only the public site files that actually changed.
2. Verify the live site with direct checks instead of trusting stale cached previews.

### Small change

For a one-file change, keep it targeted:

```bash
git status --short
git add index.html
git commit -m "Describe the website change"
git push
```

### Larger public-site sync from the app repo

If the change started in the main app repo, the source copy lives there under `website/`.
The safest bulk-sync helper in the app repo is:

```bash
website/update-website.sh
```

That helper intentionally syncs only public site assets:

- `website/*.html`
- `website/_redirects`
- `website/images/`

It does **not** blindly mirror repo-specific files like `README.md`.

## Verification

After pushing:

1. Wait for Netlify to deploy.
2. Check the exact live page directly.
3. Prefer direct responses over cached previews.

Useful checks:

```bash
curl -L -I -s https://www.primebitefishing.com/
curl -L -s https://www.primebitefishing.com/ | rg "your changed text"
```

If a search preview or crawler still looks stale, trust the direct live HTML response first.

## Guardrails

- Do not publish proprietary calibration details, formulas, raw weights, benchmark anchors, or similar secret sauce on public pages.
- Keep species methodology pages aligned with the live app behavior and the current disclosure policy.
- If a species page changes, make sure the homepage Transparency section still links to it.
