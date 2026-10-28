# Verification Report

> This file is produced by the `openspec-verify-change` skill after apply
> completes, to confirm the implementation is consistent with specs / design /
> tasks. Failed checks must be fixed in the corresponding artifact, then verify
> re-run.

**Change**: `<change-name>`
**Verified at**: `YYYY-MM-DD HH:mm`
**Verifier**: `<who / which agent>`

---

## 1. Structural Validation (`openspec validate --all --json`)

- [ ] All items are `"valid": true`

**Result**:

```text
<paste a summary of the openspec validate --all output>
```

If any items failed, list id + issues:

| Item | Type | Issues |
|---|---|---|
| — | — | — |

---

## 2. Task Completion (`tasks.md`)

- [ ] All `- [ ]` have become `- [x]`

**Incomplete tasks** (if any):

| Task | Reason incomplete | Blocks archive? |
|---|---|---|
| — | — | — |

---

## 3. Delta Spec Sync State

For each capability directory under `openspec/changes/<name>/specs/`, compare
against `openspec/specs/<capability>/spec.md`:

| Capability | Sync state | Notes |
|---|---|---|
| — | ✓ synced / ✗ pending sync / N/A | — |

---

## 4. Design / Specs Coherence Spot Check

Sample whether decisions in `design.md` are reflected in the Requirements and
Scenarios of `specs/*.md`:

| Sampled item | design description | specs counterpart | Gap |
|---|---|---|---|
| — | — | — | — |

**Drift warnings** (non-blocking):

- <list if any; otherwise write "none">

---

## 5. Implementation Signal

- [ ] No unstaged files in the worktree
- [ ] All relevant commits have been pushed

**Commit range** (if known):`<from-sha>..<to-sha>`

---

## 6. Front-Door Routing Leak Detector (warning, non-blocking)

Design output should not land in `docs/superpowers/specs/` (the brainstorm
artifact's output redirection sends it to `openspec/changes/<name>/brainstorm.md`).

Detection:

```bash
ls docs/superpowers/specs/*.md 2>/dev/null
```

- [ ] No files, or any existing files are legitimate leftovers from before the schema was installed

**Leak list** (if any):

| File | Content already captured into the change? | Suggested action |
|---|---|---|
| — | — | — |

> Does not block archive. Leaks produced by a new schema-installed cycle should
> be moved into `openspec/changes/<name>/brainstorm.md` or `design.md`, then the
> original file deleted.

---

## 7. Deferred Manual Dogfood vs Automated Test Equivalence

For each manual dogfood / smoke task marked `[~]` (deferred) in plan.md, list
the equivalent automated test coverage. If there is no equivalent automated
test, treat the item as a **real gap** rather than a reasonable deferral, and
record it under retrospective Misses.

| Deferred dogfood (plan §) | Equivalent automated test | Coverage assessment | Real gap? |
|---|---|---|---|
| e.g. §11.3 `compose up + curl /actuator/health` | `LinebcIntegrationApplicationTests` (Testcontainers, 24s) | Spring context boot + Flyway completes + main beans injected | ❌ equivalently covered |
| — | — | — | — |

> **Interpretation rules**:
> - "Equivalent" = the automated test's assertion set is a superset of the assertions the manual dogfood would have made
> - "Coverage assessment" = list the layers actually exercised (context / DB schema / wiring / HTTP path / etc.)
> - For any row with "Real gap = ✅", Overall Decision may still be PASS, but a follow-up entry must be left in the retrospective

> **When this section may be left blank**: when plan.md has no `[~]` rows at all, this section need not be filled (blank = PASS).
> If plan.md contains any `[~]`, every one must be listed here, otherwise Overall Decision must drop to FAIL.

---

## Overall Decision

- [ ] ✅ PASS — may proceed to finishing-a-development-branch and archive
- [ ] ⚠️ PASS WITH WARNINGS — may proceed, with caveats: `<explanation>`
- [ ] ❌ FAIL — fix the failing artifact, then re-run verify

**Next step**:

<describe the next action>
