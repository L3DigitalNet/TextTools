# TextTools — Project Overview

## Purpose
PySide6 desktop app for text processing on Linux: encoding conversion (UTF-8), text formatting/cleaning, find/replace, file management. MVVM framework and UI shell are in place; feature logic is mostly unimplemented scaffolding. `DESIGN.md` is the authoritative spec.

## Tech Stack
- Python 3.14, PySide6 6.8.0+, MVVM architecture, Qt Designer for UI
- Testing: pytest + pytest-qt (coverage auto-enabled via pyproject.toml addopts)
- Type checking: mypy (strict mode)
- Formatting: Black (88 chars) + isort (black profile)

## Architecture — MVVM (strictly enforced)
```
View (src/views/)         → Loads .ui files, connects signals, updates UI
    ↕ Qt Signals/Slots
ViewModel (src/viewmodels/) → QObject, emits signals, calls services
    ↕ Method calls
Service (src/services/)    → External I/O (files, APIs), injected into ViewModels
    ↕ Method calls
Model (src/models/)        → Pure dataclasses, business logic, validation
```

## Layer Rules
- Model: pure Python, no Qt imports
- ViewModel: QObject + Signal/Slot, no widget manipulation
- View: loads .ui files, findChild(), signal connections; no business logic
- Service: file I/O, external APIs; no Qt imports

## Key Patterns
- `create_application()` in `src/main.py` is sole composition root (dependency injection)
- ServiceProtocol pattern: each ViewModel defines its Protocol in the same file
- UI defined in Qt Designer .ui files under `src/views/ui/`
- Widget objectNames defined in DESIGN.md Appendix A — must match exactly
