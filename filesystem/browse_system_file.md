# 浏览文件系统

## 切换目录 - `cd`

```shell
cd destination
```

`destination`:  可以为绝对路径或相对路径

```bash
# 绝对路径
[root@server-test-211 ~]# cd /home/kz/test
[root@server-test-211 test]#
```

```bash
# 相对路径，（..）当前目录的父目录
[root@server-test-211 test]# cd ../user
[root@server-test-211 user]#
```

```bash
# 相对路径， (.) 当前目录
[root@server-test-211 kz]# cd ./user
```

## 查看文件/目录路径 - `pwd`

```bash
[root@server-test-211 user]# pwd
/home/kz/user
```