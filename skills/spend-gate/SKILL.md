---
name: Spend gate
description: >-
  Use this when any assistant is about to spend money, change a paid
  subscription, merge to a CI-backed production repo, change hosting or GitHub
  budgets, deploy a live origin, launch a paid remote agent, flip scheduled
  automation, rotate tokens, or generate paid media.
---
# Spend gate

Nominal spend is allowed only when all three are true:

1. The change has a **named scope** (one vendor, one repo, one service, one action).
2. The **cost surface** is stated first (which bill moves, spike vs recurring, estimated size).
3. The operator gives an explicit **YES**.

Finance owns the ledger. Do not invent invoices. Income does not loosen this gate.

## Materiality

Ledger two bands. Do not loosen Always YES. Do not change budgets without a new YES.

**Small scoped deploy (fine):** a named standard or critical-infra deploy that bills briefly and at a small unit cost. Do not stall it as if it were a spike.

**Spike (named why first):** a sudden daily jump on Actions, hosting, or a sibling meter. Name the why before it runs. State the estimate in the same message as the ask; do not hard-code dollar thresholds into the skill text.

## Always YES

- GitHub Actions budget or stop-usage change
- Production hosting change (env, start command, topology, restart, cron)
- Merge to a CI-backed production repo the operator named as live-auto-deploy
- New paid remote agent launch
- Scheduled-automation enable flip
- Token rotation
- Paid media generate
- Paid subscription change: start, cancel, upgrade, or downgrade for any recurring vendor

## Never silent

Do not merge, deploy, or change production hosting in the background. Do not flip scheduled Actions. Do not change a paid plan in the background after the operator said they will do it themselves. State the cost surface in the same message as the ask.

## No YES needed

Local tests. Own-repo work on non-production projects that does not start the named production CI or hosting bill. Read-only meter reads.

## After a YES

Record: scope, cost surface, band (small scoped deploy vs spike), who ran it, and the before/after meter if the change was meant to save money. One spend event at a time on the production surface.

## Preserve-core

Do not cancel core infrastructure the operator listed as preserve-core without a new YES. The preserve-core list lives with the operator; keep it out of this public skill body.
