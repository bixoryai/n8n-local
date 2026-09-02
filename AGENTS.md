# AGENTS.md — n8n-local

Live facts for this PC’s n8n stack. Product intent for the posting desk lives in `C:\Coding\BixoryAI\social-desk`. Do not put tokens, passwords, or API keys here.

## What this is

Docker Compose stack for **n8n 2.36.0**, Postgres 17, and Qdrant. Ollama runs on the **Windows host**, not in this compose file.

Social Desk (`C:\Coding\BixoryAI\social-desk`) is a client of this instance. Its workflow JSON lives in that repo (`n8n/*.json`). After you edit a live Social Desk workflow, re-export there.

## Run

| Surface | URL |
|---|---|
| n8n | http://localhost:5678 |
| Social Desk console | http://127.0.0.1:8765/social-console.html (`python serve.py` in social-desk) |

```
cd C:\Coding\BixoryAI\n8n-local
docker compose up -d
```

Image: `n8nio/n8n:2.36.0`. Do not start n8n from social-desk’s `docker-compose.standalone.yml`.

Ollama for Social Desk drafts: `http://host.docker.internal:11434` (`llama3.2:latest`).

## File access

`N8N_RESTRICT_FILE_ACCESS_TO=/data/shared;/home/node/.n8n-files` is required. n8n 2.x otherwise cannot write Social Desk files under `/data/shared`.

| What | Windows | In n8n |
|---|---|---|
| Shared root | `.\shared\` | `/data/shared` |
| Social Desk queue / media / voice / review | `.\shared\social-desk\` | `/data/shared/social-desk\` |

`shared/social-desk/` is gitignored (runtime: queue, voice, review, media).

## Do not

- Commit `.env`, credentials, `.kilocode/`, or `shared/social-desk/`.
- Invent Social Desk workflow IDs here — those stay in social-desk `AGENTS.md`.
- Run `docker-compose.standalone.yml` from social-desk.
