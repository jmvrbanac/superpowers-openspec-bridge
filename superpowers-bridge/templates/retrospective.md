# Retrospective: <change-name>

> Written: <YYYY-MM-DD> (after verify passed)
> Commit range: `<base-sha>..<head-sha>`
> Worktree: <path or "merged to main">

---

## 0. Evidence

> Quantitative groundwork — later Wins / Misses bullets cite it directly, avoiding a repeated [evidence: ...] on every line.
> For cold writes (retro written some time after the cycle ends), this section
> should be reconstructable from `git log` + `tasks.md` + commit messages alone.

- **Commit range**: `<base-sha>..<head-sha>` (<n> commits)
- **Diff size**: <+X / -Y lines across N files>
- **Tasks done**: <x>/<y> (`grep -cE '^\s*- \[x\]' tasks.md` → x; the regex tolerates sub-task indentation)
- **Active hours**: <estimate>
- **Subagent dispatches**: <count or "n/a">
- **New external dependencies**: <list, with license + version, or "none">
- **Bugs encountered post-merge**: <count, one-line each, or "none">
- **OpenSpec validate state at archive**: <pass / fail / not-run>
- **Test coverage signal**: <e.g. jacoco %, pytest count, vitest count, or "n/a">

Commit chain (chronological):

```
<base-sha> <one-line summary>
...
<head-sha> <archive commit one-line>
```

---

## 1. Wins

- [evidence: <commit/file/test>] <description>

## 2. Misses

- 🔴 [blocking | evidence: ...] <description>
- 🟡 [painful  | evidence: ...] <description>
- 📌 [nit      | evidence: ...] <description>

## 3. Plan deviations

| Plan task | What changed | Why |
|-----------|--------------|-----|
| 1.2       | ...          | ... |

## 4. Skill / workflow compliance

| Skill                                            | Used |
|--------------------------------------------------|------|
| superpowers:brainstorming                        |      |
| superpowers:writing-plans                        |      |
| superpowers:using-git-worktrees                  |      |
| superpowers:subagent-driven-development          |      |
| (transitive) superpowers:test-driven-development |      |
| (transitive) superpowers:requesting-code-review  |      |
| superpowers:finishing-a-development-branch       |      |

> **Default expectation**: all ✓. Every skill is part of the schema's design;
> skipping one is an abnormal situation. Any ✗ must be explained, with a
> prevention plan, in the `### Deliberately Skipped Skills` subsection below.

### Deliberately Skipped Skills

> Skipping a skill is a design escape hatch, not the normal path. Every ✗ must
> answer the three questions below; a blank section (all green) is the
> expected state.

- **`<skill name>`**
  - **What was skipped**: <was the whole skill skipped, or a specific sub-step?>
  - **Why this cycle**: <the concrete cycle conditions — vague reasons such as "not needed" / "too small" / "no time" / "blocked by an external dep" / "skill output looked wrong" are not acceptable; state the actual trigger (a specific commit / log line / observed behavior)>
  - **How to prevent recurrence**: How will the next cycle avoid skipping under similar conditions? Pick one:
    - `schema graph fix` — state exactly which part of schema.yaml to change
    - `skill description tightening` — state exactly which skill's frontmatter / instruction to change
    - `CLAUDE.md trigger` — state exactly which interpretation rule to add to the adopter CLAUDE.md.fragment
    - `scope-judgment rule` — state how this cycle's scope should have been judged
    - `one-off — schema boundary case, no prevention possible` — but explicitly state why it is a boundary (vague reservations are not accepted)

> **Relationship to §6 Promote candidates**: if multiple cycles give the same
> `How to prevent` answer for the same skill, that pattern should be promoted
> to §6 and trigger a schema / skill PR directly; it must not accumulate into
> a "norm".

## 5. Surprises

- <assumption that turned out wrong>

## 6. Promote candidates → long-term learning

Each candidate is a `- [ ]` checklist item:

- Title: severity emoji (🔴/🟡/📌) + a one-sentence learning
- `→ **Promote to** <destination>`(memory / CLAUDE.md / schema / skill / one-off)
- Two-line body (matches the superpowers feedback memory body schema):
  - `> **Why**: <reason; often a past incident or strong preference>`
  - `> **How to apply**: <when/where this guidance kicks in>`

An unchecked `- [ ]` means the candidate has not been promoted — it can be
re-evaluated in the next cycle's retro, or kept as a cross-cycle observation.

> **Carry-forward mechanism**: when writing the next cycle's retro, run
> `grep -A 5 '^- \[ \]' openspec/changes/archive/*/retrospective.md` to pull
> out earlier unchecked candidates, and decide one by one whether to
> carry-forward into this cycle's §6, promote on the spot, or mark stale and
> stop tracking.

Examples:

- [ ] 🔴 **<short rule>** → **Promote to memory** (type: feedback)
  > **Why**: <past incident or strong preference that motivated this rule>
  > **How to apply**: <which file / cycle phase / decision moment this kicks in>

- [ ] 🟡 **<another candidate>** → **Promote to project CLAUDE.md** (`<path/to/CLAUDE.md>` section)
  > **Why**: ...
  > **How to apply**: ...

- [ ] 📌 **<third candidate>** → **One-off** (record only, do not promote)
  > **Why**: <why it doesn't generalize>
