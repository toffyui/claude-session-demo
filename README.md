# Claude Session Demo

Demo repository for the **"AI agent team"** presentation: a minimal Angular + Spring Boot
dashboard that a team of Claude Code agents extends live on stage.

This repo is the **"before" state**. The demo itself adds a *team status* panel
(backend endpoint + frontend component) — that code is intentionally absent here.

## Structure

```
├── CLAUDE.md            # Daniel AI — team lead persona & delegation rules
├── .claude/
│   ├── settings.json    # enables the experimental Agent Teams feature
│   └── agents/          # 7 agent definitions (Chiara, Martin, Yuiko, Eva, Chris, Adrian, Alex)
├── frontend/            # Angular 20 dashboard shell (proxy to backend configured)
└── backend/             # Spring Boot 3 / Java 17, one example endpoint: GET /api/health
```

## Prerequisites

- Node.js 20+ and npm
- Java 17+ and Maven
- Claude Code v2.1.32+ (`claude --version`)
- For split-pane demo mode: tmux or iTerm2

## Setup & verify (do this before the demo!)

```bash
# Frontend
cd frontend
npm install
npm test                 # 2 specs, should pass in well under a minute

# Backend
cd ../backend
mvn test                 # 1 fast unit test, no Spring context startup

# Run the app
mvn spring-boot:run      # backend on :8080
# in another terminal:
cd frontend && npm start # Angular on :4200, /api proxied to :8080
```

Open http://localhost:4200 — you should see the dashboard shell.
Check http://localhost:4200/api/health returns `{"status":"ok"}` (proxy working).

## Running the demo

```bash
tmux            # or: tmux -CC in iTerm2 (recommended for split panes)
claude
```

Then give Claude (Daniel) the demo prompt — see the presentation runbook.
The agent team will add the team status panel to this codebase; afterwards
restart `npm start` / `spring-boot:run` and show the new panel live.

To reset the repo to the "before" state between rehearsals:

```bash
git reset --hard && git clean -fd
```
