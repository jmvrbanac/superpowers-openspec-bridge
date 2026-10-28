# CLAUDE.md

> Context guide for Claude Code when working in this repo. Written in English.
>
> For what this repo is, why it exists, and which bridges it has → see [README.md](./README.md).
> This file focuses on the **conventions and red flags** Claude needs to know when working here.

---

## Structure

```
superpowers-openspec-bridge/                     ← this repo
├── README.md                         ← rendered by default on GitHub
├── CLAUDE.md                         ← you are reading this
├── LICENSE                           ← MIT
├── .gitignore
├── .github/workflows/
│   ├── validate-schemas.yml          ← CI runs openspec schema validate for each bridge
│   └── version-check.yml             ← weekly check of upstream OpenSpec / Superpowers; opens an issue when behind
├── docs/
│   ├── roadmap.md                    ← public roadmap
│   └── superpowers/
│       ├── specs/                    ← design specs (brainstorming output)
│       └── plans/                    ← implementation plans (writing-plans output)
└── superpowers-bridge/                ← first bridge, a self-contained schema bundle
    ├── README.md                     ← full bridge docs (including install + integration runbook)
    ├── schema.yaml                   ← schema definition read by OpenSpec
    └── templates/                    ← artifact templates
        ├── brainstorm.md
        ├── proposal.md
        ├── design.md
        ├── spec.md
        ├── tasks.md
        ├── plan.md
        ├── verify.md
        └── retrospective.md
```

To add a new bridge: add a `<new-bridge>/` subdirectory at the repo root with the same structure as `superpowers-bridge/`. Add one line to `matrix.bridge` in `.github/workflows/validate-schemas.yml` for CI.

## Naming conventions

- **Repo / directory / schema name**: lowercase + hyphen + correct singular/plural
  - repo: `superpowers-openspec-bridge`
  - bridge dir / schema name: `superpowers-bridge` (singular)
  - No PascalCase (OpenSpec's own repo uses `OpenSpec`, but its CLI / npm package are lowercase; we follow the functional naming)

## Language policy

Everything in this repo is written in English: READMEs, `CLAUDE.md`, docs, `schema.yaml`, templates, commit messages, and code comments.

## Schema change workflow

1. Edit `<bridge>/schema.yaml` or `<bridge>/templates/*.md`
2. Validate locally:
   ```bash
   mkdir -p /tmp/test-project/openspec/schemas
   cp -R <bridge>/ /tmp/test-project/openspec/schemas/
   cd /tmp/test-project
   openspec schema validate <bridge-name>
   openspec schemas
   ```
3. If timing mismatches / error behavior change, **also update the "Seven Superpowers touchpoints" section of `superpowers-bridge/README.md`** (especially the verify/retrospective timing mismatch part).
4. Commit messages in English, following conventional commits (`feat:`, `fix:`, `refactor:`, `chore:`, `docs:`, `ci:`)
5. Pushing triggers CI

## Responses to the three alfred-openspec concerns (internalize)

The PR #970 review raised three concerns, which this schema addresses concretely in v1. Claude must remember them before changing any schema behavior in this repo:

| Concern | Response |
|---------|----------|
| #3 Proactively committing to the user's git | **Removed entirely**. Step 0 is now a skill PRECHECK that only verifies skills and never touches git |
| #1 Tight coupling to Superpowers with no capability detection | **Layer 1**: every skill-invoking instruction starts with a PRECHECK and STOPs if the skill is missing. **Layer 2**: verify / retrospective get an evidence-based PRECHECK (`git log`, `grep` to check observable state) |
| #2 verify timing mismatch (and the same for retrospective) | Known limitation, documented in the bridge README as the verify/retrospective timing-mismatch touchpoint. The full fix waits for the OpenSpec engine to introduce a `post_apply` phase. The Layer 2 evidence-based PRECHECK is the current mitigation |

**Red flags when changing the schema** — do **not** do the following (they undo the PR #970 responses):

- ❌ Write "proactively git add / git commit" in an instruction
- ❌ Remove a PRECHECK without replacing it with something stronger
- ❌ Drop verify / retrospective from the artifacts without updating the limitation in the README's touchpoints section
- ❌ Rename the schema without updating all docs inside the bridge plus the bridge index in the top-level README

## Related links

- Design spec: [`docs/superpowers/specs/2026-05-02-openspec-schemas-monorepo-design.md`](./docs/superpowers/specs/2026-05-02-openspec-schemas-monorepo-design.md)
- Implementation plan: [`docs/superpowers/plans/2026-05-02-phase-1-implementation.md`](./docs/superpowers/plans/2026-05-02-phase-1-implementation.md)
- PR #970 review: <https://github.com/Fission-AI/OpenSpec/pull/970>
- Existing spec-kit superpowers bridges for reference:
  - [RbBtSn0w/spec-kit-extensions/superpowers-bridge](https://github.com/RbBtSn0w/spec-kit-extensions/tree/main/superpowers-bridge)
  - [WangX0111/superspec](https://github.com/WangX0111/superspec)
