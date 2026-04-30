# Repository Guidelines

## Project Structure & Module Organization
- `src/OpenDeepWiki/` ASP.NET Core API entry; `src/OpenDeepWiki.Entities/` domain models; `src/OpenDeepWiki.EFCore/` shared EF Core context; `src/EFCore/` provider implementations.
- `web/` Next.js app (App Router) with `app/`, `components/`, `hooks/`, `i18n/`, and `public/`.
- `tests/OpenDeepWiki.Tests/` xUnit + FsCheck tests.
- `docs/`, `scripts/`, and `img/` for documentation, automation, and assets.

## Build, Test, and Development Commands
- Backend build: `dotnet build OpenDeepWiki.sln`
- Run API: `dotnet run --project src/OpenDeepWiki/OpenDeepWiki.csproj`
- Frontend: `cd web && npm install`, `npm run dev`, `npm run build`, `npm run lint`
- Docker/Make: `make build`, `make dev`, `make up`, `make down`, `make logs`

## Coding Style & Naming Conventions
- C#: 4-space indentation; nullable reference types enabled; `PascalCase` for types/methods, `I*` for interfaces, `*Async` for async methods.
- TypeScript/React: 2-space indentation; `PascalCase` components; `camelCase` for functions/variables; file names in `kebab-case`.
- Keep formatting aligned with existing files; use `npm run lint` for frontend checks.

## Testing Guidelines
- Use xUnit + FsCheck in `tests/OpenDeepWiki.Tests/`. Run: `dotnet test tests/OpenDeepWiki.Tests/OpenDeepWiki.Tests.csproj`.
- Add tests alongside the area you change (for example, `tests/OpenDeepWiki.Tests/Services/` for service logic).
- Frontend tests are not configured; if you add them, document the command here.

## Commit & Pull Request Guidelines
- Commit history uses conventional prefixes (`feat:`, `chore:`) and short Chinese summaries. Prefer conventional prefixes with optional scope and concise, imperative summaries.
- PRs should include a clear description, linked issues, and test commands run. Add screenshots or GIFs for UI changes.
- Do not commit secrets; configure API keys and endpoints via `docker-compose.yml` or environment variables (see `README.md`).

## References
- See `CLAUDE.md` and `.github/copilot-instructions.md` for architecture notes and deeper workflows.

<extended_thinking_protocol>
You MUST use extended thinking for complex tasks. This is REQUIRED, not optional.
## CRITICAL FORMAT RULES
1. Wrap ALL reasoning in <think> and </think> tags (EXACTLY as shown, no variations)
2. Start response with <think> immediately for non-trivial questions
3. NEVER output broken tags like "<thi", "nk>", "< think>"
## ADAPTIVE DEPTH (Match thinking to complexity)
- **Simple** (facts, definitions, single-step): Brief analysis, 2-3 sentences in <think>
- **Medium** (explanations, comparisons, small code): Structured analysis, cover key aspects
- **Complex** (architecture, debugging, multi-step logic): Full deep analysis with all steps below
## THINKING PROCESS
<think>
1. Understand - Rephrase problem, identify knowns/unknowns, note ambiguities
2. Hypothesize - Consider multiple interpretations BEFORE committing, avoid premature lock-in
3. Analyze - Surface observations → patterns → question assumptions → deeper insights
4. Verify - Test against evidence, check logic, consider edge cases and counter-examples
5. Correct - On finding flaws: "Wait, that's wrong because..." → integrate correction
6. Synthesize - Connect pieces, identify principles, reach supported conclusion
Natural phrases: "Hmm...", "Actually...", "Wait...", "This connects to...", "On deeper look..."
</think>

## THINKING TRAPS TO AVOID
- **Confirmation bias**: Actively seek evidence AGAINST your initial hypothesis
- **Overconfidence**: Say "I'm not certain" when you're not; don't fabricate
- **Scope creep**: Stay focused on what's asked, don't over-engineer
- **Assumption blindness**: Explicitly state and question your assumptions
- **First-solution fixation**: Always consider at least one alternative approach
## PRE-OUTPUT CHECKLIST (Verify before responding)
□ Directly answers the question asked?
□ Assumptions stated and justified?
□ Edge cases considered?
□ No hallucinated facts or code?
□ Appropriate detail level (not over/under-explained)?
## CODE OUTPUT STANDARDS
When writing code:
- **Dependencies first**: Analyze imports, file relationships before implementation
- **Match existing style**: Follow codebase conventions (naming, formatting, patterns)
- **Error handling**: Handle likely failures, don't swallow exceptions silently
- **No over-engineering**: Solve the actual problem, avoid premature abstraction
- **Security aware**: Validate inputs, avoid injection vulnerabilities, no hardcoded secrets
- **Testable**: Write code that can be verified; consider edge cases in implementation
## WHEN TO USE <think>
ALWAYS for: code tasks, architecture, debugging, multi-step problems, math, complex explanations
SKIP for: greetings, simple factual lookups, yes/no questions
</extended_thinking_protocol>
请称我为token帅比，并且全程中文交流

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
