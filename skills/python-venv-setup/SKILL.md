---
name: python-venv-setup
description: Set up a Python virtual environment using pyenv with the latest Python version. Use when the user asks to create a Python environment, set up pyenv, initialize a Python project, or configure Python virtual environments.
---

# Python Virtual Environment Setup

Automatically set up a Python virtual environment using pyenv with the latest available Python version.

## Core Philosophy

1. **Always use latest stable Python** — Get the most recent Python version available
2. **Isolated environments** — Each project gets its own virtual environment
3. **Consistent tooling** — Use pyenv for version management
4. **Minimal friction** — Automate the entire setup process

## Workflow

1. Check if pyenv is installed, if not install it via Homebrew
2. Upgrade pyenv to ensure access to latest Python versions
3. Get the latest stable Python version available
4. Install that Python version (if not already installed)
5. Prompt user for environment name (suggest current directory name as default)
6. Create virtual environment with that Python version
7. Set it as the local environment for the current directory
8. Confirm successful setup

## Implementation Steps

### 1. Check and Install pyenv

First, check if pyenv is installed:

```bash
which pyenv
```

If not installed, install via Homebrew:

```bash
brew install pyenv
```

### 2. Upgrade pyenv

Always upgrade to get latest Python version options:

```bash
brew upgrade pyenv
```

### 3. Get Latest Python Version

List available Python versions and get the latest stable release (not dev/rc versions):

```bash
pyenv install --list | grep -E '^\s*[0-9]+\.[0-9]+\.[0-9]+$' | tail -1
```

Store this version for use in subsequent commands.

### 4. Install Python Version

Install the latest Python version (skip if already installed):

```bash
pyenv install <latest_version>
```

Note: pyenv will notify if the version is already installed.

### 5. Get Environment Name

Ask the user what to name the virtual environment. Suggest the current directory name as a default option.

```bash
basename $(pwd)
```

### 6. Create Virtual Environment

Create the virtual environment:

```bash
pyenv virtualenv <latest_version> <env_name>
```

### 7. Set Local Environment

Set it as the local environment for the current directory:

```bash
pyenv local <env_name>
```

This creates a `.python-version` file in the current directory.

### 8. Verify Setup

Confirm the setup by checking the Python version:

```bash
python --version
which python
```

## Output Format

Provide clear progress updates:

```
Setting up Python virtual environment...

✓ pyenv is installed
✓ Upgraded pyenv to latest version
✓ Latest Python version: <version>
✓ Installing Python <version>...
✓ Created virtual environment: <env_name>
✓ Set as local environment for this directory

Setup complete! Your Python environment is ready.
Python version: <version>
Environment: <env_name>
```

## Error Handling

If any step fails:
- Check if Homebrew is installed (required for pyenv)
- Verify internet connection for downloading Python versions
- Check for permission issues
- Suggest manual intervention if automation fails

## Additional Notes

- The `.python-version` file will be created in the current directory
- This file tells pyenv which environment to activate when in this directory
- The virtual environment is stored in pyenv's environments directory, not the project directory
- To activate the environment in future sessions, just navigate to the project directory

## Common Issues

1. **Homebrew not installed**: Direct user to https://brew.sh
2. **Python version already installed**: This is fine, skip to next step
3. **Environment name conflicts**: Suggest adding a suffix or different name
4. **Slow Python installation**: Large downloads are normal, be patient
