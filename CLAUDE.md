# Intempt org rules for Claude Code

These apply to every dev and every Intempt repo. Repo-level CLAUDE.md files add to them.

## Offload bulk text work to Jev

Before reading 20 or more similar items into Claude's context (lint hits, findings, tickets, log
lines, small strings to rewrite), batch them through `jev` and read the result instead.

| Send to Jev | Keep on Claude |
|---|---|
| Per-item classification and triage | Anything that edits files or runs tools |
| First-pass rewrites of many small strings | Judgement calls a human will act on |
| Summarising long logs and CI output | Security, merge and release decisions |
| Bulk extraction to JSON | Final verification and the gates |
| Drafting test fixtures | Anything touching a secret or customer data |

- Jev output is a proposal. Spot-check it, apply it yourself, run the gates. Never commit it unread.
- No customer data, secrets or PII in a Jev prompt.
- The router picks a different model run to run. Do not use Jev where the answer has to be
  reproducible.

Setup, usage and the shared key: [`brain/ops/JEV.md`](https://github.com/intempt/brain/blob/staging/ops/JEV.md).

```bash
eval "$(brain/ops/bin/credentials.sh openrouter)"
jev "Summarise this CI log in 5 bullets" < build.log
jev batch in.jsonl out.jsonl --json --system-file rubric.txt --concurrency 12
```
