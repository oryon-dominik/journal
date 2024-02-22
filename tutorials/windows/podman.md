
Install & configure podman on windows.

Assumes a [prepared wsl](https://github.com/oryon-dominik/dotfiles/blob/trunk/common/wsl/get-wsl-runnning.md).

## Install

``` powershell
scoop install main/podman
scoop install extras/podman-desktop
scoop install main/docker-compose

podman machine init
podman machine start
```

## Config

```powershell
wsl -d podman-machine-default

sudo tee /etc/wsl.conf << EOF  
  [network]  
  generateResolvConf = false  
EOF

# delete the existing symlink(!)
sudo rm -rf /etc/resolv.conf
echo 'nameserver 1.1.1.1' > /etc/resolv.conf
```
