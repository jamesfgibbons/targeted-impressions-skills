---
name: JSON-LD RFC 8259 check
description: >-
  Use this when encoding or evaluating JSON-LD that must survive a single HTML
  unescape and still parse as RFC 8259 JSON (Google's documented behavior).
---
# JSON-LD RFC 8259 / single-unescape

Use when adding or evaluating search-profile checks for JSON-LD that must survive Google's single HTML unescape.

## Law

Google applies **one** HTML unescape to each `application/ld+json` block, then parses JSON ([RFC 8259 §7](https://datatracker.ietf.org/doc/html/rfc8259#section-7)). Double-escaped entities (`&amp;`, `&#…`) no longer unroll. Compliant sink: `JSON.stringify` then `\u003c` `\u003e` `\u0026` (or standard JSON escapes). Never HTML-entity-encode JSON-LD fields.

This is relevance to a dated platform change (Google, 2026-08-21). Do not say or imply Google named your project.

## Catalog check (example shape)

Use a stable check id in your own catalog. Do not confuse an alias with the canonical id.

```
check_id: search.jsonld.strict_parse
alias: search.structured_data.jsonld_rfc8259
profile: search
title: JSON-LD survives a single HTML unescape as RFC 8259 JSON
authority_refs: [rfc8259_section_7, google_jsonld_single_unescape]
governing_invariant: schema_publishable
required_evidence: [observations.search.jsonld.strict_parse]
applicability: observations.search.jsonld.present == true
evaluation: equals true
evidence_scope: public_static
mutation_class: pure_read
certification_eligible: true
remediation: Serialize at the render sink with JSON escapes or \uXXXX. Do not HTML-entity-encode fields.
```

- Present + valid after one unescape, no stacked entities → **PASS**
- Present + invalid or stacked entities → **FAIL**
- No static JSON-LD → **NOT_APPLICABLE** (do not invent a fail)
- Collector could not read the page → **UNMEASURED**

## Collector

From public HTML only (quick mode): extract every `application/ld+json` block, unescape once, parse as JSON, scan string values for `&amp;|&lt;|&gt;|"|&#`. Do not use a second unescape. Do not treat a literal `&` in a JSON string as a failure.

## Eat-first

Before any public claim, fetch the live public corpus with HTTP GET only. Paths that return 400+ are UNMEASURED unless a public sitemap lists them. Do not mutate production from this skill.

## Holds

Do not merge or deploy from this skill. A catalog change lives in the protocol repo that owns the check definitions (for example [Constitutional CMS](https://github.com/jamesfgibbons/constitutional-cms)); the public `/check` collector lives in that project's site repo. Draft PRs need an explicit YES and a stated cost surface. Press drafts only after a real self-receipt exists.
