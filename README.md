# RCT — beta

RCT builds a queryable graph of your codebase — files, functions, classes, calls,
routes, constraints — and serves it as a dashboard you can explore. This is a private
beta: run it on your own machine and tell me what's useful and what's confusing.

## Install (macOS, Apple Silicon)

One line — no Python setup needed, `uv` fetches a matching interpreter:

```bash
uv tool install --python 3.13 "ryans-context-toolbelt[langs] @ https://github.com/Ryan-Thurman/rct-dist/releases/download/v0.5.0/ryans_context_toolbelt-0.5.0-cp313-cp313-macosx_14_0_arm64.whl"
```

`--python 3.13` matches the wheel; `[langs]` adds the Go/Rust/Java/Ruby parsers (without it those files are skipped).

> Need `uv`? `curl -LsSf https://astral.sh/uv/install.sh | sh`
> Update later: re-run the command above with the new release URL plus `--reinstall`.
> After upgrading, re-run `rct index` on your repos. A new release can change what is
> parsed, and the first index after an upgrade does a full re-parse.

## Use it

```bash
rct index /path/to/your/repo     # build the graph (give it a minute on a big repo)
rct dashboard                    # serve the explorer
```

Then open the printed URL (default <http://localhost:8000>). Start on **Overview**, try
the **Graph** and **Layers** views, search in the left rail, and click a node to inspect
its callers/callees/usages/constraints.

The **Run** view reindexes, measures CRAP and coverage, runs the security scan, code sweep
and lint, and builds the **Scorecard** (under *Assess*) from the dashboard, one click each.

## Use it from Cursor

```bash
cd /path/to/your/repo
rct wire cursor --hooks          # MCP tools + rule + metrics hooks
```

Reload Cursor afterwards. It reads those files when a session starts.

## What needs what

| Feature | Requirement |
|---|---|
| Dashboard, graph, search | nothing — works offline |
| Security scan, code sweep, lint, scorecard | a one-time `rct scanners install` (downloads pinned scanners, their rules and trivy's ~1.8 GB vulnerability database) |
| AI prose summaries | optional: a Cursor/Claude/Codex CLI seat (`rct summarize --cli …`) or an LLM API key |

## Feedback

Just message me on **Slack or email** — what did you expect a click to do, what would
you want to see, was it helpful? Rough notes are perfect.

---

*Internal evaluation build. Not for redistribution. All rights reserved.*