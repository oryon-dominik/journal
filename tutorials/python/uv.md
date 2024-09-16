
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

