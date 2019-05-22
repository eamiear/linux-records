# 创建简单 `shell` 脚本

## 创建 `test.sh` 文件

```bash
[root@server-test-211 kz]# touch  test.sh

[root@server-test-211 kz]# vi  test.sh
```

## 文件指定脚本执行的 `shell`

执行 `bash shell`执行脚本

```bash
[root@server-test-211 kz]# vi  test.sh

#!/bin/bash
```

## 写入脚本内容

这里输出一个简单字符串

```bash
[root@server-test-211 kz]# vi  test.sh

#!/bin/bash

echo This is a test

```

## 执行脚本

```bash
[root@server-test-211 kz]# ./test.sh
This is a test
```

## 报无权限问题处理

```bash
[root@server-test-211 kz]# chmod u+x test.sh

```