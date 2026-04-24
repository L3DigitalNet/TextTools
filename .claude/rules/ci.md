---
globs: [".github/workflows/*.yml", ".github/workflows/*.yaml"]
---

# CI rules — loaded when editing GitHub Actions workflows

## CI-001. Track-latest lint tooling via setup-uv

**Applies when:** configuring `black`, `ruff`, `isort`, `mypy`, or other formatters/linters in a CI workflow.
**Rule:** install lint tools through `astral-sh/setup-uv` (SHA-pinned) + `uv tool install --upgrade <tool>`. Do not pin the tool versions in `pyproject.toml`/`requirements*.txt`. Add a daily `schedule` trigger so upstream releases are absorbed by an automated CI run instead of festering until the next push.

```yaml
on:
  push: { branches: [main] }
  schedule:
    - cron: '0 6 * * *'   # daily 06:00 UTC
  workflow_dispatch:

jobs:
  lint:
    steps:
      - uses: astral-sh/setup-uv@<full-sha>  # SHA-pinned to a verified tag
        with:
          python-version: "3.13"
      - name: Install latest linting tools
        env:
          UV_CACHE_DIR: ${{ github.event_name == 'schedule' && runner.temp || '/home/runner/.cache/uv' }}
        run: |
          uv tool install --upgrade black
          uv tool install --upgrade isort
      - run: uv tool run black --check src/ tests/
```

**Why:** Pinned lint tools rot — every upstream release surfaces as a CI failure on a totally unrelated commit, and the fix is always "bump the pin + reformat." Track-latest amortizes the reformat into a scheduled CI run that fails on a known-empty diff, so the next dev push lands clean. The cache-bypass on `schedule` (via `UV_CACHE_DIR=runner.temp`) forces a fresh PyPI resolve so the daily cron actually picks up new versions instead of replaying the cached install. Rejected: pinning to `==X.Y.Z` (creates the rot we're avoiding) and unpinned `actions/setup-*` SHAs (supply-chain risk; pin the action SHA, let the tool float).

**Sources:** `astral-sh/setup-uv` README; `uv tool install` docs.
**Related:** none yet.
