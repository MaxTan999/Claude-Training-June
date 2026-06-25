# Sterling &amp; Vale Advisory

A single-page static website for **Sterling &amp; Vale Advisory** — calm, trustworthy long-term wealth management for professionals and families.

The entire site is a self-contained [index.html](index.html) (HTML + inline CSS, Google Fonts, no build step).

![Sterling & Vale Advisory — homepage screenshot](assets/screenshot.png)

## Live site

Deployed via GitHub Pages:

**https://maxtan999.github.io/Claude-Training-June/**

## Local preview

No tooling required — just open the file in a browser:

```powershell
start index.html
```

Or serve it locally (optional, e.g. for correct relative paths):

```powershell
python -m http.server 8000
# then visit http://localhost:8000
```

## Deployment

Deployment is fully automated with GitHub Actions — see [.github/workflows/deploy.yml](.github/workflows/deploy.yml).

- Every push to `main` (or a manual **Run workflow**) triggers a deploy.
- The workflow uploads the repository root and publishes it to GitHub Pages.

### One-time setup

In the repository **Settings → Pages → Build and deployment**, set **Source** to **GitHub Actions**.

## Project structure

```
.
├── index.html                    # The complete static site
├── README.md                     # This file
└── .github/workflows/deploy.yml  # GitHub Pages deploy workflow
```
