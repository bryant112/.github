# Project Setup

This setup assumes GitHub Projects v2.

For the full end-to-end rollout, command examples, and current operating notes, also read:

- `docs/tracker/bootstrap-playbook.md`
- `docs/tracker/current-baseline.md`

If the repository belongs to an organization and GitHub Team is available, create an organization-level Project first. That is the cleanest default because it works for one repo now and scales to multiple repos later.

## Recommended Project

- Name: `Delivery Tracker`
- Scope: organization-level if possible; repo-level only if this work is truly isolated
- Visibility: private or internal by default unless the work should be public
- Item policy: track issues as the primary work items; do not auto-add pull requests in MVP

## Fields

Use these visible fields in the main table view:

- `Title`
- `Status`
- `Priority`
- `Effort`
- `Assignees`
- `Labels`
- `Milestone`
- `Iteration`
- `Linked pull requests`

Keep `Repository` visible if the Project will span multiple repositories.

## Configure Status

Edit the built-in `Status` field so the options are:

- `Backlog`
- `Ready`
- `In Progress`
- `Blocked`
- `In Review`
- `Done`

Use these meanings:

- `Backlog`: valid work, not yet ready to pull
- `Ready`: clear, scoped, and available to start next
- `In Progress`: actively being worked now
- `Blocked`: waiting on something external to move forward
- `In Review`: implementation exists and is waiting on review, merge, or verification
- `Done`: closed and complete

## Create Custom Fields

### Priority

- Type: single select
- Values:
  - `P1` - pull next, urgent, release-critical, or high business impact
  - `P2` - important next, should land soon
  - `P3` - useful backlog work, not urgent
  - `P4` - later, optional, or parking lot

### Effort

- Type: single select
- Values:
  - `XS` - less than half a day
  - `S` - about one day
  - `M` - two to three days
  - `L` - up to one week
  - `XL` - bigger than one week; split if you can

### Iteration

- Type: iteration
- Default cadence: two weeks
- Start day: Monday
- Usage: optional but recommended once you have more than a few active issues

## Why Type and Area Are Not Project Fields

Type and area already need to work in repository issue search, notifications, and cross-project filtering. Labels are the simpler source of truth for those dimensions, so this setup uses the built-in `Labels` field instead of duplicating `Type` and `Area` as custom Project fields.

## Views

Create these saved views:

### 1. Ready

- Layout: table
- Filter: `status:Ready`
- Sort: `Priority` ascending, then `Milestone`, then updated descending
- Show: `Priority`, `Effort`, `Labels`, `Milestone`, `Linked pull requests`

### 2. Active

- Layout: board
- Column field: `Status`
- Visible columns: `Ready`, `In Progress`, `Blocked`, `In Review`
- Hide: `Backlog` and `Done`

### 3. Backlog

- Layout: table
- Filter: `status:Backlog`
- Sort: `Priority` ascending, then updated descending

### 4. Bugs

- Layout: table
- Filter: `label:"type:bug" -status:Done`
- Sort: `Priority` ascending, then updated descending

### 5. Current Iteration

- Layout: table
- Filter: `iteration:@current -status:Done`
- Sort: `Status`, then `Priority`

### 6. Releases

- Layout: roadmap
- Timeline field: `Iteration`
- Vertical markers: milestones
- Group by: `Milestone`
- Filter: `-status:Done`

If you are not using iterations yet, make `Releases` a table grouped by `Milestone` until the iteration field becomes useful.

## Built-In Workflows

Enable these Project workflows:

### Auto-add to project

- Repository: the tracked repository
- Filter: `is:issue`

If your Project spans more than one repository, duplicate the workflow once per repository.

### Set status when item added

- Trigger: item added to project
- Value: `Backlog`

### Set status to Done when issue closed

- Leave enabled

This keeps the Project honest without requiring you to drag cards at the end of every merge.

### Set status to Done when pull request merged

- Leave enabled

This is harmless even if you are not auto-adding pull requests.

### Close issue when status changes to Done

- Leave disabled for MVP

Closing an issue should come from merged linked PRs or an explicit issue close, not from card-dragging magic.

### Auto-archive items

- Filter: `is:closed updated:<@today-14d`

This keeps recent wins visible for a short time and quietly clears old completed work.

## Repository Setup

After the Project exists:

1. Add the issue form files in `.github/ISSUE_TEMPLATE/`.
2. Add the labels from `docs/tracker/labels.md`.
3. Add the PR template.
4. Create a first milestone for the next real release or outcome target.
5. Backfill current work into issues and add them to the Project.

## Current GitHub Docs Checked

These recommendations were checked against GitHub Docs on April 20, 2026:

- Issue forms: https://docs.github.com/articles/configuring-issue-templates-for-your-repository
- Projects quickstart: https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/quickstart-for-projects
- Built-in automations: https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-built-in-automations
- Auto-add filters: https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/adding-items-automatically
- Auto-archive filters: https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/archiving-items-automatically
- Views and layouts: https://docs.github.com/en/issues/planning-and-tracking-with-projects/customizing-views-in-your-project/changing-the-layout-of-a-view
- Iteration fields: https://docs.github.com/issues/trying-out-the-new-projects-experience/managing-iterations
- Linked pull requests field: https://docs.github.com/en/issues/planning-and-tracking-with-projects/understanding-fields/about-pull-request-fields
