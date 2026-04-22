# Current Baseline

Last updated: April 21, 2026

This file is the durable memory note for the current `bryant112` tracker baseline.

## Role

`bryant112` is the sandbox, incubator, and account-tooling owner.

Its `Delivery Tracker` project is intentionally not a catch-all for every personal repo. It is the working tracker for active incubators and account-level tooling only.

## Defaults Repo

- `bryant112/.github` is public
- it is the account-wide source of default issue forms, PR template, and tracker docs

## Project

- project name: `Delivery Tracker`
- owner: `bryant112`
- visibility: private
- project number: `1`
- field count: `13`

Planning fields in use:

- `Status`
- `Priority`
- `Effort`
- `Iteration`

## Linked Repos

As of this baseline, the project is intentionally linked only to:

- `bryant112/.github`
- `bryant112/chsarp-dev-overview`
- `bryant112/LANDSPY`
- `bryant112/theLab-POC`
- `bryant112/madSci`
- `bryant112/StateBridge`
- `bryant112/feature-branch-test-brief`

Repos intentionally left unlinked:

- archive-style repos
- old personal repos
- noisy repos that do not belong in the current incubator view

## Label Policy

Active-flow repos in this owner should use only the lean tracker taxonomy:

- `type:*`
- `area:*`
- `severity:*`
- `needs:triage`
- `status:blocked`

Generic GitHub labels were pruned from the active-flow repos during this rollout after checking that live issues were already using the lean taxonomy.

## Graduation Rule

When a personal incubator becomes real delivery work, graduate it out of this tracker and into the `BrynosRepo` delivery owner instead of letting both trackers claim it.

## Manual Or UI-Only Follow-Ups

These still matter after the CLI/bootstrap pass:

- confirm or duplicate `Auto-add to project` workflows in the GitHub Project UI
- keep the `Item added` -> `Backlog` workflow enabled
- keep the `Item closed` -> `Done` workflow enabled
- keep the `Pull request merged` -> `Done` workflow enabled

Remember:

- auto-add does not backfill old matching issues
- copied projects do not bring auto-add workflows with them

## Rollout Notes

- during this rollout, `gh project copy` from the reference project produced the full field schema but the `bryant112` project description and readme still needed manual normalization afterward
- during this rollout, `gh project unlink` behaved more reliably with `--repo REPO` than with `--repo OWNER/REPO` when `--owner` was already provided
