---
id: for-developers
type: note
title: "For Developers"
tags: [development, api, cli, mcp]
importance: 6
---

Pyrite exposes four interfaces to your knowledge bases. Use whichever fits your workflow.

## CLI

The `pyrite` command handles all KB operations:

```bash
pyrite search "query" -k my-kb          # search
pyrite get entry-id -k my-kb            # read an entry
pyrite create -k my-kb --type note ...  # create
pyrite update entry-id -k my-kb ...     # update
pyrite backlinks entry-id -k my-kb      # find what links here
pyrite index sync                       # rebuild index
pyrite schema validate -k my-kb         # validate all entries
```

All commands support `--format json` for scripting and agent consumption.

## REST API

Start with `pyrite-server`. Full OpenAPI docs at `/docs`.

```bash
GET  /api/search?q=query&kb=my-kb&mode=hybrid
GET  /api/entries/{id}?kb=my-kb
POST /api/entries  { kb, type, title, body, tags }
GET  /api/graph?kb=my-kb&depth=2
GET  /api/kbs/{name}/orient
```

## MCP Server

See [[connecting-via-mcp]] for configuration. The MCP server exposes tools in three tiers (read/write/admin) with per-client rate limiting.

## Python API

```python
from pyrite.config import load_config
from pyrite.storage.database import PyriteDB
from pyrite.services.search_service import SearchService

config = load_config()
db = PyriteDB(config.settings.index_path)
search = SearchService(db, config)

results = search.search("query", kb_name="my-kb", mode="hybrid")
```

## Architecture

- **Storage**: Markdown files (source of truth) + SQLite FTS5 index (derived)
- **Backends**: SQLiteBackend (default, local) or PostgresBackend (server deployments)
- **Plugins**: Python entry points, 15-method protocol
- **Web UI**: SvelteKit + Svelte 5, Cytoscape.js for graph, Tiptap for editing

Source: [github.com/pyrite-wiki/pyrite](https://github.com/pyrite-wiki/pyrite)
