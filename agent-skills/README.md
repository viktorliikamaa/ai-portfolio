# Agent skills

A *skill* is a set of written instructions a coding agent (here, Claude Code) loads when a task matches. It turns a way of working into something repeatable.

## build-slice

[`build-slice/SKILL.md`](build-slice/SKILL.md) codifies the loop I use to build software with an AI agent: context → plan → build → verify → commit → report.

Anyone can write down *how* to build. The part that matters is **when the agent must stop building and ask a human**. The stop conditions came from the exact moments in earlier sessions where I had to step in.

I first wrote it for the [sales CRM](../projects/sales-crm/) and later reused it, unchanged except for its trigger description, on a real-time on-chain data recorder. There, it made the agent escalate repeated data problems instead of quietly working around them. That led to a full architecture pivot and a recorder with 77 passing tests.

**A note on limits:** a skill is advisory. The agent is told what to do; nothing enforces it. For a rule that must never be broken, such as "never place a real trade", use a hard technical guard (a hook), not an instruction.
