# Windows 10 wsl-setup

If you followed the windows tutorials [1-post-installation-windows10](1-post-installation-windows10.md),
[2-how-to-windows-dotfiles](2-how-to-windows-dotfiles.md) and
[3-customize-windows-dotfiles](3-customize-windows-dotfiles.md) continue with WSL-setup.


Enable WSL

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

Set the version to wsl2

    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart
    wsl.exe --set-default-version 2

Download the kernel-component update for wsl2. It's possible, that you have to download
and install [the wsl-2-kernel](https://docs.microsoft.com/de-de/windows/wsl/wsl2-kernel) manually by hand.

    ~~Invoke-WebRequest -Uri https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi -OutFile "$env:USERPROFILE/Downloads/wsl_update_x64.msi;"~~
    ~~Start-Process "msiexec.exe" -ArgumentList "/I '$env:USERPROFILE/Downloads/wsl_update_x64.msi' /quiet" -Wait -NoNewWindow~~

Download and install ubuntu-20.04 directly from the Microsoft-Store (recommended).

    ~~Invoke-WebRequest -Uri https://aka.ms/wslubuntu2004 -OutFile "$env:USERPROFILE/Downloads/Ubuntu2004.appx" -UseBasicParsing~~
    ~~Add-AppxPackage "$env:USERPROFILE/Downloads/Ubuntu2004.appx"~~

Or install via CLI

```powershell
wsl --list --online

wsl --install -d Ubuntu-22.04
```

Verify the installation

    wsl --list --verbose

Set the default version for wsl

    wsl --set-version Ubuntu-20.04 2;
    wsl --set-default Ubuntu-20.04

Pin the wsl-mount-point to your explorer quick access.

    (new-object -com shell.application).Namespace('\\wsl$\Ubuntu-20.04').Self.InvokeVerb("pintohome")


Activate wsl and setup user and root password

    wsl

You're on a native ubuntu environment now. Time to setup your [ubuntu dotfiles](../ubuntu/1-how-to-ubuntu-dotfiles.md)

---

### podman vpn fixes

```bash
wsl -d podman-machine-default
sudo tee /etc/wsl.conf << EOF  
  [network]  
  generateResolvConf = false  
EOF
sudo rm -rf /etc/resolv.conf
echo "nameserver 1.1.1.1" | sudo tee /etc/resolv.conf
```

you might also need [wsl-vpnkit](https://github.com/sakai135/wsl-vpnkit)
```powershell
# install the latest release
wsl --import wsl-vpnkit . ./wsl-vpnkit.tar.gz

# run in the foreground
wsl.exe -d wsl-vpnkit --cd /app wsl-vpnkit
```

Probably you could also set this up as a systemd service in your podman distro: https://github.com/sakai135/wsl-vpnkit  

