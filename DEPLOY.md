# Deploying teamvconstructiongroup.com on GitHub Pages

Everything in this folder is the **repo root**. Do not nest it in a subfolder.

## 1. Confirm the repo

Your repo: https://github.com/michaelvredevelt/teamvconstructiongroup.com

Check two things before uploading:
- **Settings → General → Visibility** must be **Public**. Pages requires a
  paid plan to serve from a private repo.
- The repo should be empty, or at least have no `index.html` yet. If GitHub
  created a README when you made it, that is fine and can stay.

## 2. Upload these files

If the repo is empty, click **uploading an existing file** on the landing
page. If it already has a README, go to **Add file → Upload files**.

Either way: unzip this package on your computer, open the
`teamvconstructiongroup` folder, and drag in its *contents* — not the
folder itself. That means index.html, styles.css, gallery.js, 404.html,
CNAME, robots.txt, sitemap.xml, favicon.ico, the icon PNGs, and the
`assets/` and `services/` folders. Commit.

Verify after upload: `index.html` and `CNAME` must sit at the top level of
the repo. If you see a `teamvconstructiongroup` folder instead, you dragged
the wrong thing — delete it and re-upload the contents.

Note: `.nojekyll` is a hidden file and the browser upload may skip it.
If it does, create it manually: **Add file → Create new file**, name it
`.nojekyll`, leave it empty, commit.

## 3. Turn on Pages

Repo → **Settings** → **Pages**
- Source: *Deploy from a branch*
- Branch: `main` / folder `/ (root)` → **Save**

The Custom domain field will auto-populate with
`www.teamvconstructiongroup.com` from the CNAME file. It will show an
error until DNS is live — that is expected.

## 4. DNS in Squarespace

Google Admin console → Domains → teamvconstructiongroup.com →
**MANAGE DOMAIN (via Squarespace)** → DNS settings.

**Delete first:** any existing A record on `@` (root/blank host), and any
Squarespace parking or default records.

**Then add:**

| Type  | Host | Value                    |
|-------|------|--------------------------|
| CNAME | www  | michaelvredevelt.github.io |
| A     | @    | 185.199.108.153          |
| A     | @    | 185.199.109.153          |
| A     | @    | 185.199.110.153          |
| A     | @    | 185.199.111.153          |

Enter the CNAME value exactly as `michaelvredevelt.github.io` — no
`https://`, no repo name, no trailing slash. The repo name
(`teamvconstructiongroup.com`) never appears in DNS; the `CNAME` file
inside the repo is what maps the domain to this specific repo.

**Do not touch:** MX records, or TXT records starting with `v=spf1` or
named `google._domainkey`. Those are your Gmail and email
authentication. Deleting MX takes your email offline.

**Skip** the Google Admin "Change redirect" screen entirely. It is
HTTP-only and GitHub handles the apex-to-www redirect with a real
certificate.

## 5. Finish (30-60 min later)

Repo → Settings → Pages → refresh. Green check on the domain, then tick
**Enforce HTTPS**. If the box is greyed out, the certificate is still
issuing — wait, then re-check. Still stuck after a few hours: clear the
Custom domain field, Save, re-enter it, Save.

## 6. After it is live

- Google Search Console → add property `https://www.teamvconstructiongroup.com`
  → submit `https://www.teamvconstructiongroup.com/sitemap.xml`
- Link the site from your Google Business Profile and LinkedIn
- Test the share preview: paste the URL into LinkedIn's post composer and
  confirm the og-image renders

## What changed from the v4 package

- `CNAME` → binds the repo to www.teamvconstructiongroup.com
- `.nojekyll` → skips Jekyll processing, faster and avoids surprises
- Canonical URLs on all 7 pages → prevents `/index.html` vs `/` duplicate
  indexing
- Open Graph + Twitter Card tags → link previews on LinkedIn, iMessage,
  Slack, Facebook
- `assets/og-image.jpg` → 1200x630 share image cropped from the hero
- `GeneralContractor` JSON-LD on the homepage → CSLB license numbers,
  San Marcos address, and service list in machine-readable form for local
  search
- Favicons: `favicon.ico`, `icon-192.png`, `icon-512.png`,
  `apple-touch-icon.png`
- `robots.txt` + `sitemap.xml` with absolute URLs
- `404.html` styled to match the site
- Hero image converted from a 3.0 MB PNG to a 336 KB progressive JPEG
  (~89% smaller, no visible difference on a photo) and the two CSS
  references updated
- Truncated service-page meta descriptions closed off cleanly

## Local preview

Relative paths are preserved, so opening `index.html` directly in a
browser works. For an exact match to production:

    python3 -m http.server 8000

then visit http://localhost:8000

## What changed in the November 2026 update

- Phone number (760) 805-0299 shown as a tap-to-call link on the homepage and in every page footer (the "Click to show number" button is gone)
- Service area now reads San Diego, Orange County and Los Angeles instead of "nationwide", in the page text and in the business data Google reads
- DIR PWCR #2000038322 added next to the CSLB license on every page
- EV charging page reworded so the "thousands of ports" claim is tied to 37 years in the electrical trade
- Project sections retitled "Project Experience" with a note that they include projects built in prior roles at EDF Renewables, PowerFlex, Morrow-Meadows, Neal Electric and Sullivan Solar Power
- New October 2026 logo everywhere: header and footer logo (white version), color logo for Google's business data, browser tab icon, phone home-screen icons, and the link-preview image
- Homepage hero and call-to-action backgrounds now use real job photos (EV chargers, solar carport) instead of the old graphic that carried the previous logo
