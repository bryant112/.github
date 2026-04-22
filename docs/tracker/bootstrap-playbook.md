# Repo And Tracker Bootstrap Playbook

This is the durable playbook for getting a repository owner, tracker, and repo into the lean GitHub-native workflow used across `BrynosRepo` and `bryant112`.

Use it for two kinds of work:

- first-time owner setup
- adding or tuning a repo inside an existing tracker

## Decide The Home First

Do not start by creating labels or clicking around in a Project. Start by deciding where the repo honestly belongs.

- Use `BrynosRepo` for primary delivery work.
- Use `bryant112` for sandbox work, incubators, and account tooling.
- Keep archive or low-signal repos unlinked from the active tracker.

That single decision prevents most later cleanup.

## One-Time Owner Setup

### 1. Create The Defaults Repo

Create a public repository named `.github` under the target owner.

Why:

- GitHub only applies most default issue and PR files from a public `.github` repo.
- That repo becomes the single place to update issue forms, PR templates, and tracker docs.

### 2. Put The Default Files In Place

Minimum useful contents:

- `.github/ISSUE_TEMPLATE/bug_report.yml`
- `.github/ISSUE_TEMPLATE/feature_request.yml`
- `.github/ISSUE_TEMPLATE/task_chore.yml`
- `.github/ISSUE_TEMPLATE/spike_research.yml`
- `.github/ISSUE_TEMPLATE/config.yml`
- `.github/pull_request_template.md`
- tracker docs under `docs/tracker/`

Important override rule:

- if a repo has any files in its own `.github/ISSUE_TEMPLATE/`, GitHub stops using the default issue templates from the owner `.github` repo for that repo

### 3. Create Or Copy The Project

Create a private Project named `Delivery Tracker`.

If you already have a healthy reference Project, copying it is the fastest path because GitHub copies:

- views
- custom fields
- draft issues and their field values
- configured workflows except auto-add workflows
- insights

GitHub does not copy:

- items
- collaborators
- team links
- repository links
- auto-add workflows

That means a copied Project still needs repo linking and workflow finishing.

### 4. Normalize The Project Shape

Confirm these fields exist:

- built-ins: `Title`, `Assignees`, `Status`, `Labels`, `Linked pull requests`, `Milestone`, `Repository`, `Reviewers`, `Parent issue`, `Sub-issues progress`
- custom single-select fields: `Priority`, `Effort`
- iteration field: `Iteration`

Use this `Status` model:

- `Backlog`
- `Ready`
- `In Progress`
- `Blocked`
- `In Review`
- `Done`

Use this planning model:

- `Priority`: `P1`, `P2`, `P3`, `P4`
- `Effort`: `XS`, `S`, `M`, `L`, `XL`
- `Iteration`: two-week cadence starting Monday

### 5. Write The Project Role Down

Set the project description and readme so the owner role is explicit.

Current split:

- `BrynosRepo` = primary delivery tracker
- `bryant112` = sandbox/incubator and account-tooling tracker

If the role is not written down, the project will drift.

### 6. Build The Views

Minimum saved views:

1. `Ready` table filtered to `status:Ready`
2. `Active` board grouped by `Status`
3. `Backlog` table filtered to `status:Backlog`
4. `Bugs` table filtered to `label:"type:bug" -status:Done`
5. `Current Iteration` table filtered to `iteration:@current -status:Done`
6. `Releases` roadmap grouped by `Milestone`

### 7. Finish The Built-In Workflows

Enable or confirm:

- `Item added to project` -> set `Status` to `Backlog`
- `Item closed` -> set `Status` to `Done`
- `Pull request merged` -> set `Status` to `Done`
- optional auto-archive for old closed items

Then configure `Auto-add to project` for each linked repo with at least:

- repository = target repo
- filter = `is:issue`

Important GitHub behavior:

- copied projects do not bring auto-add workflows with them
- auto-add only catches future matching items created or updated after the workflow is enabled
- auto-add does not backfill old matching issues

## Per-Repo Bootstrap

### 1. Confirm The Repo Is Honest Scope

Before you wire anything:

- repo is not archived
- issues are enabled
- repo belongs in the chosen owner's active tracker

### 2. Decide Whether The Repo Inherits Or Overrides Defaults

Default path:

- let the repo inherit issue forms and PR template from the owner `.github` repo

Override only when the repo truly needs specialized intake.

### 3. Apply The Label Baseline

Use one canonical source repo and stamp the lean tracker labels onto the target repo.

Lean baseline:

