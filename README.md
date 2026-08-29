# Louis Salvosa's Agent Skills

A focused collection of skills for a complete engineering delivery flow.

## Install

```bash
npx skills@latest add louis-salvosa0101/matt-agent-skills
```

Choose the skills and agent harness during installation. Include `setup-skills`.

## Set up a project

Run `/setup-skills` once in each project. Its workflow is unchanged from the upstream setup skill: it configures your issue tracker (GitHub, GitLab, local Markdown, or another documented workflow), triage labels, and domain-document layout.

Local Markdown is supported for solo work. GitHub Issues is also available whenever you want to publish specifications and tickets to your repository.

## Delivery flow

1. `/grill-with-docs` clarifies the change and records durable domain decisions.
2. `/to-spec` turns the settled conversation into a publishable specification.
3. `/to-tickets` breaks the specification into small, blocked vertical slices.
4. `/implement` builds a ticket using `/tdd` and finishes with `/code-review`.

## Included skills

### User-invoked

- [grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)
- [setup-skills](./skills/engineering/setup-skills/SKILL.md)
- [to-spec](./skills/engineering/to-spec/SKILL.md)
- [to-tickets](./skills/engineering/to-tickets/SKILL.md)
- [implement](./skills/engineering/implement/SKILL.md)
- [triage](./skills/engineering/triage/SKILL.md)

### Model-invoked

- [grilling](./skills/productivity/grilling/SKILL.md)
- [domain-modeling](./skills/engineering/domain-modeling/SKILL.md)
- [codebase-design](./skills/engineering/codebase-design/SKILL.md)
- [tdd](./skills/engineering/tdd/SKILL.md)
- [code-review](./skills/engineering/code-review/SKILL.md)
- [research](./skills/engineering/research/SKILL.md)
- [diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)

## Upstream and license

See [LICENSE](./LICENSE).
