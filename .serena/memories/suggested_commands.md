# TextTools — Development Commands

```bash
python -m src.main             # Run the application
pytest tests/                  # Run all tests (coverage auto-enabled)
pytest tests/unit/test_X.py    # Single test file
mypy src/                      # Type checking (strict)
black src/ tests/              # Format
isort src/ tests/              # Sort imports
uv pip install -r requirements.txt  # Install deps
```

## Git
- Work on `testing` branch only
- Never commit to `main`
