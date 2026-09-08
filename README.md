# VT Skills

A collection of [Agent Skills](https://docs.claude.com/en/docs/claude-code/skills) for
working within a Virginia Tech context — research computing, campus data services, and
related workflows. Each skill packages the norms, guardrails, and reference links an
agent needs to act responsibly on VT infrastructure.

## Skills

| Skill | Purpose |
|-------|---------|
| [`arc-usage-demo`](arc-usage-demo/SKILL.md) | Inspect resources, prepare Slurm jobs, and monitor or recover authorized CPU/GPU research workloads on VT [ARC](https://arc.vt.edu). |

## Using a skill

### Claude Code

Point Claude Code at this repo as a skills source, or copy an individual skill directory
into your project or personal skills folder:

```bash
# Personal skills (available in every project)
mkdir -p ~/.claude/skills
cp -r arc-usage-demo ~/.claude/skills/

# Project skills (checked in with a repo)
mkdir -p .claude/skills
cp -r arc-usage-demo .claude/skills/
```

Claude loads a skill automatically when a task matches its `description`, or you can
invoke it explicitly by name.

### Other agents

Each `SKILL.md` is plain Markdown with YAML frontmatter (`name`, `description`). Any
agent framework that supports skill-style instruction files can consume them directly.

## Repository layout

```
<skill-name>/
  SKILL.md          # required: frontmatter + instructions
  references/       # optional: supporting docs the skill links to
  scripts/          # optional: helper scripts the skill invokes
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for authoring conventions and the skill template.

## Scope and safety

These skills assume authorized use of VT systems by someone with a valid account and
allocation. They constrain an agent toward read-only inspection by default and require
explicit human approval before state-changing actions. They do not grant access, bypass
policy, or substitute for the
[ARC acceptable-use policy](https://docs.arc.vt.edu/usage/01-acceptable-use-policy.html)
and other VT terms.
