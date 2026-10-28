<!--
Delta spec template for a change.

This template shows the 4 kinds of delta section; use whichever you need:
- ADDED / MODIFIED / REMOVED / RENAMED
File name and location: openspec/changes/<change-name>/specs/<capability>/spec.md
(`<capability>` matches the openspec/specs/<capability>/ directory name)

Hard format rules (validated by OpenSpec):
- Requirement sentences MUST contain `SHALL` or `MUST`
- Every Requirement MUST have at least one `#### Scenario:`
- Scenarios MUST use level-4 (`####`); level-3 or bullets fail silently
-->

## ADDED Requirements

<!-- New behavior. List the new Requirements this change adds to the capability. -->

### Requirement: <!-- requirement name -->
<!-- requirement text — must contain SHALL or MUST -->

#### Scenario: <!-- scenario name -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## MODIFIED Requirements

<!--
Modify an existing Requirement. **MUST use the exact same normalized header
as openspec/specs/<capability>/spec.md** (case-sensitive comparison after trim);
otherwise the delta apply at archive time fails because it cannot find the
matching requirement.

**MUST paste the full modified content** (not just a diff), because OpenSpec
archive applies MODIFIED by full-text replacement.
-->

### Requirement: <!-- same header as in the existing spec -->
<!-- full modified requirement text — contains SHALL or MUST -->

#### Scenario: <!-- scenario name (may be added or modified) -->
- **WHEN** <!-- condition -->
- **THEN** <!-- expected outcome -->

---

## REMOVED Requirements

<!--
Remove an existing Requirement. MUST include Reason and Migration notes so
reviewers understand why it is being removed and how existing consumers
should migrate.
-->

### Requirement: <!-- header to remove, identical to the existing spec -->

**Reason**: <!-- why it is being removed -->

**Migration**: <!-- how existing callers/dependents should adjust -->

---

## RENAMED Requirements

<!--
Rename a Requirement header. Fixed format: FROM / TO using code-fence headers.
If both the name and the content change, list the rename in RENAMED **and**
write the full content again in MODIFIED under the **new** header.

Apply order at archive: RENAMED → REMOVED → MODIFIED → ADDED
-->

- FROM: `### Requirement: <Old Name>`
- TO: `### Requirement: <New Name>`
