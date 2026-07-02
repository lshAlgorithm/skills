# Run Logging Details

Use this reference when designing or cleaning experiment artifacts and run logs.

## Suggested Artifact Layout

Keep raw and derived outputs distinguishable:

- `traces/` for raw interaction traces or event streams
- `metrics/` for machine-readable measurements
- `reports/` for short human-readable summaries
- `replays/` for simulator or replay outputs
- `*.run.log` for stdout/stderr from the command that produced artifacts

Follow the repository's existing convention if it already uses different names.

## Good Log Content

Logs should make setup and execution problems visible:

- data/model/materialization progress before long network or disk steps
- server readiness checks and endpoint URLs when serving a model
- tool-call parser or schema errors when testing agents
- trace paths, metrics paths, report paths, and replay paths
- full error messages and tracebacks
- retry conditions, especially network/proxy changes

## Academic Experiment Logging

For academic or paper-facing experiments:

- Preserve raw traces and raw summaries.
- Generate concise human-readable reports beside raw outputs.
- Record negative results as carefully as positive results.
- Distinguish real-system evidence from simulator or replay evidence.
- Distinguish autonomous agent behavior from scripted fallback or synthetic stress.
- Record setup failures as failures.
- Keep enough metadata to compare runs without rereading every log.

## Cleanup

Keep logs when they prove:

- exact command execution
- setup or materialization details
- long experiment stdout/stderr
- failure modes needed to understand a result
- authoritative result generation

Clean or archive logs when they are:

- empty
- purely stale exploratory noise
- duplicated by a cleaner authoritative log
- named after obsolete runs no longer documented

Do not rewrite raw logs unless the user explicitly asks.
