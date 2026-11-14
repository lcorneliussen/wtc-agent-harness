---
name: taba-coordinate
description: Coordinate a scoped project through visible Herdr task collections, review, delivery, releases and authorized cleanup. Use when the user says “you are a coordinator”, “get going” in an established coordinator session, or asks to orchestrate work across collections. A status-only request uses the status skill.
---

# Coordinate a project

Read `harness/roles/coordinator.md` from the collection root. It is the shared,
agent-agnostic role contract; this skill is its entry point, not a second runbook.

1. Read `WTC-SCOPE.md`, repository instructions and the continuation pointers it
   names. Identify the current objective, authorization, holds and live owners.
2. Reconcile affected current facts and previous coordinator ownership. Do not
   resume a completed release or unpause work from historical handoff text.
3. Use the existing start, status, new/open, PR, local-review, follow, catch-up
   and retire skills for the operation at hand. Delegate ordinary work visibly
   through Herdr; verify the target agent, directory and pane before messages.
4. Keep scopes and reservations current, carry authorized work through its
   delivery checks, and maintain one concise durable continuation checkpoint.
5. Stop at verified completion or the actual authorization/dependency boundary.
   If orientation finds no unfinished objective, report that before proposing
   the next work. The role itself grants no merge, release or cleanup authority.

If this client does not discover skills, read the same role directly through
`harness/collection-AGENTS.md`; no client-specific configuration is required.
