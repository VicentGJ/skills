# Skills

Personal agent skills for practical engineering work.

## Install

Install with the [skills CLI](https://skills.sh/docs):

```sh
npx skills add VicentGJ/skills --skill pragmatic-mode
npx skills add VicentGJ/skills --skill pragmatic-review
```

Add `-g` for installation across projects, or `-a codex` / `-a claude-code` to select an agent. `pragmatic-mode` runs `pragmatic-review` as its self-review step, so install both.

## Available skills

- [pragmatic-mode](skills/pragmatic-mode/SKILL.md): a working mode, not a one-off utility. Once invoked, the agent follows it for the rest of the session: requirements interview, UI prototypes to pick from, minimal implementation that extends existing systems, visual QA with captured evidence and a compact E2E suite, self-review with `pragmatic-review`, and a PR.
- [pragmatic-review](skills/pragmatic-review/SKILL.md): explain functional changes, assess complexity file by file, challenge unnecessary machinery, and evaluate architectural fit with evidence. Invoke it explicitly with the change or PR to review.

## Turn pragmatic mode on for a repository

Invoke `/pragmatic-mode` (Claude Code, Cursor) or `$pragmatic-mode` (Codex) at the start of a session. To apply it to every session in a repository, add this line to its `AGENTS.md` or `CLAUDE.md`:

```md
For any task that changes code, follow the `pragmatic-mode` skill.
```

## Layout

Each skill lives in `skills/<name>/SKILL.md` with YAML `name` and `description` fields. Optional supporting files belong alongside it. `agents/openai.yaml` preserves Codex-specific invocation settings.
