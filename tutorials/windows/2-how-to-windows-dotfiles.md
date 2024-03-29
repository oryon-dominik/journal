# windows-dotfile-environment

> This is about: How-to configure your own dotfile repository


## Prerequisites

If you followed the first tutorial [1-post-installation-windows10](1-post-installation-windows10.md) you're
already set to start with the dotfiles environment. So skip the next paragraph.

Make sure you have installed every prerequisite.
```powershell
# In an admin shell
Invoke-Expression "& { $(irm https://aka.ms/install-powershell.ps1) } -UseMSI"
# open the new shell as a normal user now
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
scoop bucket add main
scoop install main/git
```


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
iex "$env:DOTFILES/install/windows/InstallAdmin.ps1"
```



Install everything from the dotfiles repository.

# ! DEPRECATION WARNING, use this at your own risk. It has changed a lot since I wrote this tutorial.
Have a look at the code.
Or ask me to help.

```powershell
# Setup git, removes old gitconfig, replaces with symlink from dotfiles and
# adds a local (non-version-controlled) gitconfig for your user
. "$env:DOTFILES\install\windows\SetupGit.ps1"
SetupGit -email $null -name $null

# Delete old powershell profiles and symlink the one from the dotfiles.
# Make system links from the cloned powershell profile to both of the generic
# powershell-profile-folders. This will delete the old folders (don't forget to
# backup your old powershell configs, if you have some).
. "$env:DOTFILES\install\windows\SymlinkPowershell.ps1"
SymlinkPowershell

# Install ALL programms
. "$env:DOTFILES/install/windows/InstallAllSoftware.ps1"
EasyInstall

# Symlink the remaining dotfiles
. "$env:DOTFILES/install/windows/SymlinkDotfiles.ps1"
SymlinkDotfiles

# Setup openssh
. "$env:DOTFILES/install/windows/SetupOpenSSH.ps1"
SetupSSH

# Also install git-credential-manager-core for https authentication.
scoop install extras/git-credential-manager

```

---

I don't recommend using anything below this line, it's deprecated and I don't know if it works anymore. I'll keep it here for reference for now.
It might also be helpful to understand how a more granular installation works.


```powershell
# Full install
Invoke-RestMethod -Uri https://raw.githubusercontent.com/oryon-dominik/dotfiles/trunk/install/windows/Install.ps1 | Invoke-Expression
```

---

Install the additional powershell-modules.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force;
Invoke-Expression "$env:DOTFILES/install/windows/InstallAdditionalPowershellModules.ps1"
```

Install packages neccessary for full features and command-availability of these dotfiles.  
Install optional software (If you like, have a look into my essential software packages for everyday work and add them to your system).  

```powershell
# Read and run all packages you want.
# Have a look: https://github.com/oryon-dominik/dotfiles/blob/trunk/install/scoops/scoop-packages.json
$only_install_essentials = $true
InstallScoops -essentials $only_install_essentials -categories @("cli", "development", "fonts", "guis", "languages", "media", "security", "web", "deployment")
```

Now symlink your dotfiles to the installed programs configs. You may get some
elevation errors, depending on your system-config.  
Run the failed lines on an elevated shell again (sudo!) (assuming your user has
elevation privilege, otherwise you have to fix the paths to match the elevated
`$env`).

```powershell
refreshenv;
Set-ExecutionPolicy Bypass -Scope Process -Force;
. "$env:DOTFILES/install/windows/SymlinkDotfiles.ps1"
SymlinkDotfiles
```

You can also add your dotfiles location to explorers quick-access.

```powershell
(new-object -com shell.application).Namespace("$env:DOTFILES").Self.InvokeVerb("pintohome")
```


Restart your shell.

From here on you should be good to go and use your config, now feel free to
[customize your windows dotfiles](3-customize-windows-dotfiles.md)
and follow the rest of my tutorial.
