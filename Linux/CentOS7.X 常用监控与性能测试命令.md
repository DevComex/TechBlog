### 测试磁盘IO速度
测试/data/目录的真实写入速度
```
time dd if=/dev/zero of=/data/test.dbf bs=8k count=300000 oflag=direct
```
测试磁盘读取速度
```
yum install hdparm
hdparm -Tt /dev/sdb
```