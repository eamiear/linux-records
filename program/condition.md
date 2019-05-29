# 条件语句

### `if-then`语句

使用格式：

```shell
if command
then
    commands
fi
```

或

通过分号，让 `if` 和 `then` 同处一行

```shell
if command; then
  commands
fi
```

与其他编程语言不同，`if`语句后面是一个命令，命令执行结束的退出状态码是 `0`，则执行 `then` 部分的命令。否则， `then` 不执行。
`fi` 语句表示 `if-then` 语句结束。

示例：

```bash
[root@server-test-211 kz]# cat test.sh
#!/bin/bash

if pwd
then
   echo "It worked"
   echo "list pwd files:"
   ls -la
fi
```

```bash
[root@server-test-211 kz]# ./test.sh
/home/kz
It worked
list pwd files:
total 160
drwxr-xr-x. 4 root root    143 May 29 10:27 .
drwxr-xr-x. 9 root root     89 May 22 14:25 ..
drwxr-xr-x. 2 root root     56 May 16 14:00 test
-rwxr--r--. 1 skz  root     88 May 29 10:27 test.sh
```

### `if-then-else` 语句

使用格式：

```shell
if command
then
   commands
else
   commands
fi
```

如果 `if` 的命令退出状态码为 `0`，则执行 `then` 中的命令，否则执行 `else` 中的命令。

示例：

```bash
#!/bin/bash

if !pwd; then 
   echo "It worked"
   echo "list pwd files:"
  
   ls -la
else
   echo "It's a \`else\` part"
fi
```

```bash
[root@server-test-211 kz]# ./test.sh
./test.sh: line 3: !pwd: command not found
It's a `else` part
```

### 多个条件判断

使用格式：

```shell
if command1
then
   commands
elif command2
then
   commands2
fi
```

### 嵌套 `if`

格式：

```shell
if command
then
  if command1
  then
     commands
fi
```

### `test` 命令

`if` 条件只能是 `shell` 命令，如果想将某个变量或非命令退出状态码之外的条件作为条件判断，可以通过 `test` 命令实现。 `test` 命令中的条件成立，返回退出状态码 `0`， 否则返回非零退出状态码。

使用格式：

```shell
test condition
```

或简写格式：

简写模式的条件变量需要通过 `$` 美元符号使用。

```shell
[ condition ]
```

与 `if-then` 结合使用格式：

```shell
if test condition
then
   commands
fi
```

或

```shell
if [ conditoin ]
then
   commands
fi
```

示例：

```bash
[root@server-test-211 kz]# cat test.sh
#!/bin/bash

isValid="yes"

if test isValid
then
   echo "It is valid condition"
fi
```

```bash
[root@server-test-211 kz]# ./test.sh
It is valid condition
```

### test 支持的条件判断类型

* [数值比较](condition_number_compare.md)
* [字符串比较](condition_string_compare.md)
* [文件比较](condition_file_compare.md)