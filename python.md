Here's the best practice for setting up a Python project with uv on a fresh Ubuntu instance:

## 1. Install uv

First, install uv using the official installer:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Then restart your shell or run:
```bash
source $HOME/.cargo/env
```

## 2. Create a new Python project

For a new project, use uv's project scaffolding:

```bash
uv init my-project
cd my-project
```

This creates a proper Python project structure with:
- `pyproject.toml` for project configuration
- `src/` directory with your package
- `README.md` and other standard files

## 3. Specify Python version

If you need a specific Python version, uv can install and manage it:

```bash
# Install a specific Python version
uv python install 3.11

# Use it in your project
uv python pin 3.11
```

## 4. Add dependencies

Add dependencies using uv instead of pip:

```bash
# Add runtime dependencies
uv add requests pandas

# Add development dependencies
uv add --dev pytest black ruff mypy
```

## 5. Working with the environment

uv automatically creates and manages a virtual environment. To run commands:

```bash
# Run Python scripts
uv run python script.py

# Run installed tools
uv run pytest
uv run black .

# Start a shell in the environment
uv shell
```

## 6. For existing projects

If you have an existing project with requirements.txt:

```bash
# Convert requirements.txt to pyproject.toml
uv init --package
uv add -r requirements.txt
```

## Key advantages of this approach:

- **Fast**: uv is significantly faster than pip
- **Reliable**: Handles dependency resolution better
- **Modern**: Uses pyproject.toml standard
- **Integrated**: Manages Python versions, virtual environments, and dependencies
- **Lock files**: Automatically creates `uv.lock` for reproducible builds

## Additional tips:

- Use `uv sync` to install dependencies from lock file
- Use `uv tree` to visualize dependency tree
- Use `uv pip` commands if you need pip-compatible interface
- Configure tools like ruff, black, mypy in pyproject.toml

This setup gives you a modern, fast, and reliable Python development environment that follows current best practices.
