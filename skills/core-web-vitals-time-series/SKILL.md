---
name: Core Web Vitals time series
description: >-
  Use this when measuring or tracking Lighthouse and field Core Web Vitals
  across public sites over time.
---
# Core Web Vitals time series

Use this when taking or comparing Lighthouse lab scores and field Core Web Vitals across a set of public origins, especially for a repeating benchmark.

## What to collect

Two layers, never mixed:

1. **Field CWV (CrUX)** — real-user LCP, INP, CLS (p75 + rating) at origin scope. This is the compliance number.
2. **Lab Lighthouse** — performance, accessibility, best-practices, SEO (0–100) plus lab LCP / CLS / TBT. This is the deploy-regression number.

Do not treat a lab score as Core Web Vitals.

## How to collect

- Do **not** call the PageSpeed Insights API unless a named key with quota exists. Anonymous PSI quota is often 0.
- **Lab:** local Lighthouse against system Chrome, mobile first, one URL at a time:

```
npx --yes lighthouse URL \
  --chrome-flags="--headless --no-sandbox --disable-gpu" \
  --only-categories=performance,accessibility,best-practices,seo \
  --form-factor=mobile --screenEmulation.mobile \
  --throttling-method=simulate --quiet --output=json --output-path=PATH
```

- **Field:** Chrome UX Report or the pagespeed.web.dev UI (not the API). If field data is missing, record `MISSING` — do not invent.

## Cohort

Homepages of every public marketing origin, plus one inner template per site (article, tool, or detail page). Skip APIs, noindex hosts, and parking landers. Use `<your-site>` until the operator names concrete origins.

## History

Append one JSON snapshot per run (ISO date in the user timezone) with: url, form_factor, perf, a11y, bp, seo, lab_lcp_ms, lab_cls, lab_tbt_ms, field_lcp, field_inp, field_cls, field_overall, source, run_id.

Keep a CSV of the same rows. Never overwrite old snapshots.

## Reporting

- First run: show the table.
- Later runs: only surface **regressions** (perf drop ≥10, a CWV metric flipping out of Good, or a newly failed origin). Green repeats stay quiet.
- Never merge, deploy, or launch a paid remote agent from this skill.

## Cadence

Weekday lab is enough to catch deploys. Field CrUX is a ~28-day window; do not over-interpret day-to-day field movement.
