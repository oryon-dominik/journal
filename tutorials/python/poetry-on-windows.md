# Installation and Setup of python poetry on windows with powershell


Attention: poetry is very annoying, and i'll try to replace it as soon as I can.

## Installation

1. Install [poetry](https://python-poetry.org/)

    Because of versioning problems with poetry I am not following the official installation guide
    (~~`(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -`~~).

    I'm installing poetry for every major system python with [pipx](pipx.md). (~~`pipx install poetry`~~)
        # for the latest version of poetry you can install the wheels directly from github
        pipx install https://github.com/python-poetry/poetry/releases/download/1.2.0b2/poetry-1.2.0b2-py3-none-any.whl


2. For a fit to my dotfiles-settings, change the virtualenvs-directory setting

        poetry config virtualenvs.path $env:USERPROFILE\Envs


## Commands

    poetry --version            # show the version
    poetry config --list        # show the config
    poetry env info             # show info about the env you're in
    poetry init                 # interactively initializes a new poetry project
    poetry install              # installs dependencies from `pyproject.toml`
    poetry update               # latest version of dependencies
    poetry add <name>           # adds a package to pyproject.toml
    poetry remove <name>        # removes a package


## Migrate an existing project

From old `requirements.txt`

    poetry init
    foreach($requirement in (Get-Content "$pwd\requirements.txt")) {Invoke-Expression "poetry add $requirement"}


