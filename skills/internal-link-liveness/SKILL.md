---
name: Internal link liveness
description: >-
  Use this when a crawl or HTML dump must fail pages that link to 404, 410, or 5xx
  internal URLs.
---
# Internal link liveness

Use this when checking a site crawl or rendered HTML dump for internal links to dead URLs.

## Law

A rendered page must not emit an internal `href` whose target returns 404, 410, or 5xx.

If the target is unpublished, omit the link or emit a typed absence. Do not keep the dead `href`.

200 + noindex is a different law (junk / unknown corridor). This skill is only non-200 targets.

## Steps

1. Take one URL spine with status codes (Screaming Frog internal HTML export or equivalent).
2. Mark every address with status not in {200} as dead.
3. Count unique inlinks and total inlinks to each dead address.
4. From rendered HTML (or the crawl outlink table), list every source page that points at a dead address.
5. Split sources into indexable vs noindex.
6. Report: dead URL, status, unique inlinks, source count, worst sources.
7. Fail the review if any indexable source links to a dead URL.
8. Do not invent a replacement URL. Do not write production links in the audit.

## Done when

The report lists every dead target and every indexable source that links to it. No new hrefs were added.
