# Skills

Personal agent skills for practical engineering work.

## Install

Install with the [skills CLI](https://skills.sh/docs):

```sh
npx skills add VicentGJ/skills --skill pragmatic-review
```

Add `-g` for installation across projects, or `-a codex` / `-a claude-code` to select an agent.

## Available skills

- [pragmatic-review](skills/pragmatic-review/SKILL.md): explain functional changes, assess complexity file by file, challenge unnecessary machinery, and evaluate architectural fit with evidence. Invoke it explicitly with the change or PR to review.

## Layout

Each skill lives in `skills/<name>/SKILL.md` with YAML `name` and `description` fields. Optional supporting files belong alongside it. `agents/openai.yaml` preserves Codex-specific invocation settings.
