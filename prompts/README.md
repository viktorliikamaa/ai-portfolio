# Prompt templates

Prompts I use when an AI agent works on something that matters: a live system, real data, or a question where a confident wrong answer is expensive.

| Template | Use it when |
| --- | --- |
| [Read-only audit brief](read-only-audit-brief.md) | Something performed badly and you need to know *why* before changing anything |
| [Safe change to a live system](safe-live-change.md) | You want one bounded change to a running system, with proof first |

## Patterns they share

- **Declare the task type up front** (`ANALYZE`, `FIX`, `BUILD`) so the agent knows whether it may change anything.
- **Read-only by default.** Permission to change things is granted per part, and only after the read-only part has confirmed what it needs to.
- **Hypotheses before evidence.** Candidate explanations are written down first and judged with numbers, so the agent can't build a story around whatever it finds first.
- **"Numbers only, no fixes proposed."** Diagnosis and treatment are separate steps.
- **Explicit STOP rules.** If a precondition fails, the agent reports and stops instead of improvising.
- **One change per task.** Everything else is listed as out of scope.
