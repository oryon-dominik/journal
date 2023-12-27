# Windows 10 post-installation

Open a powershell.

Install the modern powershell.

```powershell
Invoke-Expression "& { $(irm https://aka.ms/install-powershell.ps1) } -UseMSI"
```

Open the new powershell.

Then install [scoop](https://scoop.sh/).

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
# maybe: Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

Install git via scoop.

```powershell
# https://gitforwindows.org/
scoop bucket add main
scoop install main/git
```

(Optional) Set up your `ssh-key`.

```powershell
mkdir "$env:USERPROFILE/.ssh/"
ssh-keygen -t ecdsa -C "A comment of your choice" -f "$env:USERPROFILE/.ssh/id_ecdsa"
```

(Optional) Set a new cool [hostname](http://seriss.com/people/erco/unixtools/hostnames.html) 🌒.

```powershell
Rename-Computer -ComputerName $env:computername -NewName "enceladus"
```

Reboot, [setup dotfiles](2-how-to-windows-dotfiles.md).
