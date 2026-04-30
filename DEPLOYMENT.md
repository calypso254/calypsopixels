# Connect calypsopixels.com to GitHub Pages (GoDaddy)

This repo is ready for a custom domain via the `CNAME` file (`calypsopixels.com`).

## 1) Push this repo to GitHub

```bash
git remote add origin git@github.com:<your-user-or-org>/<repo>.git
git push -u origin <branch-name>
```

## 2) Enable GitHub Pages

1. Open your GitHub repo.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**:
   - **Source**: `Deploy from a branch`
   - **Branch**: your default branch (ex: `main`)
   - **Folder**: `/ (root)`
4. Click **Save**.

## 3) Add DNS records in GoDaddy

1. Log in to GoDaddy.
2. Go to **My Products**.
3. On your domain, click **DNS** (or **Manage DNS**).
4. In **Records**, add/update these entries:

### Apex/root domain records (`calypsopixels.com`)
Add four **A** records for host `@`:

- `@` → `185.199.108.153`
- `@` → `185.199.109.153`
- `@` → `185.199.110.153`
- `@` → `185.199.111.153`

TTL can stay on default (usually 1 hour).

### WWW record (`www.calypsopixels.com`)
Add one **CNAME**:

- Host: `www`
- Points to: `<your-user-or-org>.github.io`

If an existing `www` A record exists, delete it before adding the CNAME.

## 4) Set custom domain in GitHub Pages

Back in **GitHub → Settings → Pages**:

- Set **Custom domain** to `calypsopixels.com`
- Wait for DNS check to pass
- Then enable **Enforce HTTPS**

## 5) Verify propagation

```bash
dig calypsopixels.com +short
dig www.calypsopixels.com +short
```

Expected:
- Apex returns GitHub Pages IPs above
- `www` returns `<your-user-or-org>.github.io` (or its resolved IPs)

Once propagated, your site should load at:

- `https://calypsopixels.com`
- `https://www.calypsopixels.com`

---

## Troubleshooting (GoDaddy)

- If GitHub says domain is invalid, wait 10–30 minutes and retry.
- If HTTPS toggle is disabled, DNS likely hasn’t fully propagated yet.
- If `www` doesn’t work, confirm `www` is a **CNAME** (not A/Forwarding).
- If root works but old content appears, clear browser cache or test in private mode.
