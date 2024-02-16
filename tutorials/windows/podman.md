Install & prepare podman on windows.

``` powershell
scoop install main/podman
scoop install main/podman-desktop
scoop install main/docker-compose

podman machine init
podman machine start
```

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
