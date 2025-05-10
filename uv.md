# Using UV with pygeoapi

UV is a fast Python package installer and resolver written in Rust. This document explains how to use our new UV-based setup for pygeoapi development.

## Prerequisites

Install UV before getting started:

### macOS / Linux

```bash
curl -sSf https://install.ultraviolet.dev | sh
```

### Windows - PowerShell

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## Getting Started with the UV-based pygeoapi

### 1. Check out the feature branch

We've set up the UV configuration on the `feat-uv` branch. Make sure to check it out:

```bash
git clone https://github.com/geobeyond/pygeoapi.git
cd pygeoapi
git checkout feat-uv
```

### 2. Install dependencies

The project is already configured with `pyproject.toml`. Simply run:

```bash
uv sync
```

This automatically:
- Creates a virtual environment in `.venv`
- Installs all required dependencies
- Sets up pygeoapi in development mode

### 3. Activate the Virtual Environment

After running `uv sync`, you'll need to activate the virtual environment to use pygeoapi:

**macOS / Linux:**
```bash
source .venv/bin/activate
```

**Windows (Command Prompt):**
```cmd
.venv\Scripts\activate.bat
```

**Windows (PowerShell):**
```powershell
.venv\Scripts\Activate.ps1
```

You'll know the environment is activated when you see `(.venv)` at the beginning of your command prompt.

## Working with Optional Dependencies

We've configured the project with optional dependency groups. If you need features from these groups, you can install them as needed:

```bash
# Install with a single feature group
uv pip install -e ".[admin]"

# Install with multiple feature groups
uv pip install -e ".[admin,dev]"

# Install everything
uv pip install -e ".[all]"
```

Available feature groups:

- `admin`: Administration tools (gunicorn, jsonpatch, filelock)
- `django`: Django integration support
- `docker`: Docker deployment dependencies
- `provider`: Data provider dependencies (GDAL, elasticsearch, etc.)
- `manager`: Database management tools
- `starlette`: Starlette web framework support
- `dev`: Development and testing tools (pytest, flake8, etc.)
- `all`: All optional dependencies together

## Daily Development Workflow

### Update dependencies

To update all dependencies to their latest compatible versions:

```bash
uv sync --upgrade
```

### Running pygeoapi

After installation and activation of the virtual environment, you can run the server:

```bash
pygeoapi --help
```

Or without activation of the virtual environment:

```bash
uv run pygeoapi --help
```

### Common UV Commands

```bash
# View installed packages
uv pip list

# Install a new package
uv pip install package-name

# Install a specific version
uv pip install package-name==1.2.3

# Uninstall a package
uv pip uninstall package-name

# Generate requirements.txt
uv pip freeze > requirements.txt
```

## Additional Resources

- [UV Documentation](https://github.com/astral-sh/uv)
- [pygeoapi Documentation](https://docs.pygeoapi.io/)
