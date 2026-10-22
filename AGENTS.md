# Public reference implementation

This repository is public. Do not identify private consumers, projects or
organizations in issues, PRs, replies, commits, fixtures or artifacts. Use generic
technical descriptions; keep downstream adoption and delivery tracking private.
Before every external write, read `instructions/publication-privacy.md` and check
the exact outgoing payload. Apply this boundary to delegated agents too.

The installed collection entry point is `collection-AGENTS.md`; it describes its
destination rather than this repository root. Development and branch policy is
in `instructions/development-workflows.md`.

## Which repositories a task needs

A collection starts with the repository you were asked for. Add the others a
task turns out to need with `wtc add-repo`, and say why in `WTC-SCOPE.md`:

- **wtc-site** describes wtc. Work on what the site says about commands,
  install or behaviour needs **wtc-cli** beside it: read its `docs/` there
  rather than from memory, and fix the docs in wtc-cli when they are wrong.
- **wtc-cli** changes that people see (commands, flags, install) usually need
  the site updated too: add **wtc-site** when a change lands in its docs.
