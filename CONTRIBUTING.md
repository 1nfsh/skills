# Contributing

## Skill Structure

Each skill is a directory with a `SKILL.md` file:

```
skills/
└── my-skill/
    ├── SKILL.md           # Required: main skill file
    └── references/        # Optional: detailed docs
        └── api.md
```

## SKILL.md Format

```yaml
---
name: my-skill
description: |
  What this skill does and when to use it.
  Include relevant keywords so agents know when to activate.
allowed-tools: Bash(belt *)
---

# My Skill

Content, examples, and commands here.
```

## Adding New Skills

1. Create `skills/<skill-name>/SKILL.md`
2. Write a clear description of when to use the skill
3. Add working examples with real app IDs from `belt app list`
4. Cross-reference related skills with `npx skills add` commands
5. Test with `belt app run` to verify examples work

## Cross-Referencing

Every skill should reference related skills:

```markdown
## Related Skills

\`\`\`bash
npx skills add inference-sh/skills@infsh-cli
npx skills add inference-sh/skills@related-skill
\`\`\`
```

## Updating App Lists

Apps change over time. To refresh:

```bash
belt app list                    # All apps
belt app list --category image   # By category
belt app list --search "flux"    # Search
```
