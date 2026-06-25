# Product Marketing Context — Sterling & Vale Advisory

> Read automatically by the **seo-audit** skill (and other marketing skills) before
> asking discovery questions. Keep this current.

## Business
- **Name:** Sterling & Vale Advisory
- **Type:** Private wealth-management / financial-advisory firm (local-business + service site, single landing page at `index.html`).
- **Audience:** Professionals and families with investable assets who want calm, fiduciary, long-term advice.

## Primary goal — this is a LEAD-MAGNET site
The single business goal is **lead generation**: get qualified visitors to submit the
enquiry form. Treat the form as the conversion event for every recommendation.

- **Lead magnet / offer:** a free, no-obligation **"Wealth Health Check"** — a
  personalised review prospects claim by submitting the enquiry form.
- **Form delivery:** submissions are emailed to **isaiah.hui@redbeaconam.com** via the
  FormSubmit AJAX endpoint in `index.html`. When auditing, verify this endpoint is live
  (FormSubmit requires one-time email activation on first submit).
- **Conversion-first lens:** when auditing SEO, also flag anything that weakens the path
  to a form submission (weak CTAs, buried form, unclear offer, friction in fields). See
  the **cro** skill for deeper conversion work.

## Priority keywords / topics
- private wealth management, fiduciary financial advisor, retirement planning,
  portfolio management, estate planning, "free wealth health check / portfolio review".

## Brand
- **Theme:** purple — deep plum/aubergine primary with a champagne-gold accent for CTAs.
- **Tone:** premium but approachable; clear, unhurried, jargon-free; trustworthy.
- **Type:** Fraunces (display serif) + Inter (body).

## Notes for auditors
- Single-page SPA-style site → on-page + technical SEO matter more than crawl-budget/i18n.
- Not multilingual; skip the international-SEO checks unless that changes.
- Schema is hand-authored JSON-LD in static HTML, so `web_fetch` CAN see it here
  (the usual JS-injection caveat does not apply to this site).
