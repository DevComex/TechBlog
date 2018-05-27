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