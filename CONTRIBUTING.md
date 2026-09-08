# Contributing

## Adding a skill

1. Create a directory named for the skill in kebab-case: `my-skill/`.
2. Add `my-skill/SKILL.md` with YAML frontmatter and instructions (template below).
3. Put any supporting material in `my-skill/references/` or `my-skill/scripts/` and
   link to it from `SKILL.md` with relative paths.
4. Add a row to the Skills table in [README.md](README.md).
5. Open a pull request.

## Frontmatter

| Field | Required | Notes |
|-------|----------|-------|
| `name` | yes | Matches the directory name. Kebab-case, letters/digits/hyphens. |
| `description` | yes | One sentence, third person. State *what* the skill does and *when* to use it — this is what the agent matches against. |

## Authoring conventions

- **Least privilege.** Default to read-only inspection. Require explicit human approval
  before any action that submits, cancels, deletes, or otherwise changes state.
- **Cite authoritative docs.** Link claims about policy or system behavior to the
  relevant VT documentation and any upstream source (Slurm, a vendor, etc.).
- **Respect withheld information.** Do not have the agent infer system-wide state from
  partial views, or promise outcomes a service does not guarantee.
- **Keep credentials out** of commands, scripts, logs, and scheduler exports.
- **Be concise.** A skill is instructions, not a tutorial. Trim anything the agent does
  not need to act correctly.

## Skill template

```markdown
---
name: my-skill
description: <what it does and when to use it, one sentence, third person>
---
# <Title>

## Scope and authorization
- <what must be identified before acting>
- <what stays read-only; what needs approval>

## <Task section>
<focused instructions, with `bash` blocks for concrete commands>

## <Task section>
<...>
```
