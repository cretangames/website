# Cretan Games — coming-soon site

Single static page (`index.html`) + a GitHub Actions workflow that auto-deploys
to GitHub Pages on every push to `main`. No build step, no dependencies.

## One-time setup (needs your GitHub login — I don't have access to create this myself)

1. Create a new GitHub repo, e.g. `cretangames/website` (public or private — Pages
   works either way, but private repos need GitHub Pro/Team/Enterprise for Pages).
2. Push everything in this folder to the repo's `main` branch:
   ```
   git init
   git add .
   git commit -m "Coming soon page"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```
3. In the repo: **Settings → Pages → Build and deployment → Source → GitHub Actions**.
   (Not "Deploy from a branch" — the workflow in `.github/workflows/deploy.yml` handles
   the build/deploy itself.)
4. Push to `main` again (or re-run the workflow from the Actions tab) — the site
   will be live at `https://<org-or-user>.github.io/<repo>/` within a minute or two.

## Pointing cretangames.gr at it

The `CNAME` file already in this repo tells GitHub Pages to serve on the custom
domain. You still need to add DNS records at wherever cretangames.gr is registered:

- **Apex domain (cretangames.gr):** add these four `A` records pointing to GitHub's
  Pages IPs:
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```
- **www subdomain (optional):** a `CNAME` record for `www` pointing to
  `<org-or-user>.github.io`.

Then in the repo: **Settings → Pages → Custom domain**, enter `cretangames.gr`,
save, and check "Enforce HTTPS" once the certificate provisions (can take up to
24h after DNS propagates).

## Editing the page

Everything is in `index.html` — plain HTML/CSS, no build tooling. Edit, commit,
push to `main`, and the Action redeploys automatically.

## If you ever outgrow static hosting

This setup costs nothing and has no infrastructure to maintain. If the site later
needs a real backend (which — per the current plan — it won't, since registration
runs through a third-party provider), moving off GitHub Pages is just a DNS
change; the HTML/CSS itself doesn't need to change with it.
