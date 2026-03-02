# TextTools — Style and Conventions

- Type hints required on all functions (mypy strict)
- Google-style docstrings on all public APIs
- Files: snake_case.py, classes: PascalCase, private: _leading_underscore
- Signals for cross-layer communication — never call View methods from ViewModel
- Long operations must use QThread; never block UI thread
- Black (88 chars) + isort (black profile)
- Qt tests: always consult qt:qtest-patterns skill first
