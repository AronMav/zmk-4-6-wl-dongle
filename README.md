# ZMK Config for Charybdis 4x6 Wireless with Dongle

This repository contains ZMK firmware configuration for the Charybdis 4x6 split keyboard with wireless support and dongle.

## Features

- ✅ ZMK Studio support with proper physical layout
- ✅ Automatic keymap visualization with keymap-drawer
- ✅ Pre-commit hooks for code quality
- ✅ GitHub Actions CI/CD pipeline

## Development Setup

### Pre-commit Hooks

This repository uses pre-commit hooks to ensure code quality and consistency.

**Installation:**

```bash
# Install pre-commit
pip install pre-commit

# Install hooks
pre-commit install
pre-commit install --hook-type commit-msg
```

**What it checks:**

- ✅ C/C++ code formatting (clang-format)
- ✅ YAML/JSON/Markdown formatting (prettier)
- ✅ Commit message linting (conventional commits)
- ✅ Trailing whitespace removal
- ✅ YAML validation
- ✅ Large files check

**Commit Message Format:**

Use conventional commit format:

```
<type>: <description>

[optional body]

[optional footer]
```

**Types:** `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`

**Example:**

```bash
git commit -m "feat: add mouse scroll layer"
git commit -m "fix: correct thumb cluster rotation in physical layout"
```

## Building Firmware

The firmware is automatically built by GitHub Actions on every push. Download the latest build from the Actions tab.

## Keymap Visualization

Keymap diagrams are automatically generated and committed to the `keymap-drawer/` folder on every push.
