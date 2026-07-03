---
name: proxy-off-network
description: Use when any internet, TLS, proxy, package download, PyPI/npm/git clone, curl/wget, model download, or external network command fails or hangs unexpectedly. Try disabling the shell proxy with `proxy_off` before retrying the same network operation.
---

# Proxy-Off Network Recovery

When a network operation fails with symptoms such as TLS handshake errors, proxy failures, repeated download retries, connection resets, or unexplained hangs, first try:

```sh
proxy_off
```

Then retry the original command in the same shell or tmux pane.

## Workflow

1. Keep the failing command and exact error in mind.
2. Run `proxy_off` in that shell session.
3. Retry the same command without changing unrelated variables.
4. If working in tmux, run `proxy_off` inside the target tmux pane before sending the retry command.
5. If the retry works, record that proxy state was the cause or likely cause.
6. If the retry still fails, continue normal network debugging and report both attempts.

Do not globally install Python packages as a workaround. For Python environments, still follow the active environment-management skill, such as `uv-python`; `proxy_off` only changes network/proxy state.
