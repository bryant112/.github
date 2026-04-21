# Tracker Operating Model

This operating model is designed for a solo-heavy workflow that can grow into a small team later.

## Intake

New work enters through an issue form.

By default, new issues get:

- one `type:*` label
- `needs:triage`
- `Status = Backlog` through the Project workflow

That means everything lands in one predictable place instead of living in notes, chat, and memory.

## Triage

Triage should happen at the next sensible work start, or sooner for urgent bugs.

Triage checklist:

1. Confirm the issue is real and worth tracking.
2. Remove `needs:triage`.
3. Add one `area:*` label.
4. Add `severity:*` if it is a bug.
5. Set `Priority`.
6. Set `Effort`.
7. Attach a milestone if it belongs to a real release or outcome target.
8. Move it to `Ready`, `Backlog`, or `Blocked`.

If the issue is not actionable because the solution space is unclear, create a spike and link it from the original issue.

## timetowork Start Ritual

Start from the Project, not from memory.

Recommended start sequence:

1. Open the `Ready` view.
2. Pull the highest-value issue that is clear enough to finish.
3. Move it to `In Progress`.
4. Assign it to yourself.
5. Set the current iteration if you are using iterations.
6. Create a branch named from the issue number and short topic.

Default rule: keep one active `In Progress` issue unless something truly urgent interrupts it.

## During Work

- Keep implementation detail in the branch and PR.
- Keep planning detail and next-step clarity in the issue.
- If a PR is opened, move the issue to `In Review`.
- If work cannot move, move the issue to `Blocked` and add `status:blocked`.

If scope expands mid-stream:

- split follow-on work into a new issue
- keep the current issue pointed at the smallest useful finish

## clean-sweep End Ritual

End the session with the tracker in a truthful state.

Recommended end sequence:

1. Push the branch or save the work remotely.
2. Open or update the PR if review is the next step.
3. Leave a short issue comment with the current state.
4. Move the issue to the right status: `In Review`, `Blocked`, or back to `Ready`.
5. If blocked, say what is blocking it and what would unblock it.
6. Make sure at least one `Ready` issue exists for the next session.

Use this comment format when helpful:

```text
Session note
- What changed: ...
- Next step: ...
- Risk or blocker: ...
```

## Bug Handling

Bugs are triaged by both severity and priority.

- Severity says how bad the defect is.
- Priority says when you actually pull it.

Example:

- An `S2` bug can still be `P1` if it is blocking the next release.
- An `S1` bug should almost always become `P1`.

## Backlog Maintenance

Run a short backlog pass once a week or once per iteration:

- close stale low-value items
- split oversized issues
- re-check blocked items
- re-check the next milestone
- make sure the `Ready` column has real options

The backlog should feel curated, not hoarded.

## Completion

An issue is complete when one of these is true:

- the linked PR merged and closed it
- the work was completed without a PR and the issue was explicitly closed
- the work was intentionally dropped and the issue was closed with a clear reason

The Project then reflects completion through the built-in closed-to-done workflow and later auto-archives the item.
