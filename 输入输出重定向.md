# 输入输出重定向

> 将**命令**的输出重定向到另一个位置（文件），将文件作为命令的输入

## 输出重定向

### 覆盖文件原内容

> `command > outputfile`

```bash
# 将日期输出到文件
[root@server-test-211 kz]# date > test.sh

[root@server-test-211 kz]# cat test.sh
Thu May 23 10:43:06 CST 2019

```

```bash
#查看docker安装路径，并输出到文件
[root@server-test-211 kz]# whereis docker > test.sh
[root@server-test-211 kz]# cat test.sh
docker: /usr/bin/docker /etc/docker /usr/libexec/docker /usr/share/man/man1/docker.1.gz

```

### 不覆盖文件原内容-追加

> `command >> outputfile`

```bash
[root@server-test-211 kz]# date >> test.sh
[root@server-test-211 kz]# cat test.sh
docker: /usr/bin/docker /etc/docker /usr/libexec/docker /usr/share/man/man1/docker.1.gz
Thu May 23 10:48:32 CST 2019
```

## 输入重定向

> `command < inputfile`

```bash
[root@server-test-211 kz]# wc < test.sh
  2  11 117

```

## 管道

> 将一个命令的输出作为另一个命令的输入
>
> `command1 | command2`

```bash
# rpm 输出安装包列表，排序存放到rpm.txt文件
[root@server-test-211 kz]# rpm -qa | sort > rpm.txt

```

```bash
[root@server-test-211 kz]# ll
total 160
-rw-r--r--. 1 root root      0 May 15 16:13 admin.html
-rw-r--r--. 1 root root     48 May 16 11:47 index.html
-rw-r--r--. 1 root root 104658 May 20 09:54 installed_software.txt
-rw-r--r--. 1 root root  43492 May 24 13:56 rpm.txt
drwxr-xr-x. 2 root root     56 May 16 14:00 test
-rw-r--r--. 1 root root   2212 May 15 17:37 test.html
-rwxr--r--. 1 skz  root    140 May 23 10:59 test.sh
drwxr-xr-x. 2 root root     23 May 17 09:30 user

```

```bash
# 查看前四行内容
[root@server-test-211 kz]# head -4 rpm.txt 
abattis-cantarell-fonts-0.0.16-3.el7.noarch
abrt-2.1.11-45.el7.centos.x86_64
abrt-addon-ccpp-2.1.11-45.el7.centos.x86_64
abrt-addon-kerneloops-2.1.11-45.el7.centos.x86_64
```

```bash
# 排序输出前6条包列表9记录
[root@server-test-211 kz]# rpm -qa | sort | head -6
abattis-cantarell-fonts-0.0.16-3.el7.noarch
abrt-2.1.11-45.el7.centos.x86_64
abrt-addon-ccpp-2.1.11-45.el7.centos.x86_64
abrt-addon-kerneloops-2.1.11-45.el7.centos.x86_64
abrt-addon-pstoreoops-2.1.11-45.el7.centos.x86_64
abrt-addon-python-2.1.11-45.el7.centos.x86_64

```