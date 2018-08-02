**安装图形界面**

```shell
yum groupinstall "GNOME Desktop" "Graphical Administration Tools"

ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target
```

**配置hostname**

```shell
hostnamectl set-hostname <host-name>
```



