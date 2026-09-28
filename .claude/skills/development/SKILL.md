---
name: development
description: Implement the design task by task, with tests written alongside the code. Run after the design gate passes, and again when tasks remain open.
disable-model-invocation: true
metadata:
  version: "1.0.0"
---

# Development stage

## Purpose

Build the solution the team designed, one task at a time, with a test for
each behaviour. The design and the requirements stay in charge. If the code
needs a decision that is not recorded, stop and ask.

## Inputs

- `docs/design/DESIGN.md`: tasks and decisions. Update task status here.
- `docs/requirements/REQUIREMENTS.md`: what the behaviour must be.
- `docs/input/*.md`: **read-only.** Never modify these files.
- `CLAUDE.md` and `CONTRIBUTING.md`: standing rules.
- The source tree and tests.

## Steps

1. **Pulse started.** Run this first, before any other work:
   - macOS / Linux / Git Bash: `tools/pulse.sh development started`
   - Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1 development started`

   If the pulse prints a warning, tell the team and carry on. Pulses never block the work.

2. **Check the previous gate and the skills.** If `DESIGN.md` has no passed
   gate, stop and tell the team. If any of `development` (this skill),
   `review`, `quality`, or `handoff` is missing under `.claude/skills/`,
   stop and tell the team. Do not invent the missing skill during this stage.

3. **Read the design and the requirements** for the task you are about to
   implement. Work the next `open` task in the order written in `DESIGN.md`.
   One task at a time.

4. **Write the test and the code together.** Follow the "done when" on the
   task. Validate input. Enforce each role's permissions where the action is
   performed, not only by hiding controls. Use the stack and layout already
   recorded in `DESIGN.md`.

5. **Stop when the design or the requirements do not answer the question.**
   - Present two or three options with trade-offs and wait for the team.
   - Record the choice as a new `D-` item in `DESIGN.md`, in the same change as the code.
   - If the gap is a missing business rule, do not invent it. Ask the product owner and record an assumption or open question in `REQUIREMENTS.md` only after they decide.

6. **Run the tests for this task.** Mark the task `done` in `DESIGN.md` only
   after you ran the tests and saw them pass. Say which command you ran and
   what it printed. If a test fails, fix the cause or ask the team. Never
   weaken, skip, or delete a test to make it pass.

7. **Commit the task** before starting the next one. Use `CONTRIBUTING.md`
   message style and a requirement ID, for example `feat(REQ-004): ...` or
   `test(REQ-004): ...`. Include the `DESIGN.md` status update in that commit
   when the task is done. Do not commit `.env` or secrets.

8. **Repeat steps 3 to 7** until every task is `done` or the team tells you
   to stop. Leave unfinished tasks `open`. Do not mark them done.

9. **Review.** Check and report:
   - every `done` task has a commit and a test that was run
   - open tasks are still listed
   - behaviour matches `REQUIREMENTS.md` and `DESIGN.md`
   - documents changed by implementation were updated in the same commits

   Then walk the team through the **Gate checklist** item by item. **The team
   decides** whether the gate passed or failed. A passed gate can still leave
   open tasks; those belong in Known limitations later. Record the result and
   the completion timestamp in `DESIGN.md`.

10. **Commit** any remaining design or requirements updates and `pulses.log`
    (e.g. `docs(design): mark development gate`).

11. **Pulse completed.** Count from the committed design and the latest test
    run, never estimate:
    - `tasks_completed` = number of `T-` items with status `done`
    - `tests` = total tests reported by the test command you actually ran

    If you did not run the full suite, run it now and use that output. If the
    suite cannot run, report `tests=0` and say why. Do not guess a number.

    ```text
    tools/pulse.sh development completed --gate <passed|failed> --count tasks_completed=N --count tests=N
    ```

    On Windows: `powershell -ExecutionPolicy Bypass -File tools\pulse.ps1` with
    the same arguments. Report the gate honestly. A failed gate is valid
    information, not a problem to hide.

## Output

- Source code and tests, committed task by task.
- `docs/design/DESIGN.md` updated with task status and any new decisions.
- Two pulses in `pulses.log` (started, completed).

## Gate checklist

The team confirms each item:

- [ ] The design gate passed before implementation started.
- [ ] Each done task matches its requirement IDs and its "done when".
- [ ] Tests were written with the code, and the reported test count comes from a run.
- [ ] No test was weakened, skipped, or deleted to make it pass.
- [ ] Permissions are enforced in the action, not only in the interface.
- [ ] New decisions were recorded in `DESIGN.md`. No requirement was invented.
- [ ] Open tasks are still visible.
- [ ] The team has read the changes and agrees with them.

## Pulse calls

| When | Command |
|---|---|
| First step | `tools/pulse.sh development started` |
| Last step, after commit | `tools/pulse.sh development completed --gate <passed\|failed> --count tasks_completed=N --count tests=N` |

Only this skill sends these pulses. If a pulse fails, tell the team and carry on.
