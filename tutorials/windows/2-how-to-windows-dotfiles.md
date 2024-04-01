# windows-dotfile-environment

> This is about: How-to configure your own dotfile repository


## Prerequisites

If you followed the first tutorial [1-post-installation-windows10](1-post-installation-windows10.md) you're
already set to start with the dotfiles environment. Make sure you have installed every prerequisite (`scoop`, `git`, `powershell > 7` & the `visual studio C++ buildtools`).

Open a powershell.


## Setup your dotfiles repository

Create a directory for the location you want to install your config to. Then set an environment variable (`$env:DOTFILES`) pointing to it.

```powershell
# Set the execution policy, to make your scripts executable for the user 
# (You could also elaborate on that to a script-by-script policy).
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

```powershell
New-Item -Path "$env:USERPROFILE/.dotfiles" -ItemType Directory -Force
```

```powershell
$env:DOTFILES = Convert-Path "$env:USERPROFILE/.dotfiles"
```

```powershell
[Environment]::SetEnvironmentVariable("DOTFILES", "$env:DOTFILES", "User")
```


Recommended: Clone | Fork this dotfile git repository to `$env:DOTFILES`.

```powershell
git clone https://github.com/oryon-dominik/dotfiles "$env:DOTFILES"
```

Then run the installation preparation script.

```powershell
iex "$env:DOTFILES/install/windows/InstallPrepare.ps1"
```


Then re-open as admin and run the admin-installation script.

```powershell
iex "$env:DOTFILES/install/windows/InstallAsAdmin.ps1"
```

Now re-open a fresh unprivileged users shell and install the essential software packages.
```powershell
. "$env:DOTFILES/install/windows/InstallAllSoftware.ps1"
EasyInstall -use_defaults $true
```

Restart your shell.

From here on you should be good to go and use your config, now feel free to
[customize your windows dotfiles](3-customize-windows-dotfiles.md)
and follow the rest of my tutorial.

---

Customize your `$env:DOTFILES/.env` if you want to change things.  

To install optional software, have a look into my essential software packages for everyday work and add them to your system.  

```powershell
# Read and run all packages you want.
# Have a look: https://github.com/oryon-dominik/dotfiles/blob/trunk/install/scoops/scoop-packages.json
```powershell
. "$env:DOTFILES/install/windows/InstallScoopBucketsAndPackages.ps1"
$only_install_essentials = $true
InstallScoops -essentials $only_install_essentials -categories @("cli", "development", "fonts", "guis", "languages", "media", "security", "web", "deployment")
```

You can also add your dotfiles location to explorers quick-access.

```powershell
(new-object -com shell.application).Namespace("$env:DOTFILES").Self.InvokeVerb("pintohome")
```

### Troubleshooting

Always read your instructions and feedback on the screen carefully.  
Have a look at the code.  
Or ask me to help.  

If you want [mcfly](https://github.com/cantino/mcfly)-history (and it does work on your setup), edit your `$env:DOTFILES/.env` and activate it.

```
MCFLY_ISACTIVE=true
```
