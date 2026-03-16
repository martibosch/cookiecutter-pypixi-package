[![CI](https://github.com/martibosch/cookiecutter-pypixi-package/actions/workflows/dev.yml/badge.svg)](https://github.com/martibosch/cookiecutter-pypixi-package/blob/main/.github/workflows/dev.yml)
[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/martibosch/cookiecutter-pypixi-package/main.svg)](https://results.pre-commit.ci/latest/github/martibosch/cookiecutter-pypixi-package/main)
[![GitHub license](https://img.shields.io/github/license/martibosch/cookiecutter-pypixi-package.svg)](https://github.com/martibosch/cookiecutter-pypixi-package/blob/main/LICENSE)

# Cookiecutter PyPixi package

Template for Python packages using Pixi.

## Features

This project template includes the following features to ensure best practices:

- **Overall project configuration**: [pyproject.toml](https://www.python.org/dev/peps/pep-0518) for [PEP-621](https://peps.python.org/pep-0621)-compliant project configuration, packaging with [`uv_build`](https://docs.astral.sh/uv/concepts/build-backend), and task/environment management with [pixi](https://pixi.sh).
- **Tests**:
  - [pixi](https://pixi.sh) environments and tasks for testing against multiple Python versions in GitHub Actions.
  - [coverage](https://coverage.readthedocs.io) reporting with [codecov](https://codecov.io) integration.
- **Documentation**: generated with [sphinx](https://www.sphinx-doc.org), using [MyST](https://myst-parser.readthedocs.io) for Markdown support, auto API generation from docstrings and hosting on [readthedocs](https://readthedocs.org) with the [pydata-sphinx-theme](https://github.com/pydata/pydata-sphinx-theme) through a Pixi-managed docs environment.
- **Code quality**: set up with [pre-commit](https://pre-commit.com) to run checks and tests before each commit, including, among others:
  - [ruff](https://beta.ruff.rs) for Python code linting and formatting
  - [codespell](https://github.com/codespell-project/codespell) to check for common misspellings
  - [pyupgrade](https://github.com/asottile/pyupgrade) to automate upgrade syntax for newer Python versions
- **Continuous integration and delivery** with [GitHub Actions](https://github.com/features/actions), with jobs to run tests, publishing to test PyPI and releasing to PyPI and GitHub on new tags.
- **Conventional commits and semantic versioning** with [commitizen](https://commitizen-tools.github.io/commitizen) to enforce [conventional commits](https://www.conventionalcommits.org) (with `commit-msg` pre-commit hooks), version bumping using [semantic versioning](https://semver.org) and automated change log generation.

## Usage

### First time setup

Generate a new project using [cookiecutter](https://github.com/cookiecutter/cookiecutter):

```bash
cookiecutter gh:martibosch/cookiecutter-pypixi-package
```

and fill in the prompts. Then, navigate to the generated directory and follow the instructions below:

- Install [pixi](https://pixi.sh/latest) and create the local development environment with `pixi install -e dev`.
- Commit the generated `pixi.lock` file after the first successful resolve, and update/commit it again whenever dependencies change.
- Initialize a git repository (e.g., `git init`) and install the pre-commit hooks by running `pixi run -e dev pre-commit install` and `pixi run -e dev pre-commit install --hook-type commit-msg`.
- Register the project in [codecov](https://codecov.io) and [readthedocs](https://readthedocs.org).
- If the repository is public, enable [pre-commit.ci](https://pre-commit.ci) to automatically run pre-commit checks on GitHub and autoupdate the pre-commit hook versions.
- Create accounts (or use existing accounts) and [set up pending publishers for the github repository](https://docs.pypi.org/trusted-publishers/creating-a-project-through-oidc) for [PyPI](https://pypi.org) and [test PyPI](https://test.pypi.org). Enter "release.yml" in the "Workflow name" field and respectively "pypi" and "testpypi" in the "Environment name" field.

You can then start developing your package with `pixi run -e test test` and `pixi run -e doc build-doc`.

If you want stricter CI after committing `pixi.lock`, you can set `frozen: true` in the generated GitHub Actions workflows so CI fails when the lockfile is missing or out of date.

### Submit a recipe to conda-forge

If you want your package to be available from [conda-forge](https://conda-forge.org), you can generate a recipe for it using [grayskull](https://github.com/conda/grayskull) and then submit it by following the instructions in the [conda-forge documentation](https://conda-forge.org/docs/maintainer/adding_pkgs.html#forking-and-pull-request).

## Acknowledgements

- This template borrows several ideas from [zillionare/python-project-wizard](https://github.com/zillionare/python-project-wizard).
