# Copier PDM + MindScope NP

Copier template for MindScope Neuropixels projects to get up and running quickly with automated formatting, testing, publishing and docs.

## Quick Start

1. Install [pipx](https://github.com/pypa/pipx) for isolated CLI tools:
```bash
python3 -m pip install --user pipx
```

2. Add [Copier](https://copier.readthedocs.io/en/stable/) to [PDM](https://copier-pdm.fming.dev/):
```bash
pipx run pdm self add copier
```

3. Initialize the project folder and answer the questions that appear:
```bash
pipx run pdm init --copier gh:alleninstitute/copier-pdm-npc --UNSAFE
```
- see this [documentation](https://copier-pdm.fming.dev) for more details.

4. Add git and remote:
```bash
git init && git remote add origin https://<personal_access_token>@github.com/<repository_namespace>/{repository_name}
```
5. On the repo's Github page, go to `Settings > Secrets > Actions` and create the
   secrets used in `publish.yml` (at the very least, this will include AWS
   credentials if cloud data is accessed for testing)
6. To simplify publishing to PyPI, set up OIDC [here](https://pypi.org/manage/account/publishing/), using the `publish.yml` workflow:
   > OpenID Connect (OIDC) provides a flexible, credential-free mechanism for
   > delegating publishing authority for a PyPI package to a trusted third party
   > service, like GitHub Actions

## Creating documentation page
If you enabled documentation in the initial questionnaire, a `gh-pages` branch
will be created after the first successful run of `publish.yml` in Github Actions.

To display the docs:
- on the repo's Github page, go to `Settings > Pages`
- choose `Source: Deploy from branch`
- choose the `gh-pages` branch, the `/docs` folder, then save
- after a few seconds, a link to the documentation site should be available at the
  top of the page
- enable a link on the repository homepage by going editing the `About` settings
  (right hand side) and toggling `Use your GitHub Pages website` as the repo's webpage

## Update from original template
As the template develops, you might want to pull changes to update the
project accordingly. 

 -commit all changes first, then run `copier update`

See (here)[https://copier.readthedocs.io/en/stable/updating/] for more details.

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
