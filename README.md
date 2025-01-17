
# openEO Test Suite

Test suite for validation of openEO back-ends against the openEO API and related specifications.

## Install/Setup


As always in Python usage and development,
it is recommended to work in some sort of virtual environment (`venv`, `virtualenv`, `conda`, `docker`, ...)
to run and develop this project.
Depending on your use case and workflow, you can choose to reuse an existing environment or create a new one.

### Example virtual environment setup

Python's standard library includes a [`venv` module](https://docs.python.org/3/library/venv.html)
to create virtual environments.
A common practice is to create a virtual environment in a subdirectory `venv` of your project,
which can be achieved by running this from the project root:

```bash
python -m venv --prompt . venv
```

Note: the `--prompt .` option is a trick to automatically
use the project root directory name in your shell prompt
when the virtual environment is activated.
It's optional, but it generally makes your life easier
when you have multiple virtual environments on your system.

### Virtual environment activation

The following instructions will assume that the virtual environment of your choosing is activated.
For example, when using the `venv` approach from above,
activate the virtual environment in your shell with:

```bash
source venv/bin/activate
```

### Install dependencies

Install the project and its dependencies in your virtual environment with:

```bash
pip install -e .
```

Note: the `-e` option installs the project in "editable" mode,
which makes sure that code changes will be reflected immediately in your virtual environment
without the need of (re)installing the project.


## Running the test suite

The test suite at least requires an openEO backend URL to run against.
It can be specified through a `pytest` command line option

    pytest --openeo-backend-url=openeo.example

or through an environment variable `OPENEO_BACKEND_URL`

    export OPENEO_BACKEND_URL=openeo.example
    pytest

If no explicit protocol is specified, `https://` will be assumed automatically.



## Development and contributions

The test suite builds on [`pytest`](https://pytest.org/),
a featureful testing library for Python that makes it easy to write succinct, readable tests
and can scale to support complex functional testing.
It has some particular features (fixtures, leveraging the `assert` statement, test parameterization, ...)
that are worth getting familiar with.

### Pre-commit hooks

This project provides (git) pre-commit hooks to tidy up simple code quality problems and catch syntax issues before committing.
While not enforced, it is encouraged and appreciated to enable this in your working copy before contributing code.

#### Pre-commit Setup

- Install the general [pre-commit](https://pre-commit.com/) tool.
  The simplest option is to install it directly in the virtual environment you are using for this project (e.g. `pip install pre-commit`)
  You can also install it globally
  (e.g. using a package manager like [pipx](https://pypa.github.io/pipx/), conda, homebrew, ...)
  so you can use this tool across different projects.
- Install the project specific git hook scripts and utilities
  (defined in the `.pre-commit-config.yaml` configuration file)
  by running this in the root of your working copy:

      pre-commit install

#### Pre-commit Usage

When you commit new changes, the pre-commit hook will automatically run each of the configured linters/formatters/...
Some of these just flag issues (e.g. invalid JSON files) while others even automatically fix problems (e.g. clean up excessive whitespace).
If there is some kind of violation, the commit will be blocked. Address these problems and try to commit again.

Some pre-commit tools directly edit your files (e.g. fix code style) instead of just flagging issues.
This might feel intrusive at first, but once you get the hang of it, it should allow to streamline your development workflow.
In particular, it is recommended to use git's staging feature to prepare your commit.
Pre-commit’s proposed changes are not staged automatically, so you can more easily keep them separate for review.

> **Note**
> You can temporarily disable pre-commit for these rare cases where you intentionally want to commit violating code style,
> e.g. through git commit command line option `-n/--no-verify`.
