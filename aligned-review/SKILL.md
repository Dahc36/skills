---
name: aligned-review
description: when the user has started implementing the facts/decisions from an alignment.md and wants a progress or conformance check against it before continuing — treats alignment.md as the source of truth to check the work against, not something to review itself.
disable-model-invocation: true
---

Check the work done so far against `alignment.md`, treating that file as the agreed source of truth.

Look for `alignment.md` in the current working directory only — do not search parent directories. If it isn't there, tell me no alignment doc was found in this directory and stop; do not guess at facts or decisions.

Determine "the work so far" from git: `git diff` (staged + unstaged changes) plus untracked files from `git status`, in the current directory.

Compare that work against the Facts and Decisions in `alignment.md` and report back in plain conversational text under three headers:

- **Deviations** — changes that contradict an agreed decision
- **Scope creep** — changes touching items listed as not yet decided / deferred
- **Gaps** — decisions in `alignment.md` that the work doesn't address yet

Do not re-verify the Facts section against the live environment unless something in the diff suggests a fact has changed.

This is a report only: never edit code or `alignment.md`, and never write the review itself to a file — respond in chat.

Once the changes satisfy `alignment.md`, it should be removed.
