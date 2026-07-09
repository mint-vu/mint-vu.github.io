# MINT Lab Website — Setup Guide

The site is a Jekyll site with **Sveltia CMS** (a free, git-based content editor) at
`https://mint-vu.github.io/admin/`. Editors log in with GitHub; every edit becomes a
commit and the site rebuilds automatically.

---

## 1. One-time: switch GitHub Pages to Actions builds

The repo now includes `.github/workflows/deploy.yml` (builds with Jekyll 4).

1. Push this code to `main` of `mint-vu/mint-vu.github.io`.
2. In the repo: **Settings → Pages → Build and deployment → Source → GitHub Actions**.
3. Push again (or run the workflow manually) — the site deploys.

## 2. One-time: enable CMS login (~10 minutes)

Because the site is on GitHub Pages, the CMS needs a tiny free authentication relay.
The standard one is **sveltia-cms-auth** on Cloudflare Workers (free tier is plenty):

1. Go to https://github.com/sveltia/sveltia-cms-auth and click **Deploy to Cloudflare Workers**
   (create a free Cloudflare account if needed). Note your worker URL, e.g.
   `https://sveltia-cms-auth.YOURNAME.workers.dev`.
2. Create a GitHub OAuth App: GitHub → **Settings → Developer settings → OAuth Apps → New OAuth App**
   (create it under the `mint-vu` organization if possible):
   - Homepage URL: `https://mint-vu.github.io`
   - Authorization callback URL: `https://<your-worker-url>/callback`
3. In the Cloudflare Worker → **Settings → Variables**, add:
   - `GITHUB_CLIENT_ID` — from the OAuth app
   - `GITHUB_CLIENT_SECRET` — from the OAuth app
   - `ALLOWED_DOMAINS` — `mint-vu.github.io`
4. In `admin/config.yml`, replace `base_url: https://YOUR-AUTH-WORKER.workers.dev`
   with your worker URL. Commit and push.

Now visit `https://mint-vu.github.io/admin/`, sign in with GitHub, and edit away.

> When you later migrate hosting to **Netlify** or **Cloudflare Pages**, this still works
> unchanged — just update `ALLOWED_DOMAINS` and the `site_url`/`base_url` values.

## 3. Granting a lab member edit access

The CMS uses GitHub permissions — no separate accounts:

1. Repo → **Settings → Collaborators and teams → Add people** → their GitHub username →
   role **Write**. (Or add them to a team in the `mint-vu` org with write access.)
2. They visit `/admin/`, sign in with their GitHub account, and can edit everything.

To revoke access, remove them as a collaborator.

## 4. What's editable from the browser

| CMS section | What it controls |
|---|---|
| **People** | Add/edit members: name, role, photo (uploads to `images/people/`), email, website, bio, fun fact. Move someone to Alumni by changing their Position and filling in "Current position". |
| **News** | The homepage news list. Newest first automatically. |
| **Publications** | The full publication list, grouped by year automatically. The homepage shows the most recent ones. |
| **Homepage** | Intro paragraph, photo carousel (upload lab photos + captions), selected talks (YouTube IDs), how many news/papers appear. |
| **Pages** | The About and Join pages (markdown). |

## 5. Local development (optional)

```bash
bundle install
bundle exec jekyll serve
# open http://localhost:4000
```

## 6. Notes

- Old URLs `/publication/` and `/resources/` redirect to `/publications/` and `/join/`.
- Person page URLs are now lowercase (e.g. `/people/xinran-liu/`).
- The old `CNAME` file contained the default domain and was removed; when you get a
  custom domain, add a `CNAME` file containing it and configure it in Pages settings.
