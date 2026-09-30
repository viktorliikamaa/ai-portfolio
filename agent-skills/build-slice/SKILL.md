---
name: build-slice
description: Run one complete build slice from plan to commit. Use when the user says "build slice N", "next slice", or asks to implement the next step in NOTES.md. Codifies the loop context → plan → build → verify → commit → update NOTES, with explicit stop conditions where judgement is needed and you MUST ask instead of guessing.
---

# Build slice

This is the proven working loop for this project, made repeatable. You run the
**execution** on your own. You **escalate the decisions** to the user. That line is
not a limitation to work around; it is the point. Tests are ground truth. Where tests
cannot decide what is right, neither can you, and then you ask.

## The loop: run in this order

1. **Context.** Read `CLAUDE.md`, `NOTES.md` and the files the slice touches. Confirm
   which slice is next according to "Next" in NOTES.md. Do not assume. Read.
2. **Plan.** Write a plan in plan mode for ONE slice. If the plan grows beyond the
   requested slice, STOP (see below) and ask before building.
3. **Build.** One slice at a time. Follow the conventions in CLAUDE.md. No AI in the
   product code except the explicitly bounded AI calls. No agent loops, no orchestrator.
4. **Verify.** The full test suite must pass: old AND new tests together. Smoke-test new
   commands against a throwaway database in `/tmp`, NEVER the real database. Before you
   call the slice done, actively think through edge cases the tests should cover:
   foreign-key constraints, empty input, orphaned references, time zones and DST,
   duplicates. Add tests for them. "Looks done" is not a signal. Green is.
5. **Commit.** Before anything that touches data, make sure `.gitignore` excludes `.env`,
   `*.db`, cache and output directories. Commit with the message "Slice N: <short description>".
6. **Update NOTES.md.** Record what the slice delivered and what comes next.

## Stop conditions: you MUST stop and ask

- **Real personal data.** Anything that would read, write or import real client data.
- **A decision without a test signal.** If no test can tell you which option is right,
  you cannot either.
- **Anything irreversible.** Deleting data, migrating a real database, sending anything
  outside the machine.
- **Scope growth.** The plan is growing beyond the slice that was asked for.
- **Unverifiable results.** If you cannot verify something, say so. Do not guess.

When you stop: state the decision in one or two sentences, give the options with their
trade-offs, recommend one, and wait.

## When a slice is done

Report back: which files were built, the number of passing tests, the commit hash, and,
most importantly, the ONE open decision or question before the next slice, so the user
chooses the direction. Stop there. Do NOT start the next slice automatically. What gets
built next is always the user's decision.
