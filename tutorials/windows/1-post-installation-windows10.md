# Windows 10 post-installation

Open an admin-powershell.

Then install [scoop](https://scoop.sh/).

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
# maybe: Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```

Install git via scoop.

```powershell
# https://gitforwindows.org/
scoop bucket add main
scoop install main/git
```

Install powershell via scoop.

```powershell
# https://gitforwindows.org/
scoop bucket add main
scoop install main/pwsh
# Install powershell, start it and set a new profile.
```

Set up your `ssh-key`.

```powershell
mkdir "$env:USERPROFILE/.ssh/"
ssh-keygen -t ecdsa -C "A comment of your choice" -f "$env:USERPROFILE/.ssh/id_ecdsa"
```

(Optional) Set a new cool [hostname](http://seriss.com/people/erco/unixtools/hostnames.html) 🌒.

```powershell
Rename-Computer -ComputerName $env:computername -NewName "enceladus"
```

Reboot, [setup dotfiles](2-how-to-windows-dotfiles.md).
