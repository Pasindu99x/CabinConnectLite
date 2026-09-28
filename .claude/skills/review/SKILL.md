---
name: review
description: Review the code against the requirements and the design, and record findings. Run after development, and again after fixes.
disable-model-invocation: true
metadata:
  version: "1.0.0"
---

# Review stage

## Purpose

Check the implementation against the specification and the design, and leave
a written list of findings. The team decides which findings to fix before
quality starts. A review that finds issues is a successful review.

## Inputs

- `docs/requirements/REQUIREMENTS.md`
- `docs/design/DESIGN.md`
- `docs/input/*.md`: **read-only.** Never modify these files.
- Source code and tests.
- `docs/review/REVIEW.md`: create it on the first review; update it on later ones.
- `CLAUDE.md` and `CONTRIBUTING.md`

## Steps

1. **Pulse started.** Run this first, before any other work:
   - macOS / Linux / Git Bash: `tools/pulse.sh review started`
   - Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1 review started`

   If the pulse prints a warning, tell the team and carry on. Pulses never block the work.

2. **Check the previous gate.** If `DESIGN.md` has no development gate result,
   tell the team. You may still review, but say that development was not
   confirmed.

3. **Read the specification, the design, and the code.** Do not review names
   and file lists alone. Read the checks that enforce each business rule and
   each role permission. Read the tests and note what they actually assert.

4. **Compare.** For every `REQ-`, `BR-`, `VAL-`, `ERR-`, `EC-`, `SEC-`, and
   acceptance criterion, record whether the code and a test cover it, or
   whether there is a gap. Note open `T-` tasks as unfinished scope, not as
   surprise defects.

5. **Write findings.** Create or update `docs/review/REVIEW.md`. Keep existing
   `F-` IDs and the team's manual edits. New findings get new IDs. Never
   reuse an ID. Each finding has:
   - severity: `blocker`, `major`, or `minor`
   - location in the code or documents
   - related requirement or rule IDs
   - what is wrong and what the spec or design requires
   - status: `open` or `fixed`

   On an update, add findings; do not delete old ones. If the team edited
   the file by hand, re-read it before continuing.

6. **Present the findings and wait.** Do not fix them until the team says
   which ones to fix now. For each fix they accept:
   - change the code or the test
   - never weaken, skip, or delete a test to close a finding
   - commit with the finding ID, for example `fix(F-003): ...`
   - set that finding's status to `fixed` and note the commit

   Leave the rest `open`.

7. **Review.** Report blocker and major findings still open. Then walk the
   team through the **Gate checklist** item by item. **The team decides**
   whether the gate passed or failed. Open findings do not force a failed
   gate; hidden findings do. Record the result and the completion timestamp
   in `REVIEW.md`.

8. **Commit** `REVIEW.md`, any fixes not yet committed, and `pulses.log`
    (e.g. `docs(review): record review findings`).

9. **Pulse completed.** Count from the committed review file, never estimate:
    - `findings` = number of `F-` items
    - `findings_fixed` = number of `F-` items with status `fixed`

    ```text
    tools/pulse.sh review completed --gate <passed|failed> --count findings=N --count findings_fixed=N
    ```

    On Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1` with
    the same arguments. Report the gate honestly. A failed gate is valid
    information, not a problem to hide.

## Output

- `docs/review/REVIEW.md`, created or updated, and committed.
- Fix commits for the findings the team chose to fix now.
- Two pulses in `pulses.log` (started, completed).

## Gate checklist

The team confirms each item:

- [ ] Every requirement and business rule was checked against the code and the tests.
- [ ] Each finding has an ID, severity, location, related IDs, and a status.
- [ ] Findings the team accepted are fixed in commits, and the rest stay open.
- [ ] No test was weakened, skipped, or deleted to close a finding.
- [ ] Open tasks and unfinished scope are visible.
- [ ] The team has read the findings and agrees with the record.

## Pulse calls

| When | Command |
|---|---|
| First step | `tools/pulse.sh review started` |
| Last step, after commit | `tools/pulse.sh review completed --gate <passed\|failed> --count findings=N --count findings_fixed=N` |

Only this skill sends these pulses. If a pulse fails, tell the team and carry on.
