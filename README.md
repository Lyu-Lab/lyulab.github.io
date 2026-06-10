# lyulab.org

Website for the Lyu Lab (Evnin Family Laboratory of Computational Molecular Discovery) at The Rockefeller University. Built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages. The structure is adapted from the [Fraser Lab website](https://github.com/fraser-lab/fraser-lab.github.io).

## Local development

```sh
bundle install
bundle exec jekyll serve
```

The site is then served at [localhost:4000](http://localhost:4000).

## Editing content

- **People** — add or edit a Markdown file in `_members/`. The `order:` field controls display order; set `image:` to a photo in `static/img/members/` (365 × 365 px). Members without a photo fall back to a placeholder.
- **Publications** — add a Markdown file in `_publications/`. Bold lab authors with `**Name**` and mark equal contribution with `&#42;`. Optional `image:` and `links:` fields.
- **Research / Positions / Contact** — edit the Markdown in `research/`, `join/`, and `contact/`.
- **Navigation** — edit `_data/navigation.yml`.

The custom domain is set in `CNAME` (lyulab.org).
