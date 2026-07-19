# omp-workflow

Plan → Execute → Review workflow for omp / OhMyPi.

- `/plan <task>` — investigates the codebase with the `planner` agent (Opus 4.8, read-only) and writes a plan to `.omp/plans/<slug>.md`
- `/execute <slug>` — implements the plan with the `executor` agent (Sonnet 5, full tools)
- `/review <slug>` — adversarially audits the diff against the plan with the `reviewer` agent (Opus 4.8, read + test execution)

## Install

```bash
omp install github:<you>/omp-workflow
```

Installs at user scope by default, so it's available in every project without per-repo setup. For a repo that needs a different variant, install with `--scope project` in that repo only — it shadows the user-scoped version there.

## Before you rely on this

This was written against the general Claude-Code-compatible plugin/agent
schema that OMP's docs describe (`description`, `model`, `tools` frontmatter
on agents; `description` + `$@` on commands; `name`/`description` on
skills — the skill and command formats are confirmed against omp.sh docs).
**Agent frontmatter field names can vary between OMP forks.** Before your
first real run:

1. Open one of the 8 bundled agents under `~/.omp/agent/agents/` (or your
   fork's equivalent directory) and compare its frontmatter to
   `agents/*.md` here. Adjust field names if they differ.
2. Run `omp -p '/extensions'` after installing to confirm the plugin and
   all three agents/commands loaded.
3. Try `/plan <a small task>` first and check the output lands in
   `.omp/plans/` before trusting `/execute` or `/review` on anything real.

## Notes

- `/execute` currently always uses the executor agent's default model
  (Sonnet 5). See the comment in `commands/execute.md` for how to route
  trivial-tagged steps to a lighter model once you've confirmed your
  fork's model-override flag.
- Nothing in this repo should ever contain credentials — those stay
  per-machine (`omp login` / provider env vars), not in the plugin.
- If your wiki needs authentication, connect it as an MCP server and
  reference it in `agents/planner.md` and `agents/reviewer.md` instead of
  relying on plain WebFetch.
