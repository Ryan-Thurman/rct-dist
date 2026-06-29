# RCT — beta

> Template for the **public distribution repo**'s README. Copy this into that repo
> alongside the release wheels; fill in the `<…>` release URL. (This file lives here
> in the source repo only as the maintained source of truth.)

RCT builds a queryable graph of your codebase — files, functions, classes, calls,
routes, constraints — and serves it as a dashboard you can explore. This is a private
beta: run it on your own machine and tell me what's useful and what's confusing.

## Install (macOS, Apple Silicon)

One line — no Python setup needed, `uv` fetches a matching interpreter:

```bash
uv tool install "https://github.com/Ryan-Thurman/Ryan-Thurman/rct-dist/releases/download/v0.0.1/ryans_context_toolbelt-0.0.1-cp313-cp313-macosx_14_0_arm64.whl"
```

> Need `uv`? `curl -LsSf https://astral.sh/uv/install.sh | sh`
> Update later: re-run the command above with the new release URL plus `--reinstall`.

## Use it

```bash
rct index /path/to/your/repo     # build the graph (give it a minute on a big repo)
rct dashboard                    # serve the explorer
```

Then open the printed URL (default <http://localhost:8000>). Start on **Overview**, try
the **Graph** and **Layers** views, search in the left rail, and click a node to inspect
its callers/callees/usages/constraints.

## Optional: semantic search

Lexical (keyword) search and the whole dashboard work out of the box. To also get
**semantic** search (find code by meaning, not just keywords), fetch the embedding
model once — it comes from a dedicated repo over plain HTTPS, **no Hugging Face**, so it
works on locked-down networks:

```bash
rct fetch-model        # ~580MB, one time; auto-detects MLX (Apple Silicon) / Ollama
rct index --embed /path/to/your/repo   # re-index with embeddings
```

Without this, the Semantic search toggle quietly falls back to lexical and tells you so.

## What needs what

| Feature | Requirement |
|---|---|
| Dashboard, graph, lexical search | nothing — works offline |
| Semantic search | `rct fetch-model` (one-time, no Hugging Face) |
| AI prose summaries | an LLM API key (optional) |

## Feedback

Just message me on **Slack or email** — what did you expect a click to do, what would
you want to see, was it helpful? Rough notes are perfect.

---

*Internal evaluation build. Not for redistribution. All rights reserved.*
