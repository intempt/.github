# Agent rules for every Intempt repository

This file is the public pointer. The rules themselves live in the private `intempt/brain` repo at
`engineering/AGENT_RULES.md`, and `brain/install.sh` imports them into every developer's
`~/.claude/CLAUDE.md`, so they load in every Intempt repository without each one copying them.

```bash
cd ~/Intempt/brain && git pull && git-crypt unlock && ./install.sh --role <yours>
```

## Bulk work goes to Jev, not to Claude

Ruled 2026-10-05. When a task means judging, classifying, scoring or rewriting 20 or more similar
items (lint hits, review findings, CI log lines, recipes, submissions, tickets, rows), send them to
TypeSafe Jev on OpenRouter with `brain/ops/bin/jev` and read the summary back, instead of reading
every item into Claude's context.

| Use | Command |
|---|---|
| Classify, gate, verify, score | `jev decide` / `jev decide-batch` |
| Bulk rewrites, extraction, summaries | `jev chat` / `jev chat-batch` |

Claude keeps file edits, tool runs, merge and security decisions, and final verification. Jev's
output is a proposal: read it, apply it yourself, and run the repository's checks. Never commit Jev
output unread.

The OpenRouter key is never committed to any repository other than `intempt/brain`, where it is
encrypted with git-crypt. Do not paste it into code, a workflow or this public repository.
