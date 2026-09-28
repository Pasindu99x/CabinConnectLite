---
name: quality
description: Run the tests, record the observed results, and complete the test report. Run after review, and again when tests or the report change.
disable-model-invocation: true
metadata:
  version: "1.0.0"
---

# Quality stage

## Purpose

Show what was tested and what actually happened. Every number in the test
report comes from a run you observed. Failures stay visible. The team uses
that evidence to decide the gate.

## Inputs

- `docs/requirements/REQUIREMENTS.md`
- `docs/design/DESIGN.md`
- `docs/review/REVIEW.md`: open findings are remaining issues unless a test shows they are fixed.
- `docs/testing/TEST_REPORT.md`: fill this template. Keep its headings.
- `docs/input/*.md`: **read-only.** Never modify these files.
- `CLAUDE.md` and `README.md` (the Test and Main scenarios sections).
- The test suite.

## Steps

1. **Pulse started.** Run this first, before any other work:
   - macOS / Linux / Git Bash: `tools/pulse.sh quality started`
   - Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1 quality started`

   If the pulse prints a warning, tell the team and carry on. Pulses never block the work.

2. **Read the report template and the spec.** Keep the headings in
   `docs/testing/TEST_REPORT.md`. Remove the template's guidance text and
   example rows when you fill them. On a later iteration, **update** the
   report; do not invent a second report.

3. **Run the full automated suite** with the exact command that will be
   documented. Run it from a clean test state when the stack has one. Copy
   the raw summary line into the report, including failed and skipped counts.
   Record the UTC time and the commit you ran against.

4. **Fill the report from that run.**
   - What was tested, at which level, and why.
   - What was not tested, and why.
   - The install and test commands. They must be the commands you ran.
   - The results table. Do not round and do not type numbers from memory.
   - Manual checks for the README main scenarios that automation does not cover. Record steps, expected, actual, and result. If you did not run a manual check, say so.
   - A traceability row for **every** `REQ-` ID. Point to the design section, the code, and the test. Mark gaps as gaps. Do not omit a requirement to make the matrix look complete.
   - One test for every `BR-` ID, or a stated reason why not.
   - Known limitations and remaining issues, including open review findings and open tasks.

5. **If a test fails,** report the failure in the results table. Then either
   fix the cause, re-run, and update the table from the new output, or leave
   the failure and add a remaining issue. Never weaken, skip, or delete a
   test to make it pass. Never claim a pass you did not see.

6. **Review.** Re-read the report after any hand edit. Check that every
   number matches the pasted summary, and that every requirement ID appears
   once in the matrix. Then walk the team through the **Gate checklist**
   item by item. **The team decides** whether the gate passed or failed.
   Failing tests can still be an honest passed gate only if the team accepts
   them as known limitations. Record the result and the completion timestamp
   in the report.

7. **Commit** `TEST_REPORT.md`, any test or code fixes, and `pulses.log`
   (e.g. `docs(quality): record test results`).

8. **Pulse completed.** Count from the committed report's results table,
   never estimate:
   - `tests` = Total
   - `tests_passed` = Passed
   - `tests_failed` = Failed

   Use the automated run's counts. Do not add manual checks into these three
   numbers. Manual checks stay in the report.

   ```text
   tools/pulse.sh quality completed --gate <passed|failed> --count tests=N --count tests_passed=N --count tests_failed=N
   ```

   On Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1` with
   the same arguments. Report the gate honestly. A failed gate is valid
   information, not a problem to hide.

## Output

- `docs/testing/TEST_REPORT.md`, completed or updated from an actual run, and committed.
- Two pulses in `pulses.log` (started, completed).

## Gate checklist

The team confirms each item:

- [ ] The full suite was run with the documented command, and the raw summary is in the report.
- [ ] Totals, passed, failed, and skipped match that summary.
- [ ] No test was weakened, skipped, or deleted to make it pass.
- [ ] Every requirement appears in the traceability matrix, with gaps marked.
- [ ] Every business rule has at least one test, or a stated reason why not.
- [ ] Known limitations and remaining issues are listed, including open findings.
- [ ] The team has read the report and agrees with it.

## Pulse calls

| When | Command |
|---|---|
| First step | `tools/pulse.sh quality started` |
| Last step, after commit | `tools/pulse.sh quality completed --gate <passed\|failed> --count tests=N --count tests_passed=N --count tests_failed=N` |

Only this skill sends these pulses. If a pulse fails, tell the team and carry on.
