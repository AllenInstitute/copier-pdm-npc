# Copier PDM

Copier template for PDM projects.

This copier template is mainly for my own usage, but feel free to try it out, or fork it!

You need to install [Copier](https://copier.readthedocs.io/en/stable/) first.

## Quick Start

With PDM:
```bash
pdm init --copier gh:bjhardcastle/copier-pdm-npc --UNSAFE
```

With copier:

```bash
copier "gh:bjhardcastle/copier-pdm-npc" <project_name>
```

See the [documentation](https://copier-pdm.fming.dev) for more details.

## Features

### Package manager

The template project uses [PDM](https://pdm.fming.dev) setup, with pre-defined `pyproject.toml`

### Documentation and changelog

- Documentation is built with [MkDocs](https://github.com/mkdocs/mkdocs)
  ([Material theme](https://github.com/squidfunk/mkdocs-material)
- Changelog is auto-generated from the fragments under `news` directory, with the power of [towncrier](https://pypi.org/project/towncrier/)

### Pre-commit and linter

[pre-commit](https://pre-commit.com/) is used for both commit hook and linting, including the following hooks:

- [ruff](https://github.com/charliermarsh/ruff)

### VSCode default settings

The `.vscode/settings.json` will also be generated with the project, to enable Pylance auto-completions and test discovery in VSCode.

### Tests

- Tests run with [pytest](https://pytest.org/)
- Multi-environment testing powered by [nox](https://nox.thea.codes/)

## Requirements

Make below requirements are met to use the copier template:

- Python 3
- Git
- [Copier](https://copier.readthedocs.io/en/stable/)

