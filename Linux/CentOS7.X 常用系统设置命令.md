*** 修改默认的ssh端口
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
