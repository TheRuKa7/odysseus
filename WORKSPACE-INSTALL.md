# Odysseus — workspace install (June 2026)

Cloned from [TheRuKa7/odysseus](https://github.com/TheRuKa7/odysseus.git) into this repo for **G2 (local AI workstation)**.

**Navigation path:** `zuvana/tools/odysseus/` (junction to this folder). Workspace index: [`../WORKSPACE-MAP.md`](../WORKSPACE-MAP.md).

## Status

| Step | State |
|------|--------|
| Clone | Done |
| `venv` + `pip install -r requirements.txt` | Done |
| `.env` from `.env.example` | Done |
| `python setup.py` (DB + admin user) | Done |

## API keys

Secrets live in the workspace vault only: [`../secrets/api-keys.local.env`](../secrets/api-keys.local.env).

Before enabling cloud models in Odysseus:

```powershell
cd "c:\RuKaStash\PM-Processes\PM Processes"
powershell -ExecutionPolicy Bypass -File meta\scripts\Apply-VaultToProject.ps1 -Project odysseus
```

Local Ollama does **not** require `OPENAI_API_KEY`. See [`../docs/LOCAL-AI-SETUP.md`](../docs/LOCAL-AI-SETUP.md).

## Start (Windows, native)

From this folder:

```powershell
powershell -ExecutionPolicy Bypass -File .\launch-windows.ps1
```

Or manually:

```powershell
.\venv\Scripts\python.exe -m uvicorn app:app --host 127.0.0.1 --port 7000
```

Open **http://localhost:7000** — login **admin** with the password printed when `setup.py` first ran (change it after login). To set a known password before setup, use `ODYSSEUS_ADMIN_PASSWORD` in `.env` and re-run setup on a fresh DB.

## Ollama (optional)

Point Odysseus at local Ollama OpenAI-compatible API: `http://localhost:11434/v1` (see upstream `README.md`).

## Docker

Alternative: `docker compose up -d --build` or `update_windows.bat` in repo root.

## Notes

- This directory is its **own git repo** (nested clone). Updates: `git pull` inside `odysseus/`.
- User data (`data/`, `logs/`, `.env`, DB files) is gitignored by Odysseus — safe to keep local only.
