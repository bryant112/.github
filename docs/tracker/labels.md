# Label Taxonomy

This tracker keeps the label set intentionally small.

Two design choices are deliberate:

- `Priority` is a Project field, not a label. Keeping both creates drift and extra clicks.
- `Status` mostly lives in the Project. The only status label in MVP is `status:blocked` because blocked work is useful to find outside the Project too.

## MVP Labels

| Label | Color | Meaning | When to use |
| --- | --- | --- | --- |
| `type:bug` | `d73a4a` | Something is broken or behaving incorrectly. | Apply to bug reports only. |
| `type:feature` | `1f883d` | Net-new capability or meaningful enhancement. | Apply to feature work. |
| `type:chore` | `57606a` | Maintenance, cleanup, upgrades, refactors, or operational work. | Apply when the work matters but is not a feature or bug. |
| `type:spike` | `9a6700` | Time-boxed research used to reduce uncertainty. | Apply to investigation or feasibility work. |
| `needs:triage` | `fbca04` | New item still needs classification and planning metadata. | Applied automatically by the issue forms; remove after triage. |
| `severity:s1` | `b60205` | Critical bug. Work stops, a release is blocked, or core behavior is unusable. | Bugs only. |
| `severity:s2` | `d93f0b` | Major bug with meaningful impact but some workaround or reduced blast radius. | Bugs only. |
| `severity:s3` | `fbca04` | Minor bug, edge case, or cosmetic defect. | Bugs only. |
| `status:blocked` | `6e7781` | Work cannot move because of an external dependency, unanswered decision, or waiting state. | Add when an issue moves to `Blocked`. Remove when it is unblocked. |
| `area:frontend` | `0969da` | Browser, UI, interaction, client rendering, or front-end state. | Add one primary area label during triage. |
| `area:backend` | `1a7f37` | APIs, services, business logic, server behavior, or integrations. | Add one primary area label during triage. |
| `area:infra` | `bc4c00` | Deployment, hosting, CI, environments, secrets, or platform ops. | Add one primary area label during triage. |
| `area:data` | `0a7ea4` | Data models, migrations, analytics, ETL, or reporting pipelines. | Add one primary area label during triage. |
| `area:docs` | `8250df` | Documentation, onboarding content, runbooks, or written guidance. | Add one primary area label during triage. |
| `area:tooling` | `5e5ce6` | Developer tooling, scripts, local workflows, repo automation, or DX. | Add one primary area label during triage. |
| `area:cross-cutting` | `6f42c1` | Work that intentionally spans multiple areas and does not have one honest primary home. | Use sparingly when no single area label is a good fit. |

## Label Rules

- Every tracked issue should end up with exactly one `type:*` label.
- Every triaged issue should end up with one primary `area:*` label.
- Only bugs get `severity:*` labels.
- Only use `status:blocked` when the issue is truly waiting on something external to forward progress.
- Remove `needs:triage` as part of triage, not when the issue is first started.

## Why Priority Is Not a Label

Priority changes more often than type or area, and it matters most inside the Project's planning views. Keeping priority in a Project single-select field avoids duplicate editing and keeps backlog ordering simple.
