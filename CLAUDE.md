# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Key Docs to Read
- `README.md` for Docker/Makefile workflows, environment variables, and MCP setup.
- `.github/copilot-instructions.md` for architecture notes and development commands.

## Common Commands

### Backend (.NET)
- Build solution: `dotnet build OpenDeepWiki.sln`
- Run API: `dotnet run --project src/OpenDeepWiki/OpenDeepWiki.csproj`

### Frontend (Next.js)
- Install deps: `cd web && npm install`
- Dev server: `npm run dev`
- Build: `npm run build`
- Lint: `npm run lint`
- Prod start: `npm run start`

### Docker/Makefile
- Build all images: `make build`
- Run all services (logs): `make dev`
- Run backend only: `make dev-backend`
- Start services (detached): `make up`
- Stop services: `make down`
- Tail logs: `make logs`

## High-Level Architecture

### Solution Layout
- `OpenDeepWiki.sln` includes current OpenDeepWiki projects plus legacy KoalaWiki projects; favor `src/OpenDeepWiki/*` and `web/*` for active development.

### Backend (ASP.NET Core)
- API entry point: `src/OpenDeepWiki/Program.cs` (MiniApis + OpenAPI + Scalar in dev).
- Agent orchestration: `src/OpenDeepWiki/Agents/` (constructed via `AgentFactory`).
- Models & services: `src/OpenDeepWiki/Models/` and `src/OpenDeepWiki/Services/` for request/response DTOs and domain services.

### Data Layer (EF Core)
- Entities: `src/OpenDeepWiki.Entities/` (e.g., Users, Repositories, DocDirectory).
- Core context contract + base: `src/OpenDeepWiki.EFCore/MasterDbContext.cs` with `IContext` and shared model configuration.
- Provider contexts: `src/EFCore/OpenDeepWiki.Sqlite/SqliteDbContext.cs` and `src/EFCore/OpenDeepWiki.Postgresql/PostgresqlDbContext.cs`.

### Frontend (Next.js App Router)
- App entry/layout: `web/app/layout.tsx` with routes in `web/app/*`.
- Shared UI: `web/components/*` and hooks in `web/hooks/*`.
- API/types: `web/types/*` and `web/middleware.ts` for routing middleware.

## Configuration Pointers
- App settings: `src/OpenDeepWiki/appsettings.json` and `appsettings.Development.json`.
- LLM config: `AI` section in appsettings; environment variables fallback (`CHAT_API_KEY`, `ENDPOINT`, `MODEL_PROVIDER`).
- Docker envs: see `README.md` for full list of required environment variables.

<!-- gitnexus:start -->
# GitNexus — Code Intelligence

This project is indexed by GitNexus as **OpenDeepWiki** (12232 symbols, 25510 relationships, 300 execution flows). Use the GitNexus MCP tools to understand code, assess impact, and navigate safely.

> If any GitNexus tool warns the index is stale, run `npx gitnexus analyze` in terminal first.

## Always Do

- **MUST run impact analysis before editing any symbol.** Before modifying a function, class, or method, run `gitnexus_impact({target: "symbolName", direction: "upstream"})` and report the blast radius (direct callers, affected processes, risk level) to the user.
- **MUST run `gitnexus_detect_changes()` before committing** to verify your changes only affect expected symbols and execution flows.
- **MUST warn the user** if impact analysis returns HIGH or CRITICAL risk before proceeding with edits.
- When exploring unfamiliar code, use `gitnexus_query({query: "concept"})` to find execution flows instead of grepping. It returns process-grouped results ranked by relevance.
- When you need full context on a specific symbol — callers, callees, which execution flows it participates in — use `gitnexus_context({name: "symbolName"})`.

## Never Do

- NEVER edit a function, class, or method without first running `gitnexus_impact` on it.
- NEVER ignore HIGH or CRITICAL risk warnings from impact analysis.
- NEVER rename symbols with find-and-replace — use `gitnexus_rename` which understands the call graph.
- NEVER commit changes without running `gitnexus_detect_changes()` to check affected scope.

## Resources

| Resource | Use for |
|----------|---------|
| `gitnexus://repo/OpenDeepWiki/context` | Codebase overview, check index freshness |
| `gitnexus://repo/OpenDeepWiki/clusters` | All functional areas |
| `gitnexus://repo/OpenDeepWiki/processes` | All execution flows |
| `gitnexus://repo/OpenDeepWiki/process/{name}` | Step-by-step execution trace |

## CLI

| Task | Read this skill file |
|------|---------------------|
| Understand architecture / "How does X work?" | `.claude/skills/gitnexus/gitnexus-exploring/SKILL.md` |
| Blast radius / "What breaks if I change X?" | `.claude/skills/gitnexus/gitnexus-impact-analysis/SKILL.md` |
| Trace bugs / "Why is X failing?" | `.claude/skills/gitnexus/gitnexus-debugging/SKILL.md` |
| Rename / extract / split / refactor | `.claude/skills/gitnexus/gitnexus-refactoring/SKILL.md` |
| Tools, resources, schema reference | `.claude/skills/gitnexus/gitnexus-guide/SKILL.md` |
| Index, status, clean, wiki CLI commands | `.claude/skills/gitnexus/gitnexus-cli/SKILL.md` |

<!-- gitnexus:end -->
