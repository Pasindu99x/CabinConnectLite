---
name: design
description: Decide how to build the solution, record the decisions, and break the work into small tasks linked to requirement IDs. Run after requirements-elaboration passes, and again when the design changes.
disable-model-invocation: true
metadata:
  version: "1.0.0"
---

# Design stage

## Purpose

Turn the agreed specification into a design the team has chosen, and into
tasks small enough to build and review one at a time. The team owns every
engineering decision. Your job is to present options and record what they
choose, not to choose for them.

## Inputs

- `docs/requirements/REQUIREMENTS.md`: the specification. Read it in full.
- `docs/input/*.md`: business input, for traceability only. **Read-only. Never modify these files.**
- `docs/design/DESIGN.md`: the design to create or update. Create it if it does not exist.
- `CLAUDE.md` and `CONTRIBUTING.md`: standing rules.

## Steps

1. **Pulse started.** Run this first, before any other work:
   - macOS / Linux / Git Bash: `tools/pulse.sh design started`
   - Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1 design started`

   If the pulse prints a warning, tell the team and carry on. Pulses never block the work.

2. **Check the previous gate.** If `REQUIREMENTS.md` has no passed gate, stop
   and tell the team. Do not design against an unconfirmed specification.

3. **Check for an existing design.** If `DESIGN.md` already contains content,
   this is a new iteration: **update** it, do not rewrite it. Keep all existing
   IDs and the team's manual edits. New items get new IDs. Never reuse an ID.

4. **Read the specification.** Read `REQUIREMENTS.md` in full. Do not add
   requirements, rules, or permissions that are not already there or in an
   assumption. If something needed for the design is still ambiguous, stop and
   ask. Record a new assumption or open question in `REQUIREMENTS.md` only
   after the product owner decides. Do not edit `docs/input/`.

5. **Decide with the team.** For each decision below, present two or three
   options with trade-offs, wait for the team to choose, and record a `D-`
   item with who decided and why. Do not recommend unless asked, and then
   give reasons. Do not choose a stack, storage approach, or project layout
   yourself.
   - Language, frameworks, and test tools
   - How data persists between restarts
   - How a person acts as a seeded user (at least two members and one administrator) while permissions are still enforced
   - How the application is structured so each task can be committed on its own

6. **Describe the solution.** In `DESIGN.md`, record:
   - a short summary of the chosen solution
   - the data the application stores, and which rules depend on it
   - how each business rule and each role permission is enforced, traced to `REQ-`, `BR-`, `NFR-`, and `SEC-` IDs
   - where permission checks happen in the action, not only in the interface

   Do not write production code in this stage.

7. **Break the work into tasks.** Add `T-` items. Each task:
   - links to one or more requirement IDs
   - is small enough for one commit
   - states "done when", including the test that will prove it
   - has status `open` until development marks it `done`

   Order the tasks so later tasks build on earlier ones. Leave unfinished
   scope as open tasks. Do not hide it.

8. **Write the document.** Create or update `docs/design/DESIGN.md` with these
   headings: Summary, Decisions, Solution outline, Data, How rules are enforced,
   Tasks, Gate checklist. On an update, show the team a short summary of what
   changed. If the team edited the document by hand, re-read it and check it
   for consistency before continuing.

9. **Review.** Check the document yourself and report what you find:
   - every `REQ-` and `BR-` ID is mentioned in the design or explicitly deferred in a task
   - every `D-` item has options, a team choice, and a reason
   - every `T-` item has requirement IDs and a testable "done when"
   - no requirement was invented
   - no production code was added

   Then walk the team through the **Gate checklist** item by item. **The team
   decides** whether the gate passed or failed. Record the result and the
   completion timestamp in the document.

10. **Confirm the later skills exist.** Before development starts, these files
    must exist: `.claude/skills/development/SKILL.md`,
    `.claude/skills/review/SKILL.md`, `.claude/skills/quality/SKILL.md`,
    `.claude/skills/handoff/SKILL.md`. If any is missing, stop and tell the
    team to write it from `docs/process/SKILL-GUIDE.md`. Do not start
    development inside this skill.

11. **Commit.** Commit `DESIGN.md`, any requirements update from step 4, and
    `pulses.log` (e.g. `docs(design): record design and tasks`).

12. **Pulse completed.** Count from the committed document, never estimate:
    - `decisions` = number of `D-` items
    - `tasks` = number of `T-` items

    ```text
    tools/pulse.sh design completed --gate <passed|failed> --count decisions=N --count tasks=N
    ```

    On Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1` with
    the same arguments. Report the gate honestly. A failed gate is valid
    information, not a problem to hide.

## Output

- `docs/design/DESIGN.md`, created or updated, and committed.
- Two pulses in `pulses.log` (started, completed).

## Gate checklist

The team confirms each item:

- [ ] The requirements gate passed before this design was written.
- [ ] Every engineering decision has options, a team choice, and a reason.
- [ ] The stack, persistence, and seeded-user approach are recorded.
- [ ] Every functional requirement and business rule is covered or explicitly deferred in a task.
- [ ] Every task has requirement IDs and a testable "done when".
- [ ] Role permissions are enforced in the action, not only by hiding controls.
- [ ] No new requirement was added without a product owner decision.
- [ ] The team has read the document and agrees with it.

## Pulse calls

| When | Command |
|---|---|
| First step | `tools/pulse.sh design started` |
| Last step, after commit | `tools/pulse.sh design completed --gate <passed\|failed> --count decisions=N --count tasks=N` |

Only this skill sends these pulses. If a pulse fails, tell the team and carry on.
