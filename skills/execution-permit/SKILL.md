---
name: Execution permit
description: >-
  Use this when interpreting authorization or about to mutate, merge, wire,
  deploy, or schedule.
---
# Execution permit

Use this when any assistant is about to mutate code, merge, wire production, set a secret, deploy, schedule a job, or treat spoken/prose instruction as authorization.

## Law

Ordinary prose is never authorization. These are CONTEXT, EVIDENCE, RECOMMENDATION, STATUS, or SPECIFICATION, not permission: "next we should", "when ready", "proceed", "execute if", "you can begin after review".

Only a machine-readable block authorizes a mutation:

```yaml
kind: EXECUTION_PERMIT
decision: YES
```

Permissions are non-transitive. Unnamed verbs are denied.

inspect does not imply edit.
edit does not imply commit.
commit does not imply push.
push does not imply open_pr.
open_pr does not imply merge.
merge does not imply apply_ddl.
apply_ddl does not imply deploy.
deploy does not imply run_job.
run_job does not imply schedule.

## One work order, one role, one repository

A session may be reviewer, builder, verifier, carrier, or operator. It may not silently change role.

A reviewer may read, query, run tests, inspect an exact head, and write a review receipt. A reviewer may not edit, commit, push, open a repair PR, apply a migration, set a secret, or send a notification. On P1 or P2: emit HOLD, name findings, name exact head, stop.

The same model may later act as builder only in a new session, a new work order, a write-capable credential context, a distinct branch, and a new operator permit.

## Rehydration

After context compaction, session restart, agent handoff, model change, or worktree change, reload the active permit from a durable source and print its hash before any write-capable tool call. Until that succeeds, mode is READ_ONLY. There is no "I remember what was wanted."

## Exact states

Use only: LOCAL_CANDIDATE, PR_OPEN, CI_GREEN, REVIEW_CLEAN, MERGE_AUTHORIZED, MERGED, WIRED, HEARTBEAT_PROVEN, BREACH_PROVEN, DRILL_PROVEN, WIRE_PROVEN.

Do not say done, landed, all good, reviewed, or tested unless followed by exact state and exact identity.

A PR is merge-eligible only when current_head = CI_head = reviewed_head = authorized_head.

## Before every mutating tool

Classify the effect. Assert the permit is current, allows the verb, repository, branch, and paths, and no stop condition is triggered. Record the attempt. If no EXECUTION_PERMIT with decision YES is loaded, stop and return one HOLD decision packet.
