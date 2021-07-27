# Mac Dev Environment Installation and Setup

This project tracks its Python dependencies using [Poetry](https://python-poetry.org/). As
such, to work on this project, the following steps are recommended in order to set up a Python
virtual environment.

This document assumes you are using a Mac 11.5+ machine; though, it should be easy enough to
adapt the installation instructions for a different OS.

> **Note:** If you are not running Mac 11.5+, then you will need to adapt the steps provided
> for your system.

## pyenv

It's recommended to use [pyenv](https://github.com/pyenv/pyenv) to manage Python versions.

Assuming Homebrew is installed, you may run the following to install it:

```bash
$ brew install pyenv
```

Run the following commands to add `pyenv` to your shell `$PATH`:

```bash
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/shims:$PATH"' >> ~/.bashrc
```

Then source your `~/.bashrc`, like so:

```bash
$ source ~/.bashrc
```

Install the version of Python tracked in [`.python-version`](../.python-version):

```bash
$ cat .python-version | pyenv install
```

Now switch to that Python version, like so:

```bash
$ eval "$(pyenv init -)"
```

## Poetry

This project has some dependencies that are installed via Poetry. Poetry can be installed via
Homebrew:

```bash
$ brew install poetry
```

Poetry uses the [`pyproject.toml`](../pyproject.toml) and [`poetry.lock`](../poetry.lock)
files to track dependencies. Install the project dependencies, like so:

```bash
$ poetry install
```

### Two ways to use the Poetry environment

You can either spawn a new shell with the Python virtual environment instantiated, like so:

```bash
$ poetry shell
$ ansible-playbook main.yml --ask-become-pass
```

Or you can run commands ad-hoc style by prepending them with `poetry run`, as follows:

```bash
$ poetry run ansible-playbook main.yml --ask-become-pass
```

Now return to the original README for more instructions.
