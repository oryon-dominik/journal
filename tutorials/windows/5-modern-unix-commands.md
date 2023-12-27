# Modern unix commands on Windows 10

Will install `scoop`, `git`, `rustup`, all cargo modules found in this 
[cargo-tools list](https://github.com/oryon-dominik/dotfiles/blob/trunk/install/crates/cargo-tools.json)
and (if you decide to install all additional stuff as well) `golang`, `javascript` and some binaries to your dotfiles and CLI path.


```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

```powershell
scoop install git
```

Load the scripts from locally installed dotfiles

```powershell
. $(Join-Path -Path "$env:DOTFILES" -ChildPath "install/windows/InstallRust.ps1")
. $(Join-Path -Path "$env:DOTFILES" -ChildPath "install/windows/InstallModernUnixForWindows.ps1")
. $(Join-Path -Path "$env:DOTFILES" -ChildPath "install/windows/InstallJavaScript.ps1")
. $(Join-Path -Path "$env:DOTFILES" -ChildPath "install/windows/InstallGolang.ps1")
```

**or** directly from remote.

```powershell
$RustInstallScript = Invoke-WebRequest https://raw.githubusercontent.com/oryon-dominik/dotfiles/trunk/install/windows/InstallRust.ps1
Invoke-Expression $($RustInstallScript.Content)

$ModernUnixInstallScript = Invoke-WebRequest https://raw.githubusercontent.com/oryon-dominik/dotfiles/trunk/install/windows/InstallModernUnixForWindows.ps1
Invoke-Expression $($ModernUnixInstallScript.Content)

$JavaScriptInstallScript = Invoke-WebRequest https://raw.githubusercontent.com/oryon-dominik/dotfiles/trunk/install/windows/InstallJavaScript.ps1
Invoke-Expression $($JavaScriptInstallScript.Content)

$GoLangInstallScript = Invoke-WebRequest https://raw.githubusercontent.com/oryon-dominik/dotfiles/trunk/install/windows/InstallGolang.ps1
Invoke-Expression $($GoLangInstallScript.Content)
```

Now run the scripts.

```powershell
# Install the dependencies for the packages.
InstallRustToolchain
InstallJavaScriptToolchain
InstallGolangToolchain
```

```powershell
InstallModernUnixToolchain
```

## Additional packages.

Create the (gitignored) `.dotfiles/bin` directory if it doesn't exist

```powershell
mkdir "$env:DOTFILES/bin" -ErrorAction SilentlyContinue
```

Pick the latest windows executables for these additional packages from github and save them to `$env:DOTFILES/bin`.

- [dog - dns lookup](https://github.com/ogham/dog/releases)
- [jq - Command-line JSON processor](https://github.com/stedolan/jq/releases)
- [curlie - The power of curl, the ease of use of httpie.](https://github.com/rs/curlie/releases)