- `type:bug`
- `type:feature`
- `type:chore`
- `type:spike`
- `needs:triage`
- `severity:s1`
- `severity:s2`
- `severity:s3`
- `status:blocked`
- `area:frontend`
- `area:backend`
- `area:infra`
- `area:data`
- `area:docs`
- `area:tooling`
- `area:cross-cutting`

During the April 21, 2026 rollout, the canonical source was `JCSDFoundry/clean-sweep` because it already had the target taxonomy.

### 4. Link The Repo To The Project

Link only repos that belong in the active tracker. Do not bulk-link every repo under an owner and call it done.

Keep linked:

- active delivery repos in the org tracker
- active incubators and account tooling in the personal tracker

Unlink:

- archive-style repos
- stale experiments
- low-signal repos that only add noise

### 5. Backfill Existing Work If Needed

If the repo already has issues you care about:

- add them to the Project manually or touch/update them after auto-add is enabled

Do not assume auto-add will discover old items on its own.

### 6. Create A First Milestone If The Repo Has A Real Near-Term Outcome

Use a milestone when there is an honest release or outcome target.

Do not create fake milestones just to fill a field.

### 7. Triage The First Batch

Minimum triage pass:

1. remove `needs:triage`
2. add one `area:*`
3. add `severity:*` for bugs
4. set `Priority`
5. set `Effort`
6. move to `Ready`, `Backlog`, or `Blocked`

## Scope Tuning After First Setup

After the first pass, reduce noise.

### Keep Tracker Scope Tight

- `BrynosRepo` should stay focused on active delivery work
- `bryant112` should stay focused on active incubators and account tooling

### Remove Generic Labels From Active-Flow Repos

Once the lean taxonomy is in place and active issues are using it, remove generic GitHub labels from the repos that are part of the real flow:

- `bug`
- `documentation`
- `duplicate`
- `enhancement`
- `good first issue`
- `help wanted`
- `invalid`
- `question`
- `wontfix`

Do this only after checking that no active issue still depends on those labels.

## Verification Checklist

The setup is healthy when all of these are true:

- the owner `.github` repo is public
- issue forms and PR template exist in the defaults repo
- the `Delivery Tracker` project has the full field set
- project description and readme clearly explain the owner role
- only the intended repos are linked
- linked repos use the lean tracker labels
- open issues can be filed through the default issue forms
- the project workflows are enabled in the GitHub UI
- at least one issue can move cleanly through `Ready` -> `In Progress` -> `In Review` -> `Done`

## Command Reference

Create a public defaults repo:

```bash
gh repo create OWNER/.github --public --description "Default issue forms and PR template for OWNER repositories."
```

Create a project:

```bash
gh project create --owner OWNER --title "Delivery Tracker"
```

Copy a reference project:

```bash
gh project copy 1 --source-owner SOURCE_OWNER --target-owner OWNER --title "Delivery Tracker"
```

View project metadata:

```bash
gh project view 1 --owner OWNER --format json
gh project field-list 1 --owner OWNER --format json
```

Clone labels from a canonical repo:

```bash
gh label clone SOURCE_OWNER/SOURCE_REPO --repo OWNER/REPO --force
```

Link a repo to the tracker:

```bash
gh project link 1 --owner OWNER --repo REPO
```

Unlink a repo from the tracker:

```bash
gh project unlink 1 --owner OWNER --repo REPO
```

List project items:

```bash
gh project item-list 1 --owner OWNER --format json
```

## Environment Notes

### WSL GitHub CLI Fix

If `gh auth status` is healthy but plain `gh` or `git push` fails in WSL, repair the wrapper at:

```text
/home/neand/.local/bin/gh
```

and point GitHub credentials at that wrapper. This is an account-level environment fix, not a repo-level fix.

### `gh project link` And `unlink` Quirk

In this environment, when you also pass `--owner`, prefer the bare repo name:

```bash
gh project unlink 1 --owner bryant112 --repo LANDSPY
```

not:

```bash
gh project unlink 1 --owner bryant112 --repo bryant112/LANDSPY
```

The owner-scoped form behaved more reliably during the April 21, 2026 rollout.

## Docs Checked

Checked against GitHub Docs on April 21, 2026:

- Default community health files: https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file
- Copying an existing project: https://docs.github.com/en/issues/planning-and-tracking-with-projects/creating-projects/copying-an-existing-project
- Built-in automations: https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/using-the-built-in-automations
- Auto-add workflows: https://docs.github.com/en/issues/planning-and-tracking-with-projects/automating-your-project/adding-items-automatically
