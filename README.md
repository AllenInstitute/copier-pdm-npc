# Copier PDM + MindScope NP

Copier template for MindScope Neuropixels projects to get up and running quickly with automated formatting, testing, publishing and docs.

## Quick Start

First install [Copier](https://copier.readthedocs.io/en/stable/) and [PDM](https://copier-pdm.fming.dev/) via [pipx](https://github.com/pypa/pipx) (for isolated CLI tools).
```bash
python3 -m pip install --user pipx

pipx install copier pdm
```

With PDM:
```bash
pdm init --copier gh:bjhardcastle/copier-pdm-npc --UNSAFE
```

See this [documentation](https://copier-pdm.fming.dev) for more details.

After connecting to a github repo, create the secrets used in `publish.yml` in `Actions`

## Features

### Package manager

The template project uses [PDM](https://pdm.fming.dev) setup, with pre-defined `pyproject.toml` configuration for tools
- add dependencies: `pdm add numpy`
  - add dev dependencies: `pdm add -G dev numpy`
- remove dependencies correctly: `pdm remove numpy`
- always commit `pdm.lock` for a reproducible dev environment

### VSCode config

- `.vscode/settings.json` will be generated with the project, to enable mypy static analysis (instead of Pylance).
- `.vscode/extensions.json` will make suggestions for extenstions that aren't already instealled

### Github actions

Triggered on pushes to the main branch:

#### Documentation and changelog

- Documentation is built with [MkDocs](https://github.com/mkdocs/mkdocs)
  ([Material theme](https://github.com/squidfunk/mkdocs-material))
- A basic changelog is auto-generated from commit messages

#### Formatting and linting

- black
- [ruff](https://github.com/charliermarsh/ruff)

#### Tests

- Tests run with [pytest](https://pytest.org/)
- mypy is run (without strict mode, so untyped functions will not be analyzed)

#### Publishing
Provided all tests pass, the package is published to [pypi](https://pypi.org)