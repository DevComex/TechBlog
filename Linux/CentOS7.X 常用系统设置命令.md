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