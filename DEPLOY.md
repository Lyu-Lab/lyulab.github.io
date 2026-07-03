# Deploying the Lyu Lab site (replacing the WordPress site on SiteGround)

The site is a **Jekyll** static site. `lyulab.org` currently serves a **WordPress**
install hosted on **SiteGround**. There are two ways to put this site live. Path A
(GitHub Pages) is recommended — it's free, version-controlled, and matches the
`CNAME` file already in this repo.

---

## Path A — GitHub Pages (recommended)

### 1. Push the repo to GitHub
```bash
# create an empty repo on github.com first (e.g. lyulab/lyulab.github.io),
# then, from this folder:
git remote add origin git@github.com:<user-or-org>/<repo>.git
git add -A
git commit -m "Content mirror + design refresh"
git push -u origin main
```
The repo already contains a `CNAME` file with `lyulab.org`.

### 2. Turn on GitHub Pages
Repo → **Settings → Pages** → *Build and deployment* →
Source: **Deploy from a branch** → Branch: **main** / **/(root)** → Save.
GitHub builds the Jekyll site automatically (via the `github-pages` gem). The
custom-domain field will show **lyulab.org** (read from `CNAME`).

### 3. Repoint DNS away from SiteGround
This is the step that actually moves traffic off WordPress. Find where DNS is
managed — usually **SiteGround → Site Tools → Domain → DNS Zone Editor** (if the
domain uses SiteGround's nameservers), otherwise at your domain registrar. Then:

| Type  | Host / Name | Value |
|-------|-------------|-------|
| A     | `@`         | `185.199.108.153` |
| A     | `@`         | `185.199.109.153` |
| A     | `@`         | `185.199.110.153` |
| A     | `@`         | `185.199.111.153` |
| CNAME | `www`       | `<user-or-org>.github.io` |

**Remove** the old A record that points `@` at the SiteGround server.

### 4. Enable HTTPS
After DNS propagates (minutes to a few hours), return to Settings → Pages and
tick **Enforce HTTPS** once the certificate is issued.

### 5. Verify, then decommission WordPress
Load `https://lyulab.org`, click through every page, then take the WordPress
site down in SiteGround (keep a backup first).

---

## Path B — Stay on SiteGround, upload the static build (no DNS change)

Use this if you'd rather keep hosting at SiteGround.

```bash
bundle exec jekyll build      # generates the _site/ folder
```
1. In **SiteGround → Site Tools → File Manager** (or SFTP), back up and remove
   the WordPress files in `public_html` (or move them into a subfolder).
2. Upload the **contents of `_site/`** into `public_html`.
3. No DNS change is needed — the domain already points to SiteGround, and HTTPS
   is already provisioned there.

Trade-offs: you must re-run `jekyll build` and re-upload on every change, and you
lose WordPress. This can be automated later with a GitHub Action that builds and
SFTP-deploys to SiteGround.

---

## Local preview

```bash
bundle install
bundle exec jekyll serve      # http://localhost:4000
```
Requires Ruby 3.x (see `.ruby-version`).
