# wtc-agent-harness — read this first

You are in `harness/`, the agent harness of the **wtc-dogfood** workspace: the
worktree-collection workspace in which this pattern hosts itself. The folder
above you (`..`) is the **collection root**; its other subdirectories are the
repos in scope for this collection.

Opened on a single repo instead and want to know whether it sits in a
collection: `instructions/collection-context.md`.

## What this workspace is

`wtc-agent-harness` is a **downstream** of
[wtc-boilerplate](https://github.com/lcorneliussen/wtc-boilerplate), the
reference implementation of worktree collections. It differs from the
boilerplate only in what every downstream must add: `.harness-repos.yml`,
this file, and the harness name in `tools/lib.sh`. Everything else is the
boilerplate, and should stay recognisably so.

Two jobs, and they pull in opposite directions — name which one a change is:

1. **Dogfood.** Run the pattern on itself and on `wtc-site`, and feel the
   rough edges. A rough edge that is generic belongs **upstream**: fix it in
   the `ext.wtc-boilerplate` sibling, open a PR on wtc-boilerplate, and port
   it here once merged. A fix that lands only here is a fork drifting.
2. **Build the site.** `wtc-site` is the product. Site work follows the same
   collection-per-task rule as any product repo; it is not a place to keep
   harness experiments.

| Repo | Sibling dir | What it is |
|---|---|---|
| `wtc-agent-harness` | `harness/` | this repo — tools + instructions, downstream of the boilerplate |
| `wtc-site` | `wtc-site/` | the official Worktree Collections site. Empty seed — stack undecided |
| wtc-boilerplate | `ext.wtc-boilerplate/` | **upstream**, unmanaged: not in the registry, owned by a clone outside the workspace |

The authoritative list is `.harness-repos.yml`. The workspace root is
`~/Code/wtc-dogfood`; its herdr session is `wtc-dogfood`
(`instructions/herdr.md`).

## Upstream and downstream

- **Generic → upstream first.** Tools, instructions, skills: if a change would
  make sense in any workspace, it is a wtc-boilerplate PR made from
  `ext.wtc-boilerplate`, then a port here. Say so in the commit that ports
  it (`port: wtc-boilerplate#<n>`).
- **Upstream is public.** Before any write to wtc-boilerplate — issue, PR,
  comment, commit — read `instructions/publication-privacy.md` and check the
  exact payload. Name no private consumer, this workspace included.
- **Specific → here.** The registry, this file, the site's own hooks.
- **Ports are by hand.** The bare has no `upstream` remote; the `ext.`
  sibling's history is how upstream commits are reached. Cherry-pick or
  re-apply, and keep the diff to the boilerplate small enough to read.

## State lives in git

A collection carries **no durable state that is not in git**. Deleting one
must lose nothing — that is what makes it cheap to create one per task.

- Findings, decisions, and follow-ups become commits, PR comments, or GitHub
  issues. Not notes in the collection folder.
- `HANDOFF.md` at the collection root is an **ephemeral launch note**: the
  first agent reads it, moves anything durable into issues/commits,
  transcribes the scope into `WTC-SCOPE.md`, and **deletes it as its first
  action** (`/wtc-start`).
- `AGENTS.md` at the collection root is a **symlink** to
  `collection-AGENTS.md` here, made by `link-skills.sh`. Never hand-edit
  the link.
- `WTC-SCOPE.md` is seeded once from `collection-SCOPE.md` and then
  hand-authored. It dies with the collection. Never overwrite an existing one.
- `.env.collection`, `mise.toml`, `.mcp.json`, `.claude/skills/`,
  `.agents/skills/` at the collection root are **generated**. Regenerate,
  never hand-edit. `.env.collection.local` is the hand-authored exception, and
  still dies with the collection.

## Branch and PR policy

Full policy: `instructions/development-workflows.md`. The short version:

1. Worktrees rest **detached at `origin/main`**. That is healthy, not broken.
2. Create the branch **at the first commit**, not before:
   `git switch -c <slug>`.
3. PR into `main`, merge with a **merge commit** — never squash, never rebase.
4. After merge the branch is finished. The remote branch is kept as the
   record; the local ref is disposable and catch-up prunes it.

Bring-up exception, per the policy: while the workspace is being stood up,
harness bring-up commits go straight to `main`. That window closed with the
first collection; everything since is a PR.

## Issues

Issues and PRs live on **GitHub**, reached with `gh`; there is no in-repo
file-based tracker. No repo sets `issues_prefix`, so `branch-off.sh --issue`
has nothing to route. Use a plain slug (`tools/branch-off.sh <slug> …`), and
put the GitHub issue link in `WTC-SCOPE.md` and the PR body.

## Skills

The `wtc-*` skills in `skills/` are the recurring collection procedures —
`/wtc-start`, `/wtc-status`, `/wtc-new`, `/wtc-add-repo`, `/wtc-catch-up`,
`/wtc-pr`, `/wtc-draft-pr`, `/wtc-follow`, `/wtc-browse`, `/wtc-retire`. They are linked
into every collection root by `link-skills.sh`. Prefer one over ad hoc shell.
