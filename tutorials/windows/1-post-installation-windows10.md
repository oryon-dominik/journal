# Windows 10 post-installation

Open a powershell.

Install the modern powershell (as an admin).

```powershell
Invoke-Expression "& { $(irm https://aka.ms/install-powershell.ps1) } -UseMSI"
```

(Optional) Set a new cool [hostname](http://seriss.com/people/erco/unixtools/hostnames.html) 🌒.

```powershell
Rename-Computer -ComputerName $env:computername -NewName "enceladus"
```

Open the new powershell (as a normal user).

Then install [scoop](https://scoop.sh/).

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
# maybe: Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
Invoke-RestMethod -Uri https://get.scoop.sh | Invoke-Expression
```

Install git via scoop.

```powershell
# https://gitforwindows.org/
scoop install git
```


(Optional) Set up your `ssh-key`.

```powershell
mkdir "$env:USERPROFILE/.ssh/"
ssh-keygen -t ed25519 -C "$env:USERPROFILE@$(hostname)" -f "$env:USERPROFILE/.ssh/id_ed25519"
```


Reboot, [setup dotfiles](2-how-to-windows-dotfiles.md).
