---
name: tmux-session
description: Persistent tmux sessions with upgraded shells, use tmux for long-term works
license: MIT
compatibility: posix-shell
metadata:
  audience: developer
  workflow: session-management
---
## What I do
- Create a new session, preferably named after a short version of the project name.
- Create a pane in the session, named after the work to be done.
- Execute commands inside a specific `tmux` session, using commands like `tmux send-keys -t [session_name]:[pane_name]`. Do not use the name that has already existed.
- Immediately upgrade the default `/bin/sh` to `bash` upon creating a new pane or window.
- Ensure the current directory is under the root of the project.

## When to use me
Use this when opening a new workspace, running long-running processes, or when the user requires session persistence for review.
