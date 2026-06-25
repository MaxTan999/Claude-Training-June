# Sterling &amp; Vale Advisory

A single-page static website for **Sterling &amp; Vale Advisory** — fiduciary, long-term wealth management for professionals and families.

The site is built as a **lead-magnet landing page**: its single goal is to get qualified
visitors to claim a free **"Wealth Health Check"** by submitting the enquiry form. It uses
a purple-themed visual identity (deep aubergine + champagne-gold accents) with Fraunces and
Inter typography.

The entire site is a self-contained [index.html](index.html) (HTML + inline CSS + vanilla JS, Google Fonts, no build step).

![Sterling & Vale Advisory — homepage screenshot](assets/screenshot.png)

## Live site

Deployed via GitHub Pages:

**https://maxtan999.github.io/Claude-Training-June/**

## Features

- **Lead-magnet hero** with an offer card (free Wealth Health Check) and trust stats.
- **Mid-page conversion banner** and a benefit-driven enquiry form with a "what happens next" 3-step.
- **Enquiry form** posts via [FormSubmit](https://formsubmit.co) AJAX — submissions are
  emailed to the site owner. (FormSubmit needs a **one-time activation**: the first
  submission triggers a confirmation email; click its link and the form works thereafter.)
  Includes inline validation and a honeypot anti-spam field.
- **Auto-rotating testimonial carousel**, scroll-in reveal animations, sticky nav, responsive/mobile menu.
- **SEO**: optimised title/meta description, canonical, Open Graph & Twitter cards, and
  `FinancialService` JSON-LD structured data (incl. the free-offer markup).
- **Accessibility/quality floor**: keyboard focus styles, reduced-motion support, ARIA labelling.

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
├── index.html                       # The complete static lead-magnet site
├── README.md                        # This file
├── assets/screenshot.png            # Homepage preview
├── .github/workflows/deploy.yml     # GitHub Pages deploy workflow
└── .claude/
    ├── product-marketing.md         # Marketing context (read by the seo-audit skill)
    └── skills/                      # Project-level Claude Code skills
        ├── frontend-design/         #   (from anthropics/skills)
        └── seo-audit/               #   (from coreyhaines31/marketingskills)
```
