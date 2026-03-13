# lobs-memory-plugin

OpenClaw plugin that provides `memory_search` and `memory_get` tools by proxying to the [lobs-memory](https://github.com/lobs-ai/lobs-memory) search server.

## What it does

- **memory_search** — semantic search across indexed markdown docs (BM25 + vector + reranking)
- **memory_get** — read specific lines from files found via search
- **Auto-injection** — hooks into `before_prompt_build` to inject relevant memory snippets into fresh sessions
- **Service management** — starts/stops the lobs-memory server and reranker sidecar

## Setup

1. Clone this repo
2. Point OpenClaw to it in `openclaw.json`:
```json
{
  "plugins": {
    "load": {
      "paths": ["/path/to/lobs-memory-plugin"]
    },
    "slots": {
      "memory": "memory-lobs"
    },
    "entries": {
      "memory-lobs": { "enabled": true }
    }
  }
}
```
3. Ensure `lobs-memory` server is at `~/lobs-memory` (or set `LOBS_MEMORY_DIR` env var)
4. Restart OpenClaw gateway

## Requirements

- lobs-memory server (Bun + TypeScript)
- LM Studio running with embedding model loaded
- OpenClaw with plugin support
