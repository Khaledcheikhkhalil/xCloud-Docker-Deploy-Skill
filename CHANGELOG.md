# Changelog

## v1.1.0 — 2026-03-03

### Added
- `DETECT.md`: Stack fingerprinting — auto-detects WordPress, Laravel, PHP, Node.js, Next.js, NestJS, Nuxt, Python, Go, Rust
- **Phase 0 routing table** in `SKILL.md` — project type detection before any Docker work
- **5 production Dockerfiles**: Laravel (PHP 8.3-fpm), Next.js (standalone), Node.js (multi-stage), PHP generic (Apache), Python/FastAPI
- **4 compose templates**: Laravel+MySQL+Redis+Queue, Next.js+Postgres, Node.js API+Postgres, FastAPI+Postgres+Celery+Redis
- **4 native deploy guides**: WordPress (one-click + Git), Laravel (composer+artisan), PHP, Node.js
- **Decision matrix** (`references/xcloud-deploy-paths.md`): Native vs Docker by stack + DB + background jobs
- **2 new examples**: Laravel native end-to-end, Next.js Docker end-to-end
- README: SkillsMP badge, Codex CLI install instructions, full compatibility table

### Changed
- `SKILL.md` description updated to reflect full project-aware deployment capability
- README rewritten for SkillsMP/Claude Code/Codex CLI discoverability

## v1.0.0 — 2026-03-03

### Initial Release
- Scenario A: Build-from-source (generate GitHub Actions → GHCR)
- Scenario B: Proxy conflict (remove Caddy/Traefik, add nginx-router)
- Scenario C: Multi-service build (matrix GitHub Actions workflow)
- External config file embedding via Docker `configs:` block
- References: xCloud constraints, scenario deep-dives
- Examples: Rybbit Analytics, custom Dockerfile, fullstack monorepo
