
```bash
#1 安装 WSL2 + Ubuntu
wsl --install
# Or pick a distro explicitly:
wsl --list --online
wsl --install -d Ubuntu-24.04

#2 启用 systemd（Gateway 网关安装所需）
sudo tee /etc/wsl.conf >/dev/null <<'EOF'
[boot]
systemd=true
EOF


wsl --shutdown
systemctl --user status



```








其他命令：
```bash
#设置默认系统
wsl.exe --set-default <Distro>

#更新依赖
sudo apt update && sudo apt upgrade

#设置root密码
sudo passwd  root

```
`


