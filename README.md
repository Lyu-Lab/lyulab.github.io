# Lyu Lab website

Source for the **Lyu Lab** website — the Evnin Family Laboratory of Computational Molecular Discovery at The Rockefeller University.

**Live site:** https://lyu-lab.github.io  *(custom domain `lyulab.org` coming soon)*

Built with [Jekyll](https://jekyllrb.com/) and deployed to GitHub Pages via GitHub Actions. **Anything merged to `main` goes live automatically in about a minute.**

---

## Repository structure

| Path | What it holds |
|------|---------------|
| `index.md` | **Home** page (welcome text + video) |
| `research/` | **Research** page |
| `publications/` | **Publications** page (the layout; the papers live in `_publications/`) |
| `members/` | **People** page (the layout; the profiles live in `_members/`) |
| `gallery/` | **Gallery** page (the layout; the photo list lives in `_data/gallery.yml`) |
| `join/` | **Positions** page |
| `contact/` | **Contact** page |
| `_members/` | **One file per person** — edit this to change your profile |
| `_publications/` | **One file per paper** |
| `_data/gallery.yml` | **The gallery photo list** — one entry (photo + caption) per picture |
| `static/img/members/` | Member photos |
| `static/img/gallery/` | Gallery (lab life) photos |
| `static/img/research/` | Research figures |
| `static/css/custom.css` | Site styling (colors, fonts, layout) |
| `_data/navigation.yml` | Top navigation menu |
| `_includes/`, `_layouts/` | Page templates (HTML) — rarely need editing |
| `_config.yml` | Site-wide settings |
| `.github/workflows/pages.yml` | The build-and-deploy pipeline |

---

## How to update the site

The repository is **public**, so anyone can propose changes:

1. **Fork** this repo (the *Fork* button, top-right).
2. Edit the file(s) in your fork — the easiest way is right in the browser: open a file and click the ✏️ pencil.
3. Commit, then open a **Pull request** back to `Lyu-Lab/Lyu-Lab.github.io`.
4. Once it's merged, the site rebuilds and your change is live in ~1 minute.

> Not comfortable with GitHub? Just send your changes (and a headshot) to JK and he'll add them.

### 1. Update your personal information

Edit your file in `_members/` (named by last name, e.g. `du.md`, `tan.md`, `chen.md`). It's a small text file:

```yaml
---
name: Jane Doe
position: Graduate Student                     # your title
startdate: [2025-09-01]                         # when you joined → shows "Joined 2025"
enddate: []                                     # leave empty while you're in the lab
order: 4                                         # display order (lower number = higher up)
image: /static/img/members/placeholder.svg      # your photo (see below)
email: jdoe (at) rockefeller.edu                 # " (at) " keeps bots from scraping it
education: "B.S., 2024, Your University"         # separate multiple degrees with ·
note: "Co-mentored with ... (institution)"       # optional
# Optional links — add any you have, delete the rest:
scholar: your-google-scholar-id                  # the id in scholar.google.com/citations?user=THIS
github: your-username
twitter: your-handle
orcid: 0000-0000-0000-0000
linkedin: your-username
website: https://your-site.com
---
```

Only `name` and `position` are really needed — delete any line you don't want.

### 2. Update or add your photo

1. Add a **square** headshot (e.g. 500×500 px, `.jpg` or `.png`) to `static/img/members/`, named after yourself — e.g. `jdoe.jpg`.
2. In your `_members/` file, set `image: /static/img/members/jdoe.jpg`.

No photo yet? Leave `image: /static/img/members/placeholder.svg` and the site automatically shows your initials in a circle.

### 3. Add or update a publication

Add a file to `_publications/`, named `YEAR_firstauthor_topic.md`:

```yaml
---
title: "Your paper title"
authors: "**Doe J&dagger;**, Smith A&dagger;, ..., **Lyu J&#42;**"
journal: "Nature"                 # journal name, or "Preprint"
pub_date: "2026-05-01"            # most recent dates sort to the top
key: true                         # optional: features it under "Selected publications after Rockefeller"
links:
- name: "Journal"
  url: "https://doi.org/..."
- name: "bioRxiv"
  url: "https://www.biorxiv.org/..."
---
```

Author notation:
- **Bold** lab members: `**Lyu J**`
- `&dagger;` renders as **†** = co-first author
- `&#42;` renders as **\*** = co-corresponding author

Leave out `key:` for older papers — they appear in the "Complete list of publications" section (everything sorts by `pub_date`, newest first).

### 4. When someone leaves the lab (alumni)

In their `_members/` file: add `alumni: true`, set `enddate: [YYYY-MM-DD]`, and add `current: "New position, Institution"`. They move to the **Alumni** section, sorted by leaving date.

### 5. Add a photo to the Gallery

Two steps — upload the picture, then list it:

1. Add the image file to `static/img/gallery/` (`.jpg` or `.png`; landscape works best since photos are cropped to a 4:3 thumbnail).
2. Add an entry to `_data/gallery.yml` — photos appear **in the order listed**, so put new ones where you want them:

```yaml
- image: /static/img/gallery/lab-picnic-2026.jpg   # must match the filename you uploaded
  caption: 2026 lab picnic                          # shown under the photo
```

That's it — no HTML to touch. The Gallery page builds itself from this list, and any entry whose image file is missing is skipped automatically.

---

## Local preview (optional, for larger changes)

```sh
bundle install
bundle exec jekyll serve   # then open http://localhost:4000
```

Requires Ruby 3.x. For small edits you don't need this — just open a pull request and check the deployed site.
