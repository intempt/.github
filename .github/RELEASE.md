# Releasing

Promotions to `main` are bot-only. No human posts an approving review.

- **Robot (standard):** ro-bot reviews or runs a staging test, then approves; `ff-merge` → FF_BOT fast-forwards `main`.
- **Admin (blu-bot):** an admin labels the PR `admin-release`; `blu-bot` waits for CI green, approves, merges to staging, approves the `staging -> main` PR, and labels `ff-merge` → FF_BOT fast-forwards `main`. No ro-bot.

`main` is advanced only by FF_BOT. The full standard, provenance, and privileges are in
`brain/engineering/ops/release/promotion-approval.md`.

_Validated: blu-bot full admin pipeline, 2026-11-08._
