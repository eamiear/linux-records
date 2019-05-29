# 使用变量

> 变量分为环境（系统）变量、用户变量，变量通过美元符号 `$` 进行引用，使用变量时如果没有使用 `$`，变量将当做一个字符串

## 环境变量

```bash
[root@server-test-211 kz]# vi test.sh 

#!/bin/bash

# display user information.

echo This is a test

echo "userid: $USER"

echo UID: $UID

echo HOME: $HOME
```

```bash
# 执行
[root@server-test-211 kz]# ./test.sh
This is a test
userid: root
UID: 0
HOME: /root
```

## 用户变量

```bash
[root@server-test-211 kz]# vi test.sh 

#!/bin/bash

# display user information.

iuse='Linux'
days=30
user='Kat'

echo "$user used $iuse in $days days ago"

user='Ketty'

echo "$user doesn't use $iuse"
```

```bash
# 执行
[root@server-test-211 kz]# ./test.sh
Kat used Linux in 30 days ago
Ketty doesn't use Linux

```

## 命令替换

> 将命令赋值自定义变量

### 反引号字符( ` )

```bash
[root@server-test-211 kz]# vi test.sh 

#!/bin/bash

# display user information.

iDate=`date`

echo "The date and time are: " $iDate
```

```bash
# 执行
[root@server-test-211 kz]# ./test.sh
The date and time are:  Thu May 23 10:37:17 CST 2019
```

### `$()`

```bash
[root@server-test-211 kz]# vi test.sh 

#!/bin/bash

# display user information.

iDate=$(date)

echo "The date and time are: " $iDate
```

```bash
# 执行
[root@server-test-211 kz]# ./test.sh
The date and time are:  Thu May 23 10:37:17 CST 2019
```