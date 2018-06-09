# 安装samba
```
yum install samba samba-common samba-client  -y
```

# 为Samba配置SELinux
```
semanage fcontext -a -t public_content_rw_t '/pt(/.*)?'
restorecon -R -v /pt
setsebool -P samba_export_all_rw 1
```

# 执行restorecon命令来激活修改的标签
restorecon -R -v /pt 

# 设置防火墙例外
firewall-cmd --permanent --add-service=samba

# 编辑共享设置
nano /etc/samba/smb.conf
```
[pt]
path = /pt
public = yes
writable = yes
valid users = comex
create mask = 0644
force create mode = 0644
directory mask = 0755
force directory mode = 0755
available = yes
```

# 添加Samba用户
smbpasswd -a comex

# 激活Samba服务，并重启服务
```
systemctl enable smb.service
/bin/systemctl restart smb.service
```
