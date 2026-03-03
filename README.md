# xCloud Docker Deploy Skill

[![Version](https://img.shields.io/badge/version-1.1.0-brightgreen.svg)](CHANGELOG.md)
[![License](https://img.shields.io/badge/license-Apache%202.0-green.svg)](LICENSE)
[![ClawHub](https://img.shields.io/badge/ClawHub-install-blue.svg)](https://clawhub.ai/Asif2BD/xcloud-docker-deploy)
[![SkillsMP](https://img.shields.io/badge/SkillsMP-indexed-purple.svg)](https://skillsmp.com)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-compatible-orange.svg)](https://claude.ai/code)
[![Codex CLI](https://img.shields.io/badge/Codex%20CLI-compatible-brightgreen.svg)](https://github.com/openai/codex)
[![xCloud](https://img.shields.io/badge/platform-xcloud.host-ff6b35.svg)](https://xcloud.host)

> **Deploy any project on xCloud — from zero to live in minutes.**  
> Auto-detects your stack, chooses the right deployment path, generates all needed files.

---

## What It Does

### Phase 0 — Smart Stack Detection

The skill **automatically detects your project type** before doing anything:

| Stack Detected | Recommended Path |
|---|---|
| WordPress | xCloud Native (1-click or Git) |
| Laravel | xCloud Native (composer + artisan) |
| PHP (generic) | xCloud Native |
| Node.js / Express | xCloud Native |
| Next.js / NestJS / Nuxt | Docker (build step required) |
| Python (FastAPI / Django) | Docker |
| Go / Rust | Docker |
| Existing docker-compose.yml | Adapt → Scenario A/B/C |

### Phase 1 — Docker Compose Adaptation

For existing Docker projects, handles 4 common xCloud blockers:

| Scenario | Signal | Fix |
|---|---|---|
| **Build-from-source** | `build: context: .` in compose | Generates GitHub Actions → builds → pushes to GHCR; replaces `build:` with `image: ghcr.io/...` |
| **Proxy conflict** | Caddy/Traefik/nginx-proxy service | Removes it, adds `nginx-router` with inline config, single port |
| **Multi-port** | Multiple `ports:` on different services | Routes all traffic through `nginx-router`, single exposed port |
| **External config files** | `./nginx.conf:/etc/nginx/...` | Embeds inline via `configs:` block |

---

## Quick Start

Once installed, just say:

> **"Make this work on xCloud"** — paste any `docker-compose.yml`, project files, or just your repo structure.

The skill detects your stack and produces:
- ✅ Modified `docker-compose.yml` (xCloud-compatible)
- ✅ `Dockerfile` (if needed — from templates)
- ✅ GitHub Actions workflow (for GHCR image builds)
- ✅ `.env.example` with all required variables
- ✅ Step-by-step xCloud UI deploy instructions

---

## Install

### Claude Code (CLI)
```bash
# Option 1: Install via ClawHub CLI
clawhub install xcloud-docker-deploy

# Option 2: Download .skill file directly
curl -L https://github.com/Asif2BD/xCloud-Docker-Deploy-Skill/releases/latest/download/xcloud-docker-deploy.skill \
  -o ~/.claude/skills/xcloud-docker-deploy.skill
```

### OpenAI Codex CLI
```bash
curl -L https://github.com/Asif2BD/xCloud-Docker-Deploy-Skill/releases/latest/download/xcloud-docker-deploy.skill \
  -o ~/.codex/skills/xcloud-docker-deploy.skill
```

### Claude.ai Projects
Download [`xcloud-docker-deploy.skill`](https://github.com/Asif2BD/xCloud-Docker-Deploy-Skill/releases/latest/download/xcloud-docker-deploy.skill) and upload to your Claude Project files.

### OpenClaw
```bash
clawhub install Asif2BD/xcloud-docker-deploy
```

### Cursor / Windsurf / Any AI Agent
Drop `xcloud-docker-deploy.skill` into the agent's `skills/` or workspace folder, or reference `SKILL.md` directly in your agent's context.

### Manual / Self-hosted
```bash
git clone https://github.com/Asif2BD/xCloud-Docker-Deploy-Skill.git
# Add SKILL.md to your agent's context
```

---

## What's Included

```
xcloud-docker-deploy/
├── SKILL.md                              # Core agent instructions
├── DETECT.md                             # Stack fingerprinting rules
├── README.md                             # This file
├── SECURITY.md                           # Security disclosure
├── CHANGELOG.md                          # Version history
├── LICENSE                               # Apache 2.0
│
├── assets/
│   └── github-actions-build.yml          # Ready-to-use GitHub Actions workflow
│
├── dockerfiles/
│   ├── laravel.Dockerfile                # Multi-stage PHP 8.3-fpm-alpine
│   ├── nextjs.Dockerfile                 # 3-stage Next.js standalone
│   ├── node-app.Dockerfile               # Multi-stage Node.js 20-alpine
│   ├── php-generic.Dockerfile            # PHP 8.3-apache (Symfony, CI4, Slim)
│   └── python-fastapi.Dockerfile         # Python 3.12-slim + uvicorn
│
├── compose-templates/
│   ├── laravel-mysql.yml                 # Laravel + Nginx + MySQL 8 + Redis 7 + Queue
│   ├── nextjs-postgres.yml              # Next.js + PostgreSQL 16
│   ├── nodejs-api-postgres.yml          # Node.js API + PostgreSQL 16
│   └── python-fastapi-postgres.yml      # FastAPI + PostgreSQL + Redis + Celery
│
├── references/
│   ├── xcloud-constraints.md            # xCloud rules & architecture
│   ├── xcloud-deploy-paths.md           # Native vs Docker decision guide
│   ├── xcloud-native-wordpress.md       # WordPress native deploy guide
│   ├── xcloud-native-laravel.md         # Laravel native deploy guide
│   ├── xcloud-native-nodejs.md          # Node.js native deploy guide
│   ├── xcloud-native-php.md             # PHP native deploy guide
│   ├── scenario-build-source.md         # Docker Scenario A deep-dive
│   ├── scenario-proxy-conflict.md       # Docker Scenario B deep-dive
│   └── scenario-multi-service-build.md  # Docker Scenario C deep-dive
│
└── examples/
    ├── laravel-app.md                    # End-to-end: Laravel → xCloud Native
    ├── nextjs-app.md                     # End-to-end: Next.js → xCloud Docker
    ├── rybbit-analytics.md               # Real-world: Caddy + multi-port
    ├── custom-app-dockerfile.md          # Real-world: build-from-source
    └── fullstack-monorepo.md             # Real-world: multi-service build
```

---

## Compatibility

| Platform | Install Method | Status |
|---|---|---|
| **Claude Code** (Anthropic) | `.skill` file in `~/.claude/skills/` | ✅ Full support |
| **OpenAI Codex CLI** | `.skill` file in `~/.codex/skills/` | ✅ Full support |
| **Claude.ai Projects** | Upload `.skill` to Project files | ✅ Full support |
| **OpenClaw** | `clawhub install` | ✅ Native |
| **Cursor** | Add to project context | ✅ Partial |
| **Windsurf** | Add to project context | ✅ Partial |
| **Any LLM agent** | Reference `SKILL.md` directly | ✅ Universal |

---

## xCloud-Specific Context

This skill is built around [xCloud.host](https://xcloud.host) constraints:

- ✅ No `build:` directives in compose — images must be pre-built
- ✅ Single exposed port only — SSL/reverse proxy handled by xCloud
- ✅ No bundled proxy containers (Caddy/Traefik/nginx-proxy) — conflicts with xCloud's proxy layer
- ✅ Config files must be inline (via Docker `configs:` block) — external file mounts may not persist

---

## Examples

### Rybbit Analytics (Caddy + multi-port)
Detected: Existing Docker stack with Caddy proxy + multiple services → Scenario B  
Fix: Remove Caddy, add nginx-router, single port 3080

### Next.js App (build-from-source)
Detected: Next.js → Docker path → use `dockerfiles/nextjs.Dockerfile` + `compose-templates/nextjs-postgres.yml`  
Fix: Add `output: 'standalone'`, generate GHCR workflow, expose port 3000

### Laravel App (native deploy)
Detected: `composer.json` + `artisan` → xCloud Native  
Fix: No Docker needed — composer install + artisan deploy hooks directly in xCloud UI

---

## Author

Built by **M Asif Rahman** ([@Asif2BD](https://github.com/Asif2BD))

- GitHub: [Asif2BD/xCloud-Docker-Deploy-Skill](https://github.com/Asif2BD/xCloud-Docker-Deploy-Skill)
- ClawHub: [clawhub.ai/Asif2BD/xcloud-docker-deploy](https://clawhub.ai/Asif2BD/xcloud-docker-deploy)
- xCloud: [xcloud.host](https://xcloud.host)

---

## License

[Apache 2.0](LICENSE) — free to use, modify, and distribute.
