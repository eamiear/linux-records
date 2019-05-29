# 数据文件处理

## 数据排序 - `sort`

| 选项 | 用途 |
|:-------|:-----|
|  | 按照指定默认语言的排序规则进行排序，将数字识别为字符 |
|-b --ignore-leading-blanks |排序时忽略起始的空白|
|-C --check=quiet |不排序，如果数据无序也不要报告|
|-c --check |不排序，但检查输入数据是不是已排序；未排序的话，报告|
|-d --dictionary-order |仅考虑空白和字母，不考虑特殊字符|
|-f --ignore-case |默认情况下，会将大写字母排在前面；这个参数会忽略大小写|
|-g --general-number-sort |按通用数值来排序（跟-n不同，把值当浮点数来排序，支持科学计数法表示的值）|
|-i --ignore-nonprinting |在排序时忽略不可打印字符|
|-k --key=POS1[,POS2] |排序从POS1位置开始；如果指定了POS2的话，到POS2位置结束|
|-M --month-sort |用三字符月份名按月份排序|
|-m --merge |将两个已排序数据文件合并|
|-n --numeric-sort |按字符串数值来排序（并不转换为浮点数）|
|-o --output=file |将排序结果写出到指定的文件中|
|-R --random-sort |按随机生成的散列表的键值排序|
|-R--random-source=FILE | 指定-R参数用到的随机字节的源文件|
|-r --reverse |反序排序（升序变成降序）|
|-S --buffer-size=SIZE |指定使用的内存大小|
|-s --stable |禁用最后重排序比较|
|-T --temporary-directory=DIR |指定一个位置来存储临时工作文件|
|-t --field-separator=SEP |指定一个用来区分键位置的字符|
|-u --unique |和-c参数一起使用时，检查严格排序；不和-c参数一起用时,仅输出第一例相似的两行|
|-z --zero-terminated |用NULL字符作为行尾，而不是用换行符|

```bash
[root@server-test-211 kz]# vi index.html

a index file
9
11
2
30
8
cat
five
four
one
```

```bash
# 默认排序
[root@server-test-211 kz]# sort index.html

11
2
30
8
9
a index file
cat
five
four
one

```

```bash
# 按数值排序
[root@server-test-211 kz]# sort -n  index.html

a index file
cat
five
four
one
2
8
9
11

```

## 数据搜索 - `grep`

> `grep [options] pattern [file]`

- `options`: 选项配置
- `pattern`: 字符匹配规则
- `file`:    目标文件

| 选项 | 用途 |
|:-------|:-----|
||默认使用正则表达式匹配模式|
| -v | 反向搜索，输出不匹配该模式的行|
| -n | 显示匹配模式的行所在的行号|
| -c | 含有匹配模式的行的数量|
| -e | 指定多个匹配模式|

```bash
[root@server-test-211 kz]# grep f index.html
a index file
five
four
```

```bash
# 正则表达式
[root@server-test-211 kz]# grep [fc] index.html
a index file
cat
five
four

```

```bash
# 反向查询
[root@server-test-211 kz]# grep -v  [fc0-9] index.html





one
```

```bash
# 显示行号
[root@server-test-211 kz]# grep -vn  [fc0-9] index.html
2:
8:
10:
12:
14:
15:one
```

```bash
# 匹配总数
[root@server-test-211 kz]# grep -vnc  [fc0-9] index.html
6
```

```bash
# 多个匹配规则
[root@server-test-211 kz]# grep -e d -e e  index.html
a index file
five
one
```

## 数据压缩 - `gzip`

> 压缩单个文件

```bash
[root@server-test-211 kz]# gzip test.html
[root@server-test-211 kz]# ll
total 8
-rw-r--r--. 1 root root    0 May 15 16:13 admin.html
-rw-r--r--. 1 root root   48 May 16 11:47 index.html
drwxr-xr-x. 2 root root   65 May 16 13:58 test
-rw-r--r--. 1 root root 1054 May 15 17:37 test.html.gz

```

## 文件解压 - `gunzip`

> 解压单个文件

```bash
[root@server-test-211 kz]# gunzip test.html.gz
```

## 数据归档 - `tar`

> `tar function [option] object1 object2 ...`

`function`

| 选项 | 用途 |
|:-------|:-----|
|-A --concatenate |将一个已有tar归档文件追加到另一个已有tar归档文件|
|-c --create |创建一个新的tar归档文件|
|-d --diff| 检查归档文件和文件系统的不同之处|
|-d --delete |从已有tar归档文件中删除|
|-r --append |追加文件到已有tar归档文件末尾|
|-t --list |列出已有tar归档文件的内容|
|-u --update |将比tar归档文件中已有的同名文件|
|-x --extract |从已有tar归档文件中提取文件|

`option`

| 选项 | 用途 |
|:-------|:-----|
|-C dir |切换到指定目录|
|-f file |输出结果到文件或设备file|
|-j |将输出重定向给bzip2命令来压缩内容|
|-p |保留所有文件权限|
|-v |在处理文件时显示文件|
|-z |将输出重定向给gzip命令来压缩内容|

```bash
# 归档test.html index.html文件到test.rar
[root@server-test-211 kz]# tar -cvf test.rar test.html index.html
test.html
index.html

[root@server-test-211 kz]# ls -l
total 20
-rw-r--r--. 1 root root     0 May 15 16:13 admin.html
-rw-r--r--. 1 root root    48 May 16 11:47 index.html
drwxr-xr-x. 2 root root    56 May 16 14:00 test
-rw-r--r--. 1 root root  2212 May 15 17:37 test.html
-rw-r--r--. 1 root root 10240 May 16 14:10 test.rar
```

```bash
# 归档目录文件到test.rar
[root@server-test-211 kz]# tar -cvf test.rar test/*
test/admin.md
test/index.html
test/index.md

```

```bash
# 查看归档文件test.rar中的内容
[root@server-test-211 kz]# tar -tf test.rar
test/admin.md
test/index.html
test/index.md

```

```bash
# 提取 test-archive.rar 文件
[root@server-test-211 kz]# tar -xvf test-archive.rar
test.html

```