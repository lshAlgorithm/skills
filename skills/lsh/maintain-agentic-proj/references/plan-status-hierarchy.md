# STATUS.md / PLAN.md Hierarchy

Use this reference when adding, deleting, renaming, or editing `PLAN.md` or `STATUS.md`.

## Preferred STATUS.md-Only Model

Prefer one durable `STATUS.md` per useful hierarchy level. Structure it as:

- `Current Status`
- `How to Run Current Workflow`
- `Future Plans`
- `Retained Obsolete Intentions`
- `Artifact and Detail Pointers`

Parent status files should summarize and point down. Child status files should own local state, local future phases, and local artifact pointers.

## Optional PLAN.md

Use `PLAN.md` only when the project explicitly keeps future plans separate from current state.

If retained, each folder should have at most one `PLAN.md`, and it should be future-only. Current state, verified results, artifact maps, failures, and history belong in `STATUS.md`.

- Root or `spec/`: high-level project phases, research direction, and proposal-scale acceptance criteria.
- Experiment folder: experiment phases, dataset/model/workload choices, and evaluation gates.
- Submodule folder: implementation phases and sequence local to that submodule.

When cleaning:

- If the user wants STATUS.md-only, migrate useful future-plan content into `STATUS.md` and delete `PLAN.md`.
- If retaining `PLAN.md`, make the plan match the folder level.
- Remove completed, obsolete, or current-state material from `PLAN.md`; preserve needed history in `STATUS.md`.
- Keep unresolved tasks concrete and verifiable.
- Preserve future phases, but place them at the right level: direction in parent plans, execution in child plans.
- Move details down only when they belong exclusively to a child folder.
- Move summary up only when parent readers need it.
- Add or keep a short pointer to the relevant `STATUS.md` for current state, verified results, and history.

## STATUS.md

Use `STATUS.md` like a durable state map, not a diary.

A root or `spec/STATUS.md` should contain:

- Current best result or implementation.
- How to run the current maintained workflow, using exact commands and operational tools such as `uv`, `.venv`, `tmux`, GPU variables, model paths, endpoints, and log paths when relevant.
- Future project phases.
- Important environment constraints.
- Where authoritative artifacts live.
- Major remaining gaps.
- One-sentence tried, failed, obsolete, or superseded intentions that explain current state.

Subfolder `STATUS.md` files should:

- State only what is local to that folder.
- Reference parent status for global context.
- Reference child status files only when a reader must drill down.
- Avoid contradicting parent status.

## Historical Notes in STATUS.md

Keep history useful but compact:

- Retain obsolete intentions when they explain why the current state exists or prevent rediscovery.
- Write one sentence per obsolete intention: original intention plus why it is no longer current.
- Keep negative results and failures if they are scientifically or operationally relevant.
- Remove diary detail, repeated logs, and stale play-by-play.
- Defer obsolete or retained command recipes to `doc/` under the same folder; link them from the retained-intention sentence when useful.

Pattern:

```md
- <Old intention> was intended to <goal>, but was superseded/removed/failed because <reason>.
```

## Retained Workflow Docs

Use local `doc/` files for runnable details that are not current:

```text
<folder>/doc/<retained-or-obsolete-workflow>.md
```

These docs may include old `uv`, `.venv`, `tmux`, GPU/model, and command recipes needed to reproduce retained evidence. Keep `STATUS.md` short by linking to the doc instead of copying the recipe.

## Fixed-Point Maintenance

If a project has explicit hierarchy rules or hooks, follow them exactly.

Generic cascade:

1. For changed `STATUS.md`, walk upward and update ancestor `STATUS.md` files if they need to reflect child state.
2. For changed `PLAN.md`, walk downward and update descendant `PLAN.md` files if they conflict with the parent plan.
3. Repeat until a full pass produces no more edits.
4. Run the project's checker if one exists.

Never hide unresolved conflicts. Ask the user when files and artifacts cannot decide the current direction.
