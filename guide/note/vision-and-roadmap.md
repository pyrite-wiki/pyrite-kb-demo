---
id: vision-and-roadmap
type: note
title: "Vision and Roadmap"
tags: [overview, roadmap, vision]
importance: 7
---

## The vision

Pyrite is building toward a future where knowledge infrastructure is self-configuring. An autonomous agent encounters a domain, builds a Pyrite extension for it (entry types, validators, MCP tools), provisions a KB, and starts working — all without human intervention. The schema is the program. Pyrite is the runtime.

Every milestone moves toward this goal: making structured, validated, queryable knowledge the default for both human and AI workflows.

## Current status: v0.20.0 (beta)

Pyrite has shipped 18 milestones covering:

- **Core platform**: CLI, REST API, MCP server, SvelteKit web UI
- **Storage**: Git-native markdown with SQLite FTS5 + optional PostgreSQL
- **Search**: Keyword (FTS5), semantic (sentence-transformers), hybrid (RRF)
- **Auth**: GitHub OAuth, per-KB permissions, rate limiting
- **Deployment**: Docker, Railway, Render, Fly.io one-click deploy
- **Plugins**: software-kb, journalism-investigation, zettelkasten, cascade, encyclopedia
- **Agent workflow**: Kanban for agent teams, work session logging, quality gates

## What's next

- **Extension registry** — public directory for sharing plugins
- **Obsidian migration** — import from Obsidian vaults
- **Quartz static site export** — publish KBs as static sites on GitHub Pages
- **Hosting security hardening** — for journalist deployments
- **Event bus / webhooks** — real-time integration with external tools

## Architecture decisions

Pyrite's architecture is documented in 22 ADRs (Architecture Decision Records). Key decisions:

- **ADR-0001**: Git-native markdown storage (files are the source of truth)
- **ADR-0002**: Plugin system via Python entry points
- **ADR-0003**: Two-tier durability (git for content, SQLite for index)
- **ADR-0006**: MCP three-tier tool model (read/write/admin)
- **ADR-0007**: AI integration with BYOK (bring your own key)
- **ADR-0008**: Schema-as-config (kb.yaml defines types and validation)

All ADRs are browsable in the pyrite KB on this demo site.

## Open source

Pyrite is MIT licensed. Source at [github.com/pyrite-wiki/pyrite](https://github.com/pyrite-wiki/pyrite).

Contributions welcome — see [CONTRIBUTING.md](https://github.com/pyrite-wiki/pyrite/blob/main/CONTRIBUTING.md).
