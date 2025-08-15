# Custom Domain Setup for KMMobi (GitHub Pages)

This guide helps you bind `www.kmmobi.net` to your GitHub Pages site.

## 1) Prerequisites
- You own the domain `kmmobi.net` (at Aliyun, Tencent Cloud, GoDaddy, Namecheap, etc.)
- GitHub repo: `fuyekai1-ui/kmmobi-website`
- GitHub Pages enabled: Settings → Pages → Source: `Deploy from a branch`, Branch: `main`

## 2) Add the CNAME file (done)
A `CNAME` file with this content is already in the repo root:
```
www.kmmobi.net
```
This tells GitHub Pages your custom domain.

## 3) DNS Records (set at your domain registrar)
Create these records in your DNS console:

- CNAME for the `www` subdomain
  - Type: CNAME
  - Name/Host: `www`
  - Value/Target: `fuyekai1-ui.github.io`
  - TTL: default (e.g., 3600)

- A records for apex (root) domain `kmmobi.net` (optional but recommended so kmmobi.net redirects to www)
  - Type: A, Name/Host: `@`, Value: `185.199.108.153`
  - Type: A, Name/Host: `@`, Value: `185.199.109.153`
  - Type: A, Name/Host: `@`, Value: `185.199.110.153`
  - Type: A, Name/Host: `@`, Value: `185.199.111.153`

Propagation may take 5–30 minutes (sometimes up to 24h).

## 4) Set custom domain in GitHub
- Open repo → Settings → Pages → Custom domain → enter `www.kmmobi.net`
- Click Save
- Enable “Enforce HTTPS” when the TLS certificate is issued

## 5) Verify
- Visit `https://www.kmmobi.net`
- Visit `https://kmmobi.net` (should redirect to `www.kmmobi.net` after DNS propagates)

## 6) Update flow
After any website edits:
```
git add .
git commit -m "Update site"
git push
```
GitHub Pages will auto-redeploy.

## Troubleshooting
- Domain not resolving: wait for DNS propagation; verify records
- No HTTPS toggle: wait ~5–30 minutes after saving the custom domain
- CSS/JS not loading: check relative paths and file names
- Wrong domain in CNAME: ensure it matches exactly `www.kmmobi.net`

---
Tip: Keep only one custom domain (www) in CNAME. Use A records for apex to support `kmmobi.net` → `www.kmmobi.net` redirect.
