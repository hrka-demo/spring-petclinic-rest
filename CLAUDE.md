# CLAUDE.md: spring-petclinic-rest (HRKA demo client project)

Read this before any change. Agents and humans follow the same rules.

## Project

Spring Boot REST API for a veterinary clinic (owners, pets, vets, visits). Java 21, Maven 3.9+, OpenAPI-generated API (`src/main/resources/openapi.yml`), JPA repositories under `repository/jpa`, global error handling in `rest/advice/ExceptionControllerAdvice.java`.

- Build: `mvn -q -B -DskipTests package`
- Test: `mvn -q -B test` (full suite must stay green; 239 tests on master as of PR #1)
- Run locally: container `petclinic` on `127.0.0.1:9966`, base path `/petclinic/api`

## HRKA delivery rules (non-negotiable)

1. **Agents build, humans decide.** Every change reaches `master` through a draft PR that a human approves and merges. Never push to `master`, never force-push, never merge.
2. **TDD.** Write or extend a failing test first, then the fix. Never modify or delete an existing test to make a change pass (PDF risk R2).
3. **Branches:** `fix/<JIRA-KEY>`, `feat/<JIRA-KEY>`, `brd/<slug>`, `arch/<slug>`. Base is always `master`.
4. **Commits and PRs:** conventional commits (`fix(PET-8): ...`). No AI attribution lines, no "Generated with" footers.
5. **Traceability.** Every requirement has an ID in `brd/<slug>/index.json`. Stories, ADRs, tests and PRs cite the IDs they implement (gate G6: every acceptance criterion appears in a test name or tag).
6. **Client errors are 4xx and log WARN.** Only unexpected failures log ERROR (the sentinel pages on ERROR).
7. **SonarQube:** no new blocker or critical issues; do not lower coverage on changed code.

## Knowledge layout

| Path | Owner agent | Contents |
|---|---|---|
| `brd/<slug>/` | A1 Requirements | `source/` (client BRD as received), `brd.md`, `index.json`, `open-questions.md` |
| `architecture/<slug>/` | A2 Solution Architect, A3 HLD/LLD | solution architecture, ADRs, C4 diagrams, HLD, LLD, OpenAPI deltas |
| `progress/<KEY>.md` | any build agent | per-ticket ledger: plan, decisions, test evidence, PR link |

Agent definitions live in `.claude/agents/`. Confluence space **HRKA** holds the published copies (RTM, architecture, open questions).

## Human gates (PDF section 14)

BRD sign-off (PO) before A2 starts · architecture review before backlog · PO approval before any Jira create/update by A4 · PR approval on every PR.
