# `shell` 命令

## 外部命令 - `which | type`

> 非 `bash shell` 自带程序，通常位于`/bin`、`/usr/bin`、`/sbin`或`/usr/sbin`中的安装程序，可通过 `which` 或 `type`命令找到，`which`只能查询外部命令

```bash
[root@server-test-211 kz]# type ps
ps is /usr/bin/ps
[root@server-test-211 kz]# which ps
/usr/bin/ps
```

## 内建命令 - `type`

> `bash shell` 自带命令程序，通过`type`进行查找，（存在多种实现的命令，即外部命令及内建命令并存）

| 选项 | 用途 |
|:-------|:-----|
|  | 内建命令 |
| -a | 内建命令，外部命令|

```bash
[root@server-test-211 kz]# type exit
exit is a shell builtin
[root@server-test-211 kz]# which exit
/usr/bin/which: no exit in (/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin)

```

```bash
[root@server-test-211 kz]# type -a cd
cd is a shell builtin
cd is /usr/bin/cd

[root@server-test-211 kz]# which echo
/usr/bin/echo
```

## 历史命令使用记录 - `history`

> 查询 `shell` 命令使用记录

```bash
[root@server-test-211 kz]# history
    1  csh
    2  exit
    3  cd /home

```

## 命令别名 - `alias`

### 查看现有可用别名 - `alias -p`

```bash
[root@server-test-211 kz]# alias -p
alias cp='cp -i'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias li='ls -li'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'

```

### 自定义别名 - `alias [别名]='[命令]'`

```bash
[root@server-test-211 kz]# alias li='ls -li'


[root@server-test-211 kz]# li
total 20
269629433 -rw-r--r--. 1 root root     0 May 15 16:13 admin.html
269629435 -rw-r--r--. 1 root root    48 May 16 11:47 index.html
537281613 drwxr-xr-x. 2 root root    56 May 16 14:00 test
269629429 -rw-r--r--. 1 root root 10240 May 16 14:16 test-archive.rar
269629434 -rw-r--r--. 1 root root  2212 May 15 17:37 test.html
```