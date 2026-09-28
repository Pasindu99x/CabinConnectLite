---
name: handoff
description: Validate the delivery, finish the README and AI log, and open the pull request to main. Run after quality, when the team is ready to hand off.
disable-model-invocation: true
metadata:
  version: "1.0.0"
---

# Handoff stage

## Purpose

Make the repository runnable from the commands in the README, and leave an
honest account of what was delivered, what was tested, and what remains
unfinished. The team confirms the gate. Do not merge the pull request.

## Inputs

- `README.md`: fill every section marked *Completed at handoff*.
- `docs/requirements/REQUIREMENTS.md`
- `docs/design/DESIGN.md`
- `docs/review/REVIEW.md`
- `docs/testing/TEST_REPORT.md`
- `AI-LOG.md` and `AI-USAGE.md`
- `.github/pull_request_template.md`
- `CONTRIBUTING.md` and `CHALLENGE.md`
- `docs/input/*.md`: **read-only.** Never modify these files.

## Steps

1. **Pulse started.** Run this first, before any other work:
   - macOS / Linux / Git Bash: `tools/pulse.sh handoff started`
   - Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1 handoff started`

   If the pulse prints a warning, tell the team and carry on. Pulses never block the work.

2. **Check earlier stages.** Run `tools/pulse.sh status` (on Windows,
   `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1 status`). If any
   earlier stage has no completed pulse, tell the team. Do not mark this gate
   passed while an earlier stage was never completed.

3. **Finish the README.** Replace every *Completed at handoff* placeholder.
   - Chosen stack: language, frameworks, storage, test tools, and the `D-` IDs in `DESIGN.md`.
   - Prerequisites: tools and versions a fresh machine needs.
   - Install, configure, run, and test: exact commands. Write "None" for configure when there is nothing to configure.
   - How to open the running application and act as each seeded user.
   - Known limitations: the out-of-scope items already listed, plus unfinished tasks, open findings, failing tests, and partial requirements. Do not remove a limitation to make the delivery look finished.

   The test command in the README must match `TEST_REPORT.md`.

4. **Verify the commands.** Run the install, run, and test commands you wrote.
   Say what you ran and what happened. Do not claim a fresh clone works unless
   you actually cloned fresh and used only those commands. If you could not
   do that, write what you did not verify under Known limitations.

5. **Complete `AI-LOG.md`.** Ask the team the three reflection questions and
   record their answers. Do not invent the reflection. Check that key prompts
   and corrections, including skill changes, are filled in. If a row is
   empty because it never happened, say so. Do not fabricate entries.

6. **Draft the pull request body** from `.github/pull_request_template.md`.
   Use requirement IDs, `D-` IDs, and the test command plus the summary line
   from `TEST_REPORT.md`. Mark partial features as partial. List the same
   known limitations as the README.

7. **Review.** Walk the team through the **Gate checklist** item by item.
   **The team decides** whether the gate passed or failed. Record the result
   in the PR body. Count, from the committed test report and README:
   - `requirements_traced` = number of `REQ-` rows in the traceability matrix whose implementation and test are both filled in
   - `known_limitations` = number of limitation items under Known limitations in `README.md`

8. **Commit** the README, `AI-LOG.md`, any report or design updates, and
   `pulses.log` (e.g. `docs(handoff): complete README and AI log`). Do not
   commit `.env` or secrets.

9. **Pulse completed.** Use the counts from step 7. Do not estimate.

   ```text
   tools/pulse.sh handoff completed --gate <passed|failed> --count requirements_traced=N --count known_limitations=N
   ```

   On Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1` with
   the same arguments. Report the gate honestly. A failed gate is valid
   information, not a problem to hide.

10. **Commit `pulses.log` again** so the handoff completed pulse is in git
    (e.g. `chore: record handoff pulse`).

11. **Open the pull request** from `solution` to `main`, using the body from
    step 6. Follow `CONTRIBUTING.md`. If the work is not on `solution`, stop
    and tell the team. **Do not merge the pull request.**

## Output

- `README.md` completed and committed.
- `AI-LOG.md` completed and committed.
- `pulses.log` committed, including the handoff completed pulse.
- An open pull request from `solution` to `main`. It stays open.

## Gate checklist

The team confirms each item:

- [ ] `tools/pulse.sh status` shows every earlier stage completed, and this stage's pulses are committed.
- [ ] README install, run, and test commands were executed, and the result is stated honestly.
- [ ] README test commands match the test report.
- [ ] Every *Completed at handoff* section is filled in.
- [ ] Known limitations match unfinished work. Nothing unfinished is hidden.
- [ ] The traceability count matches the test report, and gaps are not counted as traced.
- [ ] `AI-LOG.md` includes the team's reflection and the corrections made during the challenge.
- [ ] The pull request to `main` is open and not merged.

## Pulse calls

| When | Command |
|---|---|
| First step | `tools/pulse.sh handoff started` |
| After the README commit, before the pull request | `tools/pulse.sh handoff completed --gate <passed\|failed> --count requirements_traced=N --count known_limitations=N` |

Only this skill sends these pulses. If a pulse fails, tell the team and carry on.
