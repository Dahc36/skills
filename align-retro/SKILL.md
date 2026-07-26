---
name: align-retro
description: reverse-engineers the facts/decisions implied by changes made before any alignment doc existed, confirms them, and only then writes alignment.md.
disable-model-invocation: true
---

Read `~/.claude/skills/align/SKILL.md` — that's the interview process this skill builds on, and everything below assumes that context. One exception: ignore the instruction to always produce `alignment.md` at the end; that step is conditional here.

If `alignment.md` already exists in the current working directory, refuse — this skill is only for the "no alignment doc yet" case. Tell me to use `aligned-review` instead and stop.

Determine "the work so far" from git: `git diff` (staged + unstaged changes) plus untracked files from `git status`, in the current directory.

From that work, infer the apparent facts and decisions — what `alignment.md` would probably have said if it had been written before the changes. Then run the same interview process from `align`: one question at a time, waiting for feedback before continuing, facts looked up directly rather than asked. For each question, use the inferred value as the recommended answer, but still ask every one explicitly — never silently accept an inferred decision just because the code already does it.

Once every decision is confirmed:

- If the confirmed decisions match what the code already does, don't create `alignment.md` — just tell me conversationally that things line up.
- If anything diverges, create `alignment.md` in the same format a normal `/align` session would produce (Facts, Decisions, and any deferred items) — reflecting the _confirmed_ decisions, not annotated with the mismatches. Report the specific mismatches separately, conversationally, in chat — never write them into the file.

This skill never edits existing code, only ever decides whether to write `alignment.md`.
