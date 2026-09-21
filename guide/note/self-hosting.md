---
id: self-hosting
type: note
title: "Self-Hosting Pyrite"
tags: [deployment, docker, self-hosting, privacy]
importance: 7
---

Pyrite runs anywhere — your laptop, a $4/month VPS, or a Docker container. You own your data completely.

## Local install (simplest)

```bash
pip install "pyrite[all]"
pyrite init --template research --path my-kb
pyrite-server                    # web UI at http://localhost:8088
pyrite mcp                       # MCP server for AI agents
```

No server needed. Everything runs locally with SQLite.

## Docker (recommended for servers)

```bash
git clone https://github.com/pyrite-wiki/pyrite.git && cd pyrite
bash deploy/selfhost/setup.sh kb.example.com
```

This installs Docker, starts Pyrite + Caddy (auto TLS), and creates your first KB. Total setup time: ~10 minutes.

### Create users

```bash
docker compose -f deploy/selfhost/docker-compose.yml exec pyrite \
  python /app/deploy/selfhost/create-user.py admin yourpassword
```

## One-click deploy

Deploy buttons available for:
- **Railway** — simple container hosting
- **Render** — auto-deploy from GitHub
- **Fly.io** — edge deployment with persistent volumes

See the [Deploy documentation](https://pyrite.wiki/docs/deploy) for details.

## Privacy and security

Pyrite is designed for privacy-conscious users:

- **No telemetry** — zero outbound network calls unless you initiate them
- **No cloud dependency** — everything runs on your hardware
- **Git-native storage** — your data is plain markdown files, portable and auditable
- **AI is BYOK** — bring your own API key, or use local models. No AI runs without your explicit configuration
- **Per-KB access control** — read/write/admin tiers, per-KB permissions

For journalism deployments with specific threat models, see the hosting security requirements in the Pyrite project KB.

## Connecting AI agents to your server

See [[connecting-via-mcp]] for MCP configuration. AI agents connect locally to your Pyrite install — they don't need access to the server directly.
