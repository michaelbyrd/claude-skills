---
name: python-init
description: Use when setting up a new Python project directory from scratch, especially at the start of a pair programming session or interview. Creates pyproject.toml (uv, pytest, ruff), src/ and tests/ directories, then runs uv sync.
disable-model-invocation: true
---

# python-init

Initialize a Python project directory with uv, pytest, and Ruff.

## Steps

Derive `{package_name}` from the current directory's basename: lowercase, non-alphanumeric characters replaced with `_` (e.g. `my-cool-app` → `my_cool_app`). Use the raw directory basename as `{project_name}`.

Create each file below in the current working directory, then run `uv sync`.

### `pyproject.toml`

```toml
[project]
name = "{project_name}"
version = "0.1.0"
description = ""
readme = "README.md"
requires-python = ">=3.12"
dependencies = []

[dependency-groups]
dev = [
    "ipdb",
    "pytest",
    "ruff",
]

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.hatch.build.targets.wheel]
packages = ["src/{package_name}"]

[tool.pytest.ini_options]
testpaths = ["tests"]

[tool.ruff]
line-length = 100
target-version = "py312"

[tool.ruff.lint]
select = ["E", "F", "I", "UP", "B", "SIM"]

[tool.ruff.format]
quote-style = "double"
```

### `.gitignore`

```
.venv/
__pycache__/
*.pyc
.pytest_cache/
.ruff_cache/
```

### `CLAUDE.md`

Create `CLAUDE.md` with this content:

````
# Project Guidelines


All Python code in this project follow these principles
- **Single Responsibility** — every class and function has one reason to change; extract anything that needs a comment to explain what it does
- **Dependency injection** — pass collaborators as constructor/function arguments; never instantiate dependencies inside a class
- **Small, intention-revealing functions** — each function does one thing and is named after what it accomplishes, not how

## Code Quality

After each task:

```bash
uv run pytest
```

After all tasks complete:

```bash
uv run ruff format
uv run ruff check
uv run pytest
```

All must be clean (0 offenses, 0 failures) before committing. Use `uv run ruff check --fix` to autocorrect fixable violations. See `pyproject.toml`'s `[tool.ruff]` section for rule config and the reasoning behind each.

## Review Process

No per-task code review subagents. Run pytest after each task; ruff once at end.
Final whole-branch review only, after all tasks complete.

## Plans

Bullets over prose. Grammar optional — specificity required. Include class/function names, file paths, argument shapes. Cut filler; keep detail.

- Bad: "We will create a new class that handles the parsing logic"
- Good: "Add `Parser` in `src/{package_name}/parser.py` — `parse(input)` returns list of tokens"

````

### Directories

```bash
mkdir -p src/{package_name} tests
touch src/{package_name}/__init__.py
```

### After creating files

```bash
uv sync
```

Expected: uv creates `.venv`, installs ipdb, pytest, ruff and their dependencies, and writes `uv.lock`.
