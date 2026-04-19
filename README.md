# auditfocus-site

Static marketing site for the AuditFocus Chrome extension, served at https://auditfocus.app.

Three pages, plain HTML, no build step, no framework:

- `index.html` — landing page (hero, features, differentiators, pricing, setup CTA, footer)
- `privacy.html` — privacy policy (URL submitted to the Chrome Web Store)
- `setup.html` — Chrome AI / Gemini Nano setup guide for Pro and Agency users

## Deploy to Vercel via GitHub

1. Create a new public repo on GitHub under the Loophead Labs account, named `auditfocus-site`.
2. From this folder:
   ```
   git init
   git add .
   git commit -m "Initial site: homepage, privacy, Chrome AI setup"
   git branch -M main
   git remote add origin git@github.com:<your-account>/auditfocus-site.git
   git push -u origin main
   ```
3. In the Vercel dashboard, click **Add New → Project**, import the `auditfocus-site` repo, accept the defaults (Vercel reads `vercel.json`), and deploy.
4. In the Vercel project settings, open **Domains** and add `auditfocus.app` (and optionally `www.auditfocus.app`).
5. At your DNS provider for `auditfocus.app`:
   - Apex record: either an `A` record to `76.76.21.21`, or an `ALIAS/ANAME` to `cname.vercel-dns.com`.
   - `www` CNAME to `cname.vercel-dns.com`.
6. Vercel provisions a TLS certificate automatically. Give it a minute, then visit https://auditfocus.app.

Once DNS propagates:

- https://auditfocus.app serves the homepage
- https://auditfocus.app/privacy serves the privacy policy (this is the URL that goes into the Chrome Web Store "Privacy policy URL" field)
- https://auditfocus.app/setup serves the Chrome AI setup guide

The `cleanUrls` setting in `vercel.json` means the `.html` suffix is optional; both `/privacy` and `/privacy.html` resolve to the same page.

## Local preview

```
cd auditfocus-site
python3 -m http.server 4000
```

Open http://localhost:4000 in your browser.

## Editing copy

All three pages are single self-contained HTML files with inline `<style>` blocks. Edit the HTML directly. CSS variables at the top of each file (`--accent`, `--bg`, `--ink`, etc.) control the brand palette. The AuditFocus accent color is `#0a4d68`, matching the extension's side panel.

## Files

| File            | Purpose                                               |
| --------------- | ----------------------------------------------------- |
| `index.html`    | Homepage                                              |
| `privacy.html`  | Privacy policy                                        |
| `setup.html`    | Chrome AI / Gemini Nano setup guide                   |
| `vercel.json`   | Vercel build config with clean URLs and security headers |
| `CNAME`         | Legacy GitHub Pages domain binding (harmless on Vercel) |
| `.nojekyll`     | Legacy GitHub Pages marker (harmless on Vercel)       |
| `.gitignore`    | Ignore OS, editor, and Vercel build artifacts         |
