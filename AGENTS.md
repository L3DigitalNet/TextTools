# Codex Instructions for TextTools

**Session state:** detect layout first. V2: read `docs/state.md`, then this file, then conventions; V1: read `docs/handoff.md`, then this file, then conventions.

**Full conventions reference:** [`docs/conventions.md`](docs/conventions.md) - LLM-targeted pattern library. Every convention follows the six-field schema (Applies-when / Rule / Code / Why / Sources / Related) with a Quick Reference table at the top for O(1) lookup. Do not introduce new patterns without checking conventions first.

**Detailed review workflows:** [AGENTS.reviews.md](AGENTS.reviews.md) - read this only for review-related tasks (review planning, review sweeps, code/security/test/etc. reviews). The verbose per-review routing, defaults, and orchestrator notes live there.

## Repo Purpose

PySide6 desktop app for text processing on Linux. Uses MVVM with Qt Designer `.ui` files.

## Branch Rules

- Run `.agents/branch_protection.py` before file modifications.
- Work on `testing`, not `main`.

## Commands

```bash
pytest tests/
mypy src/
black src/ tests/
isort src/ tests/
```

## Key Rules

- MVVM separation is strict: models and services stay Qt-free, views stay thin, viewmodels never reach directly into widgets.
- UI structure comes from Qt Designer `.ui` files; object names are part of the contract with the view layer.
- Each viewmodel defines its `ServiceProtocol` in the same file as the viewmodel.
- Use signals for cross-layer communication. Long-running work must not block the UI thread.
