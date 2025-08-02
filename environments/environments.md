# Virtual environments

## uv

`brew install astral-sh/astral/uv`

`uv venv`

`source .venv/bin/activate`

If we have a pyproject.toml file then:

```
[project]
name = "my-app"
version = "0.1.0"
description = "My app description"
dependencies = [
  "fastapi",
  "uvicorn"
]

[build-system]
requires = ["uv"]
build-backend = "uv.build"
```
You can omit build-system if you don’t need to build packages.

Install dependencies from pyproject.toml

`uv pip install -r <(uv pip compile)`

Add dependency directly:

`uv pip add httpx`

This updates both pyproject.toml and your environment.

Lock dependencies:

`uv pip compile --output requirements.txt`

This creates a requirements.txt from the pyproject.toml, similar to pip-tools.

Makefile for uv:

```
VENV_DIR := .venv
PYTHON := $(VENV_DIR)/bin/python

.PHONY: venv install lock run clean

# Create virtual environment if it doesn't exist
venv:
	@test -d $(VENV_DIR) || uv venv

# Install from pyproject.toml (using lockfile if exists)
install: venv
	@if [ -f requirements.lock ]; then \
		echo "🔒 Installing from requirements.lock"; \
		source $(VENV_DIR)/bin/activate && uv pip install -r requirements.lock; \
	else \
		echo "📦 Installing from pyproject.toml"; \
		source $(VENV_DIR)/bin/activate && uv pip install -r <(uv pip compile); \
	fi

# Lock dependencies from pyproject.toml
lock:
	@echo "🔐 Locking dependencies..."
	uv pip compile --output requirements.lock

# Run your app (edit entry point as needed)
run:
	source $(VENV_DIR)/bin/activate && uvicorn main:app --reload

# Clean virtual environment and lockfile
clean:
	rm -rf $(VENV_DIR) requirements.lock
```

Usage:

```
make venv      # Create virtual env
make install   # Install deps (from lock if available)
make lock      # Create/refresh lockfile
make run       # Run your FastAPI app (edit entry point)
make clean     # Remove env and lock
```

## virtualenv

`python3 -m venv myvenv`

Then

`source myenv/bin/activate`

## poetry




