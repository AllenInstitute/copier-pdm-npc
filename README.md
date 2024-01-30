# Copier PDM + MindScope NP

Copier template for MindScope Neuropixels projects to get up and running quickly with automated formatting, testing, publishing and docs.

## Quick Start

1. Install [PDM](https://copier-pdm.fming.dev/) via [pipx](https://github.com/pypa/pipx) (for isolated CLI tools):
```bash
python3 -m pip install --user pipx
```

2. Add [Copier](https://copier.readthedocs.io/en/stable/) to PDM:
```bash
pipx run pdm self add copier
```

3. Initialize the project folder and answer the questions that appear:
```bash
pipx run pdm init --copier gh:bjhardcastle/copier-pdm-npc --UNSAFE
```
- see this [documentation](https://copier-pdm.fming.dev) for more details.

4. Add a remote on Github
5. Go to the `Actions` menu in Github and create the secrets used in `publish.yml`
6. To simplify publishing to PyPI, set up OIDC [here](https://pypi.org/manage/account/publishing/), using the `publish.yml` workflow:
   > OpenID Connect (OIDC) provides a flexible, credential-free mechanism for delegating publishing authority for a PyPI package to a trusted third party service, like GitHub Actions
## Features

### Package manager

The template project uses [PDM](https://pdm.fming.dev) for reproducible dev environments, with pre-defined `pyproject.toml` configuration for tools
While working on the project, use pdm to manage dependencies:
- add dependencies: `pdm add numpy pandas`
  - add dev dependencies: `pdm add -G dev mypy`
- remove dependencies correctly: `pdm remove numpy`   # does nothing because pandas still needs numpy!
- update the environment to reflect changes in `pyproject.toml`: `pdm update`
Always commit & push `pdm.lock` to share the up-to-date dev environment

### VSCode config
- `.vscode/settings.json` will be generated with the project, to enable mypy static analysis (instead of Pylance)
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

- tests discovered in `tests` and all doctests (including in `README.md`) are run with [pytest](https://pytest.org/)
- mypy is run (without strict mode, so untyped functions will not be analyzed)

#### Publishing
Provided all tests pass, the package is published to [PyPI](https://pypi.org)
