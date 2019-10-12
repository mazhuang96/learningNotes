# linux command

[命令搜索](https://wangchujiang.com/linux-command/)

## 查看系统信息

```sh
# 查看系统版本号
$ cat /etc/issue
Ubuntu 18.04.2 LTS \n \l
# 查看系统信息
$ uname -a
Linux ubuntu 4.15.0-48-generic \#51-Ubuntu SMP Wed Apr 3 08:28:49 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```

## 查看端口进程

```sh
netstat -nap | grep 端口号
```

## 修改文件夹用户组

```sh
chown [-R] 账号名称 文件或目录
chown [-R] 账号名称:用户组名称 文件或目录
```
