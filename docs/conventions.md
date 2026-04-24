# Conventions

Short, scannable pattern library for future LLM sessions. Rule bodies moved to `.claude/rules/*.md` during handoff-system-v2 Phase 5; this file retains the numbered skeleton as a stable cross-reference surface.

## Quick Reference

| ID | Title | Applies when | Rule body |
| --- | --- | --- | --- |
| DOC-001 | LLM-first docs | editing files under `docs/` | `.claude/rules/global.md` |
| DOC-002 | Session start | starting work in this repo | `.claude/rules/global.md` |
| DOC-003 | Convention changes | adding or revising a repo convention | `.claude/rules/global.md` |
| CI-001 | Track-latest lint tooling via setup-uv | configuring `black`/`ruff`/`isort`/`mypy` in CI | `.claude/rules/ci.md` |

## DOC-001. LLM-first docs

Moved to `.claude/rules/global.md` on 2026-04-24. See that file for the full rule.

## DOC-002. Session start

Moved to `.claude/rules/global.md` on 2026-04-24 (rule content updated to reflect the new hook-injected state flow — no more manual "read handoff.md first"). See `.claude/rules/global.md` for the current rule.

## DOC-003. Convention changes

Moved to `.claude/rules/global.md` on 2026-04-24. See that file for the full rule.

## CI-001. Track-latest lint tooling via setup-uv

Body lives in `.claude/rules/ci.md` (path-scoped to `.github/workflows/*.yml`). Added 2026-04-24 after a Black 26.3.1 release reformatted `src/models/example_model.py` and `src/services/example_service.py` and turned CI red.
