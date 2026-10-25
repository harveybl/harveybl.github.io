# harveybl.github.io — repository index

Plain-markdown orientation. **This repository is PUBLIC**; this file deliberately contains only information already in the public README and files. Based on `main` at `3b26f7b` (2026-06-08).

## Purpose
GitHub user-pages site. Per `README.md`, it hosts a Tesla Fleet API partner **public** key (intentionally public) for domain verification, plus an Apple App Site Association file and a SAFE Budget Plaid OAuth redirect page.

## Structure
| Path | What |
|---|---|
| `index.html` | Site root page |
| `.well-known/apple-app-site-association` | Apple universal-link association |
| `.well-known/appspecific/com.tesla.3p.public-key.pem` | Tesla Fleet API partner public key (public by design) |
| `safebudget/plaid-oauth/index.html` | OAuth redirect landing page |
| `.nojekyll` | Makes GitHub Pages serve `.well-known/` |
| `README.md` | Authoritative description |

## Build and test
No build step, no tests. Static files served by GitHub Pages.

## CI/CD
No CI configuration found. Deployment is GitHub Pages from `main` (assumed from the repo name; not verified).

## Recent notable changes
- 2026-06-08: Add Apple App Site Association and SAFE Budget Plaid OAuth redirect page.
- 2026-05-01: `.nojekyll` instead of `_config.yml` so `.well-known` is served; Tesla Fleet API partner public-key endpoint added.
