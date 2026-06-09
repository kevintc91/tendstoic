# Putting tendstoic.com live (GitHub Pages + Cloudflare DNS)

Same pattern as the privacy policy site. About 15 minutes, then up to an hour of DNS/certificate waiting.

## Step 1: Create the repo

1. Go to github.com → New repository
2. Name it `tendstoic` (any name works), Public, no README
3. Upload both files from this `landing/` folder: `index.html` and `CNAME`
   (the CNAME file tells GitHub Pages which domain to serve; it's already filled in)
4. Commit

## Step 2: Enable Pages

1. Repo → Settings → Pages
2. Source: "Deploy from a branch", Branch: `main`, folder `/ (root)` → Save
3. In the "Custom domain" field type `tendstoic.com` → Save
   (it may show a DNS warning until Step 3 propagates; that's normal)

## Step 3: DNS at Cloudflare

In the Cloudflare dashboard → tendstoic.com → DNS → Records, add these five:

| Type | Name | Content | Proxy status |
|---|---|---|---|
| A | @ | 185.199.108.153 | DNS only (grey cloud) |
| A | @ | 185.199.109.153 | DNS only |
| A | @ | 185.199.110.153 | DNS only |
| A | @ | 185.199.111.153 | DNS only |
| CNAME | www | kevintc91.github.io | DNS only |

Important: set each record to **DNS only** (click the orange cloud so it turns grey). GitHub needs to see the domain directly to issue its HTTPS certificate. You can flip them to proxied later if you ever want Cloudflare's CDN, but DNS-only is the no-surprises configuration.

## Step 4: HTTPS

1. Back in GitHub repo → Settings → Pages, wait for the DNS check next to the custom domain to turn green (can take 15 to 60 minutes)
2. Tick "Enforce HTTPS"

## Step 5: Verify

- https://tendstoic.com loads the page
- https://www.tendstoic.com redirects to the apex
- Page looks right in both light and dark mode (toggle your OS theme)
- The "Join the closed test" button opens the Play opt-in page

## Updating the page later

Edit `index.html` in the repo (or re-upload from this folder). Changes go live in about a minute. At public launch, swap the CTA link to the real Play Store listing URL:
`https://play.google.com/store/apps/details?id=com.kevintc91.tend`
