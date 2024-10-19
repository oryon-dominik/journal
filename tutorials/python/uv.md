
Installation

#### posix

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
```

#### windows 

```powershell
irm https://astral.sh/uv/install.ps1 | iex
```


#### add windows cfg paths with dotfiles

```powershell
Remove-Item -path "$UserPath/.config/uv.toml" -recurse -force -ErrorAction SilentlyContinue
New-Item -Path "$UserPath/.config/uv.toml" -ItemType SymbolicLink -Value "$env:DOTFILES/common/python/uv.toml"
```


### Issues

If some pacakges do not install:

- Try to wipe the cache-directory configured with `uv clean`.  
- Check if all build tools required for the package (C, C++, Haskell, rust) are installed and on `PATH`.
- Another useful workaround for unavailable wheels is to pre-install a matching binary package downloaded from [gohlkes pythonlibs](https://www.lfd.uci.edu/~gohlke/pythonlibs/) via `pip` to your activated venv and then add it via `uv`.


### Commands

    uv --version                # show the version
    uv init                     # initializes a new uv project
    uv sync                     # installs dependencies from `pyproject.toml`
    uv sync --all-extras        # installs all extra groups
    poetry update               # latest version of dependencies
    uv add <name>               # adds a package to pyproject.toml
    uv remove <name>            # removes a package


## Migrate an existing project

From old `requirements.txt`

    poetry init
    foreach($requirement in (Get-Content "$pwd\requirements.txt")) {Invoke-Expression "poetry add $requirement"}

