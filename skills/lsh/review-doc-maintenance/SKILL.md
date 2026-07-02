---
name: review-doc-maintenance
description: Review project documentation maintenance quality and write the review to a temporary markdown file. Use when the user asks for an independent reviewer or audit of STATUS.md, README, doc/, retained/obsolete notes, hierarchy consistency, stale references, piled-up documentation, or whether docs should be cleaned before the main agent edits them.
---

# Review Doc Maintenance

## Role

Act as a documentation-maintenance reviewer, not the fixer.

Your output is a temporary markdown review file. Do not edit project docs while using this skill unless the user separately asks the main agent to apply the review.

## Workflow

1. Locate the project root and read project instructions such as `AGENTS.md` and `README.md`.
2. Inventory durable docs, excluding dependency/build folders:

```sh
find . -path './.venv' -prune -o \
  \( -name STATUS.md -o -name PLAN.md -o -name README.md -o -path '*/doc/*.md' \) -print | sort
```

3. Read parent docs before child docs.
4. Check whether docs are easy to maintain:
   - `STATUS.md` has clear current status, how to run current workflows, future plans, retained obsolete intentions, and artifact/detail pointers.
   - Current runnable commands live in the relevant `STATUS.md`, including tools such as `uv`, `.venv`, `tmux`, GPU/model variables, endpoints, logs, and output paths when relevant.
   - Obsolete or retained runnable recipes are deferred to `doc/` under the same folder and linked from `STATUS.md`.
   - Detailed metrics/results are in reports, summaries, logs, traces, or result files, not copied into status.
   - Parent status files summarize and point down; child status files own local details.
   - Retained obsolete intentions are one sentence each and explain why the old direction is no longer current.
   - No stale references to deleted paths, obsolete methods, or conflicting next steps remain.
5. Verify major artifact pointers exist when practical.
6. Write the review to a temp file and make that file the skill result.

## Temp File Output

Write the review to:

```sh
${TMPDIR:-/tmp}/doc-maintenance-review-$(date +%Y%m%d-%H%M%S).md
```

If the environment cannot expand shell variables, choose an equivalent unique markdown path under `/tmp`.

The final response when using this skill should primarily return the temp file path. The main agent should read that file before applying corrections.

## Review File Format

Use this structure:

```md
# Documentation Maintenance Review

Project: <absolute path>
Generated: <timestamp>

## Verdict

<Clean / Needs cleanup / Blocked>, with one short paragraph.

## Findings

### Critical

- <File path>: <issue>. Why it matters. Suggested correction.

### Important

- <File path>: <issue>. Why it matters. Suggested correction.

### Minor

- <File path>: <issue>. Suggested cleanup.

## Hierarchy Check

- Parent/child consistency:
- Missing or redundant STATUS.md / PLAN.md:
- Stale links or deleted paths:

## Runbook Check

- Current workflows missing run commands:
- Commands that should move to doc/:
- Missing `uv`, `.venv`, `tmux`, GPU/model/log/output details:

## Suggested Fix Order

1. <First correction>
2. <Second correction>

## Do Not Change

- <Docs or artifacts that should be preserved>

## Evidence Reviewed

- <Files, reports, commands, or artifact paths inspected>
```

If a section has no entries, write `None found`.

## Reviewer Standards

- Be specific and file-grounded.
- Prefer fewer high-signal findings over long commentary.
- Do not duplicate detailed result metrics in the review; point to where they already live.
- Do not propose deleting evidence required for reproducibility.
- Mark unresolved ambiguity explicitly instead of guessing.
- If a hook or checker exists, note the exact command the main agent should run after fixes.
