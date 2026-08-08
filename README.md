# sabrina-reis.com

Personal academic site built with Jekyll, deployed via GitHub Pages.

## Structure

- `index.md` — About page (home)
- `publications.md` — Publications (filtered to programming-languages / formal-verification work)
- `cv.md` — Full CV
- `_layouts/default.html` — Page shell (masthead nav + footer)
- `assets/css/style.css` — All styling
- `CNAME` — Custom domain config (`sabrina-reis.com`)

## Before you push

1. **Fill in real links** in `_config.yml`:
   ```yaml
   github_url: "https://github.com/YOUR_USERNAME"
   email: "your@email.com"
   orcid_url: "https://orcid.org/YOUR-ORCID-ID"
   ```
2. If your repo is `<username>.github.io`, `url` in `_config.yml` should stay as `https://sabrina-reis.com` (the custom domain) — leave `baseurl` empty.
   If instead you're using a project repo (e.g. `username/website`) served at a `/website/` path *without* the custom domain, set `baseurl: "/website"` — but since you're pointing `sabrina-reis.com` at this repo via `CNAME`, you likely want baseurl empty either way.

## Run locally

```bash
bundle install
bundle exec jekyll serve
```

Visit `http://localhost:4000`.

**Note on the Gemfile:** this uses plain `jekyll` + `jekyll-seo-tag` rather than the `github-pages` gem. The `github-pages` gem exists to mirror GitHub's exact build environment (useful if you're using GitHub-Pages-only plugins), but it pins an old native-extension markdown parser (`commonmarker`) that can fail to compile against newer Ruby versions. Since this site only uses `kramdown` (already the GitHub Pages default) and `jekyll-seo-tag` (which GitHub Pages supports), plain `jekyll` builds an identical result without that dependency. GitHub still builds your site the same way on their end when you push — this only affects local development.

## Deploy to GitHub Pages

1. Push this repo to GitHub (either `sabrina-reis.github.io`-style or any repo name — the `CNAME` file is what maps your custom domain).
2. In the repo, go to **Settings → Pages** and set the source to the branch you pushed (e.g. `main`, root).
3. Under **Settings → Pages → Custom domain**, confirm `sabrina-reis.com` is set (GitHub will pick it up from the `CNAME` file automatically, but double check it here).
4. At your domain registrar, point DNS at GitHub Pages:
   - For an apex domain (`sabrina-reis.com`), add **A records** pointing to:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - If you also want `www.sabrina-reis.com` to work, add a **CNAME record** for `www` pointing to `<your-github-username>.github.io`.
5. Wait for DNS to propagate, then enable **Enforce HTTPS** in the Pages settings once GitHub shows the certificate is ready.

## Adding a new publication

Open `publications.md` and copy one of the existing `<li class="pub">...</li>` blocks — update year, title, authors (wrap yourself in `<span class="pub__me">`), and venue. Mirror the same entry in `cv.md`'s Papers section if you want it on both pages.
