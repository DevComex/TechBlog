### 修改默认的ssh端口
默认的22端口，风险较高，可能被攻击，我们改为其他端口，如 47289
```
vim /etc/ssh/sshd_config
```
增加我们想要设置的端口，如
```
Port 47289
```
然后保存退出，重启sshd即可
```
systemctl restart sshd
```

### 在防火墙策略中开放特定端口
首先添加策略(--permanent表示设置为永久策略，如果不加此选项表示重启后失效)
```
firewall-cmd --zone=public --add-port=47289/tcp --permanent
```
重新载入新的配置
```
firewall-cmd --reload
```

### 在SELinux中开放特定端口
执行下述命令(http_port_t/ssh_port_t)
```
semanage port -a -t ssh_port_t -p tcp 47289
reboot
```

### 将已有分区的磁盘挂载到系统（CentOS）中
首先查看现有的磁盘情况
```
fdisk -l
```
![](https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-28_013821.png)
发现已有分区/dev/md127，只需将其挂载到我们想要的目录即可
首先创建我们所需的目录
```
mkdir /comexDir
```
修改
```
cp /etc/fstab /etc/fstab.`date +%Y%m%d.%H%M%S`
vi /etc/fstab
```
在其中添加如下内容(其中/comexDir为我们需要挂载的目录)
```
/dev/md127 /comexDir ext4 defaults 1 2
```
然后重新mount
```
mount -a
```
最后查看挂载结果
```
df -h
```

### 修改中文语言为英文语言
首先备份相关配置文件
```
cp /etc/locale.conf /home/locale.conf.`date +%Y%m%d.%H%M%S`
```
然后修改此配置文件内容
```
echo LANG=\"en_US.UTF-8\" > /etc/locale.conf
```
最后重启系统即可
```
reboot
```

### 卸载软件
查看已经安装的软件
```
yum list installed | grep qt
```
卸载指定名称的软件包
```
rpm -e qt-devel.x86_64
```

### CentOS7 支持NTFS文件系统
```
wget https://tuxera.com/opensource/ntfs-3g_ntfsprogs-2017.3.23.tgz
tar -zxf ntfs-3g_ntfsprogs-2017.3.23.tgz 
cd ntfs-3g_ntfsprogs-2017.3.23/
./configure
make
make install
```

### 使用ntfs-3g挂载NTFS文件系统
创建目录并挂载（重启后失效）
```
mdkir /comex
mount -t ntfs-3g /dev/sdb1 /comex
```
设置重启后自动挂载（编辑文件/etc/fstab，添加如下内容）
```
/dev/sdb1 /comex ntfs-3g defaults 0 0
```