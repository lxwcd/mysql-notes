**mycli 使用笔记**



# 资源
> [mycli](https://github.com/dbcli/mycli)


# 安装
- ubuntu 22.04 
  
```bash
sudo apt install mycli -y
```

# 环境
- Ubuntu 22.04
- MySQL 版本
- MyCLI 版本
```bash
MySQL 8.0.43
mycli 1.24.3
```

# 初次登录

## 本机套接字登录
```bash
[root@Ubuntu2204 ~]$ mycli -uroot
Connecting to socket /var/run/mysqld/mysqld.sock, owned by user mysql
MySQL 8.0.43
mycli 1.24.3
Home: http://mycli.net
Bug tracker: https://github.com/dbcli/mycli/issues
Thanks to the contributor - Phil Cohen
MySQL root@(none):(none)>

```


`mycli -uroot` 走 **unix‑socket套接字登录，不走TCP/IP网络**
```
Connecting to socket /var/run/mysqld/mysqld.sock
```
这里**没有使用3306端口TCP网络**，直接用本地文件套接字登录MySQL。

提示符 `root@(none):(none)> `含义：
- `root`：mysql数据库用户名
- `(none)`：**没有使用TCP主机，socket连接没有host信息**

连接文件：`/var/run/mysqld/mysqld.sock`
- 不经过TCP/IP、不走`bind‑address`配置！
- **依靠操作系统当前登录Linux用户名做身份校验**
- Ubuntu安装的MySQL默认：Linux root用户可以socket免密登录数据库root账号。
- 此时`bind‑address=127.0.0.1`也完全不影响socket登录。

> `bind‑address` **只管TCP网络连接，对socket完全无效**。

或者下面方式也是套接字登录
```bash
[root@Ubuntu2204 ~]$ mycli -uroot -hlocalhost
Connecting to socket /var/run/mysqld/mysqld.sock, owned by user mysql
MySQL 8.0.46
mycli 1.24.3
Home: http://mycli.net
Bug tracker: https://github.com/dbcli/mycli/issues
Thanks to the contributor - Johannes Hoff
MySQL root@localhost:(none)> select user,host from mysql.user;
                          ->
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| debian-sys-maint | localhost |
| mysql.infoschema | localhost |
| mysql.session    | localhost |
| mysql.sys        | localhost |
| qt               | localhost |
| root             | localhost |
+------------------+-----------+
6 rows in set
Time: 0.015s
```

## TCP方式本地登录
```bash
```

# 添加账号
初次只有 localhost 登录，添加本地环回地址
```sql

```


# 切换为 vi-mode
- 默认按 F4 键


# 改为多行模式
- 按 F3，只能临时生效
