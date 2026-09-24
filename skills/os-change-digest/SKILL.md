---
name: OS change digest
description: >-
  Use this when summarizing recent commits, PRs, releases, or RSS/site updates
  across an operating set of repos and public websites. Default output is a
  magazine (day or week edition), not a raw inventory. Read-only. Do not merge
  or deploy from a digest.
---
# OS change digest

Use when the operator wants to stay on top of what moved: commits, pull requests, releases, and public site or RSS updates.

This skill is read-only. It does not merge, open PRs, deploy, or change live files.

The operator consumes this as a **magazine**, not as an inventory. Probe first. Then write the magazine. Do not dump the probe.

## Edition

- **Day** — last 24 hours, or since the last morning issue. Monday–Thursday default.
- **Week** — last 7 days. Friday morning default, or when the operator says "the week."

Say the edition and the window in the masthead.

## 1. Name the set

1. Surface set: the operator's current map, or the surfaces named this run.
2. If no map is named, ask for the repo and site list. Do not invent extra repos.

Use placeholders until the operator names concrete surfaces:

Repos:

- `<your-repo>` (repeat for each repo in the set)

Public sites:

- `<your-site>` (repeat for each origin in the set)

Add a sibling site only if the operator named it this run.

## 2. Probe live. Do not recall.

Do not write a SHA, PR number, merge state, or "shipped" line from memory.

For each repo, live-read:

- Open PRs: number, title, author, updated, draft or not
- Merged PRs in the window
- Commits on the default branch in the window: SHA (short), subject, date
- Releases or tags in the window

Prefer the GitHub CLI or the GitHub API. If those fail, use the public Atom feeds:

- `https://github.com/{owner}/{repo}/commits/{branch}.atom`
- `https://github.com/{owner}/{repo}/releases.atom`

If a probe fails, mark that surface `UNMEASURED`. Do not fill the gap.

For each site, live-read in this order:

1. A changelog, Insights, or news index if one exists
2. RSS or Atom (`/feed`, `/rss.xml`, `/atom.xml`, `/feed.xml`)
3. Sitemap `lastmod` only as a last resort, and only to say "pages changed," not what they said

A site with no feed and no changelog is `UNMEASURED` for content. You may still report HTTP status if you fetched the homepage.

## 3. Classify. Do not promote.

- **Merged** — on the default branch, or a PR with a merge commit you saw
- **Open** — PR not merged
- **Draft** — draft PR or local note, not shipped
- **Released** — a tag or GitHub release you saw
- **Site** — a public page or feed item you fetched
- **Advisory** — reported by another agent, cached, or projected. Not wire-probed this run

Advisory findings must not headline the magazine as done, live, or measured.

Do not treat a stale watch card, an unmerged PR, or a Pages preview as a production ship.

## 4. Holds

- Do not mint a new public protocol from a magazine. Report only against protocols the operator already named.
- A proof or demo site is not a protocol unless the operator says it is.
- Keep internal OS notes out of a public-facing magazine title.
- No prices. No invoice language.
- Do not deploy hosting or a production origin from this skill.
- Spend: a digest is free. If a later step would spend, stop and run the spend-gate skill.
- Treat vault or private recall repos as clerk notes only. Say "vaulted" only when you saw the commit on that named private repo.

## 5. Write the magazine

Write for a person who will read this with coffee. Short. Prose first. Collapse routine commits into the story they belong to.

### Masthead

Title (`OS Day` or `OS Week`), dates, surfaces probed, surfaces `UNMEASURED`.

### Lede

One short paragraph. The story of the window. Not a list. If nothing moved, say so and stop after Quiet.

### The ship

Releases, merged work, and live site publishes that changed a public protocol or a public page. A few items, not every commit. One or two sentences each. Identifier in the sentence (tag, PR, URL).

### Still open

Open and draft PRs only. One line each. Product PRs above docs. Drafts last.

### On the wire

Dated public Insights, changelog, or RSS items. If a site has no date, do not invent one.

### The clock

A compact timeline of the load-bearing events only. Week edition always includes it. Day edition includes it only when more than three items moved.

### Quiet

`UNMEASURED` and truly silent surfaces. One short box. A uniform sitemap `lastmod` is not news.

### One decision

Zero or one. Only if something is waiting on a named YES. If none, omit the section.

Do not paste diffs. Do not write a play-by-play of CI. Do not invent authors or dates.

## 6. Schedule

A weekday morning routine may run this skill: Monday–Thursday as **Day**, Friday as **Week**. Keep repo lists and delivery hour in the routine. Keep this skill generic.
