# Contributing to DBWarden

DBWarden is a model‑first migration system with a strong correctness guarantee, and we're glad you want to
be part of it.

This document will help you get set up and explain the standards we follow.
Every contribution makes the project better for everyone.

---

## Project philosophy (the short version)

DBWarden’s core thesis is:

> *SQLAlchemy models are the canonical schema. DBWarden converges the database to them, and it proves that convergence.*

We care deeply about **correctness** (the convergence gate must never regress), **honesty** (we don’t auto‑apply unreviewed changes), and **developer experience** (the CLI should feel polished and the docs should answer the question before you finish asking it).

If your contribution fits that mindset, it’s in the right place.

---

## Code of Conduct

We follow the [Contributor Covenant](https://www.contributor-covenant.org/).
Please be kind, constructive, and patient.

---

## What you can contribute

- **Bug reports**: open an issue with a clear reproduction.
- **Feature requests**: open an issue describing the *problem* it solves, not
  just the solution.
- **Documentation**: fixes, improvements, new cookbook recipes.
- **Code**: CLI improvements, backend handlers, safety analysis, etc.
- **Plugin reviews**: help us review community plugins for the Approved tier.
- **Plugin development**: build a plugin and submit it for approval.

---

## Development setup

You need **Python 3.12+** and **uv**.

```bash
git clone https://github.com/dbwarden-org/dbwarden.git
cd dbwarden
uv sync --extra dev
```

This installs DBWarden in editable mode with all development dependencies (pytest, linters, docs tools).

### Running tests

```bash
uv run pytest
```

The full suite includes **1,450+ tests** across unit, integration, and convergence gate checks. Integration tests for PostgreSQL and ClickHouse require Docker. They are marked with `@pytest.mark.integration` and are skipped by default when Docker is not available.

To run everything:

```bash
uv run pytest -m "not integration"   # unit tests only
uv run pytest -m "integration"       # integration tests (requires Docker)
```

### Running the convergence gate locally

```bash
uv run pytest -m p0
```

The **P0 convergence gate** must **never** fail. This is the contract: our migration history always reproduces the models exactly. Any change that breaks the gate cannot be merged.

---

## Code standards

### Import boundaries

- **Core** must not import from any `dbwarden_plugin_*` package.
- **Plugins** must not import from `dbwarden.engine.*`, `dbwarden.databases.*`, or any internal module. The plugin contract is `dbwarden.plugin` and the public API surface.
- The import boundary is enforced by `scripts/check-import-boundary.py` and runs in CI.

### Type hints and docstrings

- All public functions and methods must have type annotations.
- Use `from __future__ import annotations` in every module.
- Docstrings follow PEP 257. At minimum, a one‑line summary for simple functions; a full description with parameters and return types for complex ones.

### No import‑time side effects

- Core: importing `dbwarden` must not scan the filesystem, connect to a database, or execute plugin code. Everything happens lazily or on demand.
- Plugins: the `setup(registry)` function is the **only** place hooks are registered. Importing the plugin package or its `plugin.py` must have no side effects.

### Linting and type checking

```bash
uv run ruff check
uv run mypy
```

These run in CI and must pass.

---

## Pull request process

1. **Branch naming**: `feature/short-description` or `fix/short-description`.
2. **Write tests**: every new feature or bugfix must include tests. If you're changing a handler, include a round‑trip test.
3. **Run the full suite locally** (unit + integration if applicable).
4. **Open a PR** against `main`. The PR template will prompt you for:
   - What the change does.
   - How to verify it.
   - Any breaking changes.
5. **CI checks**: linting, type checking, import boundary, unit tests, and convergence gate must all pass before review.
6. **Review**: a maintainer will review. Be prepared to discuss trade‑offs, especially around correctness and API surface.

---

## Documentation

Documentation lives in `docs/` and is built with **Zensical**.

```bash
cd docs
zensical build    # or mkdocs build
```

- New features need documentation in the appropriate section.
- Cookbook recipes are especially welcome.
- If you add a new CLI command, include it in the CLI reference.

---

## Developing plugins

DBWarden has a **plugin system** that allows framework integrations (value plugins) and new database object types (object plugins) to live outside core.

- Start from the **[plugin template](https://github.com/dbwarden-org/dbwarden-plugin-template)**.
- Read the **[plugin developer guide](https://dbwarden.emiliano-go.com/plugins/developing/)**.
- To get your plugin listed as **Approved**, it must pass the [Approved test standard](https://dbwarden.emiliano-go.com/plugins/approved-standard/) and be reviewed.
- Official plugin status requires the plugin to live under the `dbwarden-org` GitHub organisation and be published with PEP 740 provenance.

---

## License

DBWarden is licensed under the **MIT License**. By contributing, you agree that your contributions will be licensed under the same terms.

---

## Recognition

Contributors are acknowledged in the project README and release notes. Every merged PR, including documentation, gets credit. If you contribute significantly, we’ll add you to the maintainers list.

---

## Questions?

Open a discussion in **[GitHub Discussions](https://github.com/dbwarden-org/dbwarden/discussions)** or ask in the issue tracker. We’re happy to help you get started.

Thank you for helping make DBWarden better!
```
