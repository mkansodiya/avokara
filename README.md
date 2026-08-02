# Avokara Website

Static website for Avokara Private Limited — www.avokaraai.com.
Pure HTML/CSS, no build step, no JavaScript dependency for content. Ready for GitHub Pages.

## Deploy on GitHub Pages (5 minutes)

1. Create a new GitHub repository (e.g. `avokara-website`).
2. Upload **the contents of this folder** (not the folder itself) to the repository root — `index.html` must be at the top level.
3. In the repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / root → Save**.
4. Your site is live at `https://<username>.github.io/<repo>/` within a minute or two.

## Connect the custom domain (www.avokaraai.com)

1. The `CNAME` file in this folder already contains `www.avokaraai.com` — GitHub Pages picks it up automatically.
2. At your domain registrar (where avokaraai.com is registered), add DNS records:
   - `CNAME` record: host `www` → `<username>.github.io.`
   - Four `A` records for the apex `avokaraai.com` → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. In repo **Settings → Pages**, confirm the custom domain shows `www.avokaraai.com` and tick **Enforce HTTPS** once the certificate is issued (can take up to an hour).

## Contact form

The form on `/contact/` posts to Formspree. Create a free form at https://formspree.io, then replace
`YOUR_FORM_ID` in `contact/index.html` with your real form ID (one line). Until then, the email
link works as a fallback.

## Editing content

Every page is plain HTML in its own folder (`services/ai-agent-development/index.html` etc.).
Shared styling lives in `assets/styles.css`. If you have the generator (`website/*.py` in the
project folder), edit the content files and rebuild with `python3 pages4.py`.

## After deploying

- Submit `https://www.avokaraai.com/sitemap.xml` in Google Search Console and Bing Webmaster Tools.
- Set up the `hello@avokaraai.com` mailbox (or change the address in the site) so email links work.
