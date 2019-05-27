# 退出脚本

## 查看退出状态码 - `$?`

> Linux 通过变量 `$?` 来保存上个已执行命令的退出状态码，退出状态值范围： 0 ~ 255

|状态码|描述|
|-----|----|
|0|命令成功结束|
|1|一般性未知错误|
|2|不适合的 shell 命令|
|126|命令不可执行|
|127|没找到命令|
|128|无效的退出参数|
|128+x|与Linux信号x相关的严重错误|
|130|通过Ctrl + C 终止的命令|
|255|正常方位之外的退出状态码|

```bash
# 正常执行
[root@server-test-211 kz]# date
Mon May 27 10:08:26 CST 2019
[root@server-test-211 kz]# echo $?
0

```

```bash
# 不存在的命令
[root@server-test-211 kz]# iuse -h
bash: iuse: command not found...
[root@server-test-211 kz]# echo $?
127

```

```bash
# Ctrl + C 强制退出
[root@server-test-211 kz]# cat
^C
[root@server-test-211 kz]# echo $?
130
```

## `exit` 退出命令

> 通过 `exit` 命令，可以在脚本结束时指定一个退出状态码

```bash
[root@server-test-211 kz]# vi test.sh 

#!/bin/bash

var1=10
var2=20

echo var1 + var2 = $[var1+var2]

exit 3

[root@server-test-211 kz]# ./test.sh
var1 + var2 = 30

[root@server-test-211 kz]# ./test.sh
var1 + var2 = 30

```