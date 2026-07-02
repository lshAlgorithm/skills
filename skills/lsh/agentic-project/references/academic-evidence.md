# Academic Evidence Guidance

Use this reference when maintaining research experiments, agent workflows, benchmark runs, or paper-facing evidence.

## Evidence Labels

Use precise labels:

- **Real-system evidence**: collected from the actual system or agent workflow being claimed.
- **Replay evidence**: derived by replaying traces through a simulator or scheduler model.
- **Simulator evidence**: synthetic or model-only evaluation, useful but not proof of system performance.
- **Partial evidence**: setup, trace, or metric is incomplete but still informative.
- **Failure**: setup failed, trace invalid, parser failed, or workload did not exercise the intended behavior.

Do not blur these categories. A negative replay result is still useful if recorded honestly.

## STATUS.md for Experiments

`STATUS.md` should briefly include:

- Current authoritative result.
- How to run or reproduce the current maintained workflow, including `uv`, `.venv`, `tmux`, GPU/model variables, and log paths when relevant.
- Future plans or next phases at that folder's level.
- Paths to traces, metrics, reports, replays, and logs.
- Verification commands or validators that passed.
- Major limitations.
- Tried-but-failed, obsolete, or superseded intentions that explain why the current approach exists, written as one sentence each.

Keep historical notes concise. Preserve the original intention and why it is no longer current; do not turn `STATUS.md` into a chronological diary.

Example:

```md
- Regex tool-call parsing was intended as a quick Qwen3-4B harness path, but was superseded because parse errors made OpenAI native tools the cleaner evidence path.
```

## Running Current and Retained Workflows

For the current maintained workflow, keep a short runnable recipe in the local `STATUS.md`:

```md
## How to Run Current Workflow

- Environment: `uv sync` or `.venv/bin/python ...`
- Long job: `tmux new -s <session>`
- Command: `<exact command> 2>&1 | tee <run-log>`
- Outputs: `<trace/report/summary paths>`
```

For obsolete or retained workflows, move the runnable recipe into `doc/` under the same folder:

```text
<folder>/doc/<short-retained-workflow>.md
```

Then keep only a one-sentence retained intention plus a link in `STATUS.md`. Do not copy old command recipes into status unless they are still the current maintained path.

## Future Phases

Prefer putting future phases directly in `STATUS.md` under a `Future Plans` section:

- Root/spec plans: proposal-scale phases, major research milestones, and broad acceptance criteria.
- Experiment plans: dataset/model/workload phases and evaluation gates.
- Local implementation plans: concrete phases for one module or harness.

Use separate `PLAN.md` files only when the repo explicitly keeps a plan hierarchy. Avoid duplicating child implementation phases in parent status files. Parent status files should point down when details belong to a child folder.

## Artifact Hygiene

Organize artifacts so a reader can answer:

- Which model or implementation?
- Which method, serving mode, or tool mode?
- Which workload or dataset?
- Which run is authoritative?
- Which outputs are raw versus summarized?

Follow local conventions. If the existing layout is confusing, make the smallest cleanup that improves navigation.

## Decision Records

Use an ADR only for decisions likely to be challenged again:

- hard to reverse
- surprising without context
- chosen from real alternatives

Ordinary failed attempts, temporary conclusions, and active future steps belong in `STATUS.md` unless the repo explicitly uses a separate `PLAN.md`.
