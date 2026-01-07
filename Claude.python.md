# Python

Language-specific instructions for Python development.

## Environment & Package Management

### UV (Recommended)
UV is a fast Python package installer and resolver written in Rust. Use UV for all environment and package management.

#### Environment Setup
- `uv venv` - Create virtual environment in `.venv/`
- `uv venv <path>` - Create environment at specific path
- `uv venv --python 3.12` - Create with specific Python version
- `source .venv/bin/activate` (Linux/Mac) or `.venv\Scripts\activate` (Windows) - Activate environment

#### Package Management
- `uv add <package>` - Add package to dependencies (edits pyproject.toml)
- `uv add --dev <package>` - Add dev dependency
- `uv remove <package>` - Remove package
- `uv pip install <package>` - Install package (legacy pip-style)
- `uv pip sync requirements.txt` - Install from requirements.txt
- `uv sync` - Install all dependencies from pyproject.toml or requirements.txt
- `uv lock` - Update lock file

#### Running Code
- `uv run python main.py` - Run script with UV environment
- `uv run <command>` - Run any command in UV environment
- `uv run pytest` - Run tests with UV
- `uv python` - Start Python REPL in UV environment

#### Package Information
- `uv pip list` - List installed packages
- `uv pip freeze` - Output installed packages in requirements format
- `uv pip show <package>` - Show package details

### Legacy Environment Detection
If UV is not available, detect existing environments:
- `.venv/` or `venv/` → `source .venv/bin/activate` or `source venv/bin/activate`
- `poetry.lock` → use `poetry install` and `poetry shell`
- `Pipfile.lock` → use `pipenv install` and `pipenv shell`
- Check `pyproject.toml` for project type (uv, poetry, setuptools, etc.)

## Common Commands

### Running Code
- `uv run python main.py` - Run script with UV (recommended)
- `python main.py` / `python3 main.py` - Run directly (if env activated)
- `uv run python -m <module>` - Run module with UV
- `python -m <module>` - Run module directly
- `uv run flask run` / `uv run uvicorn main:app` - Run web servers with UV

### Type Checking & Linting
- `mypy .` - Run type checker
- `mypy <specific_file.py>` - Type check specific file
- `ruff check .` - Fast linter (modern replacement for flake8/pylint)
- `ruff check --fix .` - Auto-fix lint issues
- `pylint <file>` - Traditional linter (if ruff not used)
- `black .` - Format code
- `isort .` - Sort imports
- `ruff check --select I --fix .` - Sort imports with ruff

### Testing
- `uv run pytest` or `pytest` - Run tests (discover mode)
- `uv run pytest <specific_test.py>` - Run specific test file
- `pytest -v` - Verbose output
- `pytest --cov=<module>` - Run with coverage
- `pytest -x` - Stop on first failure
- `uv run python -m pytest` - Alternative pytest invocation
- `python -m unittest` - Use unittest framework

## Python Best Practices

### Type Hints
- Use type hints for all function signatures (PEP 484)
- Import from `typing` module for complex types (List, Dict, Optional, etc.)
- Use `|` union syntax in Python 3.10+ (e.g., `str | int` instead of `Union[str, int]`)
- Use `typing_extensions` for newer types on older Python
- Always return meaningful types, avoid `-> None` when actually returning values

### Import Style
- Group imports: standard library → third-party → local (PEP 8)
- Use absolute imports, not relative (except in complex packages)
- Avoid wildcard imports (`from module import *`)
- Sort imports with isort or ruff

### Code Conventions
- Follow PEP 8 style guide
- Use snake_case for functions and variables
- Use PascalCase for classes
- Use UPPER_SNAKE_CASE for constants
- Use f-strings for formatting, not `.format()` or `%`
- Use context managers (`with` statements) for resource management
- Prefer list comprehensions over `map()`/`filter()`
- Use `pathlib.Path` for file paths, not `os.path`

### Error Handling
- Use specific exception types, not bare `except:`
- Always include informative error messages
- Use `finally` for cleanup code
- Log exceptions before re-raising with context
- Use custom exceptions for domain-specific errors

### Async/Await
- Use `asyncio.run()` to execute async code
- Prefer `async`/`await` over callbacks
- Use `asyncio.gather()` for concurrent tasks
- Be careful with blocking operations in async functions
- Use `aiohttp` / `asyncpg` / etc. for async I/O

## File Conventions

### File Naming
- Modules: `lowercase_with_underscores.py` (e.g., `user_service.py`)
- Tests: `test_<module>.py` (e.g., `test_user_service.py`)
- Packages: lowercase with `__init__.py`

### Project Structure
```
project/
├── src/ or <project_name>/
│   ├── __init__.py
│   ├── main.py
│   └── modules/
├── tests/
│   ├── __init__.py
│   └── test_modules/
├── pyproject.toml or setup.py or requirements.txt
└── README.md
```

## Testing Patterns

### pytest Best Practices
- Use descriptive test names (`test_user_login_returns_token_on_valid_credentials`)
- Follow Arrange-Act-Assert pattern
- Use fixtures for reusable test data
- Parametrize tests with `@pytest.mark.parametrize`
- Mock external dependencies with `unittest.mock`
- Use pytest plugins: `pytest-asyncio`, `pytest-cov`, `pytest-mock`

### Test Structure
```python
def test_<function>_<expected_result>():
    # Arrange
    input_data = ...

    # Act
    result = function_under_test(input_data)

    # Assert
    assert result == expected_output
```

## Framework-Specific Notes

### Django
- `python manage.py runserver` - Start dev server
- `python manage.py makemigrations` - Create migrations
- `python manage.py migrate` - Apply migrations
- `python manage.py test` - Run tests
- `python manage.py createsuperuser` - Create admin user
- Check `settings.py` for configuration

### Flask
- `flask run` - Start dev server
- Check `app.py` or `wsgi.py` for entry point
- Use blueprints for organizing routes
- Check `.env` or `config.py` for settings

### FastAPI
- `uvicorn main:app --reload` - Start dev server with hot reload
- `uvicorn main:app` - Production server
- Automatic OpenAPI docs at `/docs`
- Use pydantic models for request/response validation

### Data Science (pandas, numpy, etc.)
- `uv run jupyter notebook` or `uv run jupyter lab` - Launch notebooks
- Convert notebooks to scripts with `jupyter nbconvert`
- Use UV for dependency isolation
- Use `uv pip freeze` for reproducibility

## Build Verification

Before completing work, run in order:
1. Type check: `uv run mypy .` or `mypy .`
2. Lint: `uv run ruff check .` or `ruff check .`
3. Format check: `uv run ruff format --check .` or `black --check .`
4. Tests: `uv run pytest` or `pytest`
5. Fix any issues before committing

### UV Quick Fix
- `uv run ruff check --fix .` - Auto-fix lint issues
- `uv run ruff format .` - Auto-format code

## Security

- Never use `input()` for production code (SQL/command injection risk)
- Validate and sanitize all user input
- Use parameterized queries for database access (not string formatting)
- Keep dependencies updated (`pip list --outdated`)
- Use `bandit` for security linter
- Never commit secrets (use `.env` files, add to `.gitignore`)

## When to Ask for Clarification

- Which web framework to use (Django, Flask, FastAPI, etc.)
- Python version to use (check .python-version or pyproject.toml)
- Testing framework choice (pytest vs unittest)
- Async vs sync approach for I/O operations
- Whether to use UV or legacy pip/poetry for existing projects
