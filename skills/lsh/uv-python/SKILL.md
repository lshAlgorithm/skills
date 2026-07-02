---
name: uv-python
description: When you need to manage a python environment, use uv.
license: MIT
compatibility: python
metadata:
  audience: python-developer
  workflow: package-management
  documentation: https://docs.astral.sh/uv/pip/environments/
---
## What I do
- **Environment Creation:** Initialize local virtual environments explicitly using `uv venv [ProjName]` in the project root.
- **Activation** Use `. .venv/bin/activate` under the project root folder; or add `.venv/bin/python` before executing python scripts.
- **Dependency Management:** Use `uv pip install [package]` for adding libraries, leveraging its comprehensive caching and resolution logic.
- **State Synchronization:** Prefer `uv pip sync requirements.txt` (if a lockfile exists) to ensure the environment exactly matches the definition.
- **Isolation:** Never install packages globally. Ensure all operations target the local `.venv`.
- **Resolution:** Rely on `uv`'s resolver to handle dependency conflicts, prioritizing pre-built binary wheels for speed.
- More information refers to https://docs.astral.sh/uv/pip/environments/

## When to use me
Use this immediately upon entering a directory containing Python code or a `pyproject.toml`/`requirements.txt`.
Specifically applicable for:
- Pure-Python projects.
- Projects relying on pre-built wheels from other languages (C/Rust/etc).
- **Note:** If source compilation of complex non-Python extensions is strictly required and fails under `uv`, fall back to standard `pip` only after a failed attempt.
