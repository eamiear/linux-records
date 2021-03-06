# 用户管理

## 查看系统用户

系统用户信息存放在 `/ect/shadow` 和 `/etc/passwd` 中

```bash
[root@server-test-211 kz]# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
kz:x:1005:1005::/home/kz:/bin/bash
...
```

```bash
[root@server-test-211 kz]# cat /etc/shadow
root:$6$RnO4aI6fLfGPQt...
kz:$6$OPcj3AW...

...
```

## 新增用户 - `useradd`

### 查看新增用户系统默认配置 - `-D`

```bash
[root@server-test-211 home]# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

|配置|描述|
|---|-----|
|GROUP=100|新用户会被添加到GID为100的公共组|
|HOME=/home|新用户的HOME目录将会位于/home/loginname|
|INACTIVE=-1|新用户账户密码在过期后不会被禁用|
|EXPIRE=|新用户账户未设置过期日期|
|SHELL=/bin/bash|新用户账户将bash shell作为默认shell|
|SKEL=/etc/skel|系统会将/etc/skel目录下的内容复制到用户的HOME目录下|
|CREATE_MAIL_SPOOL=yes|系统会该用户账户在mail目录下创建一个用于接受邮件的文件|

### 新增用户

|选项|用途|
|---|----|
||默认不会创建HOME目录|
|-m|创建HOME目录|
|-c comment|给新用户添加备注|
|-d home_dir|为主目录指定一个名字（如果不想用登录名作为主目录名的话）|
|-e expire_date|用YYYY-MM-DD格式指定一个账户过期的日期|
|-f inactive_days|指定这个账户密码过期后多少天这个账户被禁用，0表示密码已过期就禁用，1表示禁用这个功能|
|-g initial_group|指定用户登录组的GID或组名|
|-G group ...|指定用户除登录组之外所属的一个或多个附加组|
|-k|必须和-m一起使用，将/etc/skel目录的内容复制到用户的HOME目录|
|-M|不创建用户的HOME目录（当默认设置里要求创建时才使用这个选项）|
|-n|创建一个与用户登录名同名的新组|
|-r|创建系统账户|
|-p passwd|为用户账户指定默认密码|
|-s shell|指定默认的登录shell|
|-u uid|为账户指定唯一的UID|

```bash
[root@server-test-211 home]# useradd -m das -c dasheng

[root@server-test-211 home]# ll
total 4
drwx------.  3 das      das     78 May 22 10:30 das
drwxr-x---. 14 do       rd    4096 May 10 16:05 do


[root@server-test-211 das]# ls -al
total 12
drwx------. 3 das  das   78 May 22 10:30 .
drwxr-xr-x. 9 root root  89 May 22 10:30 ..
-rw-r--r--. 1 das  das   18 Aug  3  2016 .bash_logout
-rw-r--r--. 1 das  das  193 Aug  3  2016 .bash_profile
-rw-r--r--. 1 das  das  231 Aug  3  2016 .bashrc
drwxr-xr-x. 4 das  das   39 May 10 12:14 .mozilla

```

## 修改用户

### 修改用户账户 - `usermod`

包含`useradd`的指令，同时具备以下选项
|选项|用途|
|---|---|
|-l|修改用户账户的登录名|
|-L|锁定账户，使用户无法登录|
|-p|修改账户的密码|
|-U|解除锁定，使用户可以登录|

```bash
[root@server-test-211 home]# usermod -L das

```

### 修改用户密码 - `passwd`

```bash
[root@server-test-211 home]# passwd das
Changing password for user das.
New password: 
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password: 
passwd: all authentication tokens updated successfully.

```

### 查询登录名密码对并修改密码 - `chpasswd`

可批量修改账户密码，输入内容格式: userid:passwd

```bash
# 新建users.txt文件
[root@server-test-211 home]# touch users.txt

# 添加用户账户密码对
[root@server-test-211 home]# vi users.txt 

das:12345678

# 使用chpasswd批量修改
[root@server-test-211 home]# chpasswd < users.txt
```

### 修改密码过期日期 - `chage`

|选项|用途|
|---|---|
|-d|设置上次修改密码到现在的天数|
|-E|设置密码过期的日期|
|-r|设置密码过期到锁定账户的天数|
|-m|设置修改密码之间最少要多少天|
|-w|设置密码过期前多久开始出现提醒信息|

```bash
[root@server-test-211 home]# chage -E '2019-06-07' das
```

### 修改用户账户备注信息 - `chfn`

```bash
[root@server-test-211 home]# chfn das
Changing finger information for das.
Name [dasheng]: dasheng
Office []: ob
Office Phone []: 111
Home Phone []: 111

Finger information changed.


[root@server-test-211 home]# grep das /etc/passwd
das:x:1005:1005:dasheng,ob,111,111:/home/das:/bin/bash
```

### 修改用户账户默认登录shell - `chsh`

```bash
[root@server-test-211 home]# chsh -s /bin/csh das

```

## 删除用户 - `userdel`

|选项|用途|
|----|-----|
| |默认只删除/etc/passwd文件中的用户信息，不会删除系统中输入该账户的任务文件|
|-r|删除用户的HOME目录以及邮件目录|

```bash
[root@server-test-211 das]# userdel -r das

[root@server-test-211 home]# ll
total 4
drwxr-x---. 14 do       rd    4096 May 10 16:05 do
```