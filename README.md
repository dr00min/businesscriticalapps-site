# businesscriticalapps.com

Static site for **Business Critical Apps** — landing page plus the legal pages that the
Atlassian Marketplace listing for *Confluence Bulk Operations* links to.

## Structure (clean URLs)

| File | Served at |
|---|---|
| `index.html` | `/` |
| `docs/index.html` | `/docs` (setup guide + use cases) |
| `support/index.html` | `/support` |
| `privacy/index.html` | `/privacy` |
| `terms/index.html` | `/terms` |
| `styles.css` | `/styles.css` (shared) |

Each page also has a flat companion at the root (e.g. `docs.html`, `support.html`) so the
Marketplace link checker doesn't trip on Cloudflare Pages' 307 trailing-slash redirect. When you
add or change a page, update **both** `<page>/index.html` and `<page>.html`.

The folder-per-page layout gives extension-less URLs (`/privacy`, `/terms`) on Cloudflare Pages
without needing redirects. These exact URLs are referenced from the app's Marketplace listing and
Distribution settings, so **don't rename the folders** without updating those links.

## Deploy — Cloudflare Pages CI/CD

The domain DNS is already on Cloudflare. To wire continuous deployment:

1. Push this repo to GitHub (or GitLab).
2. Cloudflare dashboard → **Workers & Pages → Create → Pages → Connect to Git** → pick this repo.
3. Build settings: **Framework preset = None**, **Build command = (empty)**, **Build output directory = `/`**
   (it's plain static HTML — no build step).
4. **Custom domains** → add `businesscriticalapps.com` (Cloudflare wires the DNS automatically since it
   manages the zone).

After that, every push to the default branch redeploys automatically. The previous manual
**Direct Upload** of `/privacy` can be replaced by this Git-connected project.

## Editing notes

- Legal content lives in `privacy/index.html` and `terms/index.html`. Update the **Effective date**
  at the top of a page when you make a material change.
- Keep the privacy/security claims consistent with the app's actual behaviour and with the
  Marketplace **Privacy & Security** tab — don't claim anything stronger than is true.
- Publisher identity: **Business Critical Apps**, operated by Andrew Abdul-Malek (sole trader);
  contact `info@businesscriticalapps.com`; governing law England and Wales, UK.
