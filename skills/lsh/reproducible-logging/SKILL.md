---
name: reproducible-logging
description: Use when running or preparing experiments, benchmarks, long tmux jobs, model serving, dataset setup, replay/evaluation commands, or agent workflows where exact commands, stdout/stderr, traces, metrics, reports, environment details, and failure modes must be captured for reproducibility and later audit.
---

# Reproducible Logging

## Goal

Make runs auditable without relying on chat history.

For important experiments, benchmarks, model-serving runs, dataset setup, replay/evaluation jobs, or long agent workflows, preserve enough evidence that a future agent can answer:

- What command ran?
- Where did it run?
- Which model, dataset, workload, config, GPU allocation, and code revision were used?
- Where are raw outputs and summaries?
- Did setup fail, partially complete, or produce usable evidence?

Use this skill with `agentic-project` or `maintain-agentic-proj` when the result also changes durable project state.

## Command Capture

For important commands, capture stdout and stderr:

```sh
command ... 2>&1 | tee path/to/run_name.run.log
```

For long jobs, use `tmux` when available or when the user asks. Keep the session name meaningful and record it in the run log or status file.

When launching a run, log:

- working directory
- exact command
- environment variables that affect the result
- model path or identifier
- dataset path or version
- GPU allocation such as `CUDA_VISIBLE_DEVICES`
- output directory
- start time

When a run completes or fails, log:

- exit status
- output paths
- summary metrics, if produced
- failure mode and traceback, if any
- whether the result is complete, partial, invalid, or failed

If network, TLS, proxy, package download, git clone, model download, or external fetch commands fail or hang, and the environment has a proxy workflow, try `proxy_off` in the same shell before retrying. Record the retry condition in the log.

## Run and Artifact Names

Use names that encode variables needed to distinguish results:

- model or implementation
- serving mode or tool mode
- workload or dataset
- concurrency, turn count, or request count
- parser, replay, scheduler, or cache policy

Avoid vague names like `test1`, `latest`, or `newrun`.

Follow the repository's existing artifact layout. If no convention exists, see `references/run-logging.md`.

## Completion Check

Before saying a run is reproducible:

1. Confirm the run log exists and includes the command or enough context to reconstruct it.
2. Confirm referenced traces, metrics, reports, and replays exist.
3. Inspect key output files, not just exit codes.
4. Record whether the result is real-system evidence, replay/simulator evidence, partial evidence, invalid, or failed.
5. Update relevant `STATUS.md` files only if the project uses them and the result changes durable state.
