---
description: Security-scan, update the README, push to GitHub, and deploy to GitHub Pages
argument-hint: "[optional commit message]"
---

# /githubupdate

Run a safe, end-to-end publish of this repository to GitHub. Perform the steps **in this order** and **stop immediately** if the security scan (Step 1) finds anything sensitive — do not push until the user resolves it.

Git on this machine is installed at `C:\Program Files\Git\cmd`. If `git` is not on PATH in the shell, prepend it for the session:
`$env:Path = "$env:ProgramFiles\Git\cmd;" + $env:Path`

Optional commit message from the user: **$ARGUMENTS** (if empty, write a concise, descriptive message based on the actual changes).

---

## Step 1 — Security scan (BLOCKING, do this first)

Before anything is pushed, scan the working tree for secrets and sensitive information. **This is a gate: if anything credible is found, STOP and report it to the user. Do not commit or push.**

1. Determine what will be published — the tracked files plus anything currently staged/modified (`git status`, `git diff`). Pay special attention to files that would be newly added.
2. Scan those files (use Grep over the repo) for sensitive patterns, including but not limited to:
   - API keys / tokens: `api[_-]?key`, `secret`, `token`, `bearer`, AWS keys (`AKIA[0-9A-Z]{16}`), GitHub tokens (`ghp_`, `gho_`, `ghs_`, `github_pat_`), Google API keys (`AIza[0-9A-Za-z_\-]{35}`), Slack (`xox[baprs]-`), Stripe (`sk_live_`, `pk_live_`), private keys (`-----BEGIN (RSA |EC |OPENSSH |PGP )?PRIVATE KEY-----`).
   - Credentials: `password\s*[=:]`, `passwd`, connection strings (`mongodb://`, `postgres://`, `mysql://` with embedded credentials), `.env`-style `KEY=value` secrets.
   - Personal/sensitive data: hardcoded emails, phone numbers, internal hostnames/IPs that shouldn't be public.
   - Sensitive files that should never be committed: `.env`, `.env.*`, `*.pem`, `*.key`, `*.pfx`, `id_rsa`, `credentials.json`, `*.keystore`, service-account JSON, `.npmrc`/`.pypirc` with tokens.
3. Ensure a `.gitignore` exists and covers the common sensitive files above. If it is missing or incomplete, create/update it (do not delete entries the user already has).
4. **If anything credible is found:** stop, clearly list each finding with its file and line, recommend a remediation (remove the value, move it to an untracked `.env`, add to `.gitignore`, rotate the secret if it was ever committed), and ask the user how to proceed. Do **not** continue to later steps.
5. If the scan is clean, say so briefly and continue.

## Step 2 — Create / update the README

- If `README.md` is missing or is just a placeholder, create a proper one.
- If it exists, update it so it accurately reflects the current project: what it is, how to run/preview it locally, the live site URL, and how deployment works.
- Keep it concise and accurate — do not invent features that don't exist.

## Step 3 — Ensure the GitHub Pages deploy workflow exists

- Confirm `.github/workflows/deploy.yml` exists and deploys this project to GitHub Pages via GitHub Actions (trigger on push to the default branch + `workflow_dispatch`, with `pages: write` and `id-token: write` permissions, using `actions/configure-pages`, `actions/upload-pages-artifact`, and `actions/deploy-pages`).
- If it is missing, create it (for a static site, publish the repo root / the directory containing `index.html`).
- Remind the user that GitHub Pages must have its **Source set to "GitHub Actions"** in repo Settings → Pages — this is a one-time manual setting only a repo admin can change.

## Step 4 — Commit and push to GitHub

- Stage the changes, commit (using `$ARGUMENTS` if provided, otherwise a descriptive message), and `git push` to the `origin` remote on the default branch.
- If there is no `origin` remote yet, stop and ask the user for the GitHub repository URL before pushing.

## Step 5 — Verify deployment

- The push triggers the Pages workflow. Verify the result via the public GitHub API (no `gh` CLI required):
  - Latest run: `https://api.github.com/repos/<owner>/<repo>/actions/runs?per_page=1` → check `status`/`conclusion`.
  - Live site: fetch the Pages URL and confirm `HTTP 200`.
- Report the workflow conclusion and whether the live site is reachable. If the run failed, read the failed job's steps and explain the cause + fix.

## Final report

Summarize: security scan result, what changed in the README, push status (commit SHA), workflow conclusion, and the live site URL.
