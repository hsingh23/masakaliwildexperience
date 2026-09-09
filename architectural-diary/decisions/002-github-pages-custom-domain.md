# 002 — GitHub Pages + custom domain via CNAME

- **Date:** 2024-10-16
- **Commits:** 6a6be2a (Create CNAME)
- **Status:** Accepted, still in force

## Context

The site needed free hosting under the brand's own domain,
masakaliwildexperience.com.

## Decision

Serve the repository root with GitHub Pages and claim the custom domain
by committing a one-line `CNAME` file containing
`masakaliwildexperience.com`. DNS records are managed outside the repo.

## Consequences

- Zero-cost hosting with automatic deploys on every push to `main`.
- The apex domain became the canonical URL; `masakali.json` references
  images with absolute `https://masakaliwildexperience.com/images/...`
  URLs (see commit 77ac05e), so the domain and GitHub Pages are now a
  load-bearing dependency for blog images.
- Any rename of the GitHub repository relies on redirects — which
  decision 005 also depends on.
