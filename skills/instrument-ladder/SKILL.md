---
name: Instrument ladder
description: >-
  Use this when claiming that a change shipped, was fetched, indexed, cited, or
  used. Strength of a reading is only as strong as the rung beneath it.
---
# Instrument ladder

Use this when you need to state how far a change has traveled from merge to real-world use. Pair with the identity: **MERGED ≠ SHIPPED ≠ SERVED ≠ USED**.

A reading is only as strong as the rung beneath it. Do not skip rungs. Do not treat a higher rung as proven when a lower one is missing or mismatched.

## The five rungs

1. **Served** — the server returned the page. Evidence is a log line (or equivalent access record) for that URL, status, and time.
2. **Fetched by a known agent** — a known crawler or agent fetched it. Verify by IP (and ASN when needed), not by a user-agent string alone.
3. **Indexed** — the search engine reports the URL as indexed (or present in its index view). Engine say-so, not your hope.
4. **Cited** — an answer engine names or quotes it in a generated answer. Capture the citation surface and time.
5. **Used** — a person clicked, read, or acted. Human engagement, not bot traffic.

## Match served build to merged commit

When you call a change shipped:

1. Read the build id (or equivalent) the **served** page itself reports.
2. Match that build id to the **merged** commit on the default branch.
3. Only then follow the same URL to the crawler that fetched it and the search results it earned.

If the served build id does not match the commit you merged, you have not shipped that commit. Stop and say so.

## Exclude internal traffic

Before counting Fetched, Indexed, Cited, or Used:

- Exclude internal traffic by IP and ASN.
- Exclude known probe user agents (health checks, your own monitors, CI fetchers).
- Do not promote internal or probe hits to any rung above Served.

## Holds

- Merged is not shipped. Served is not used.
- User-agent strings are hints, not identity. Prefer IP/ASN allowlists for known agents.
- Do not invent index or citation status. If a probe fails, mark `UNMEASURED`.
- Do not merge or deploy from this skill. It classifies evidence; it does not change production.

## Done when

Each claim names its highest proven rung, the evidence id (log line, IP match, engine report, citation, or human event), and the matched served-build ↔ merged-commit pair when the claim is about a specific change.
