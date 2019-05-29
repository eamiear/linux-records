# 磁盘管理

## 查看磁盘空间状态 - `df`

| 选项 | 用途 |
|:-------|:-----|
|  | 显示磁盘使用状态 |
| -h | 以易于阅读的方式显示|

```bash
[root@server-test-211 kz]# df
Filesystem          1K-blocks    Used Available Use% Mounted on
/dev/mapper/cl-root 294984984 7079236 287905748   3% /
devtmpfs              3933336       0   3933336   0% /dev
tmpfs                 3949516     124   3949392   1% /dev/shm
tmpfs                 3949516   17768   3931748   1% /run
tmpfs                 3949516       0   3949516   0% /sys/fs/cgroup
/dev/sda1             1038336  177812    860524  18% /boot
tmpfs                  789904      16    789888   1% /run/user/42
tmpfs                  789904       0    789904   0% /run/user/0

```

```bash
[root@server-test-211 kz]# df -h
Filesystem           Size  Used Avail Use% Mounted on
/dev/mapper/cl-root  282G  6.8G  275G   3% /
devtmpfs             3.8G     0  3.8G   0% /dev
tmpfs                3.8G  124K  3.8G   1% /dev/shm
tmpfs                3.8G   18M  3.8G   1% /run
tmpfs                3.8G     0  3.8G   0% /sys/fs/cgroup
/dev/sda1           1014M  174M  841M  18% /boot
tmpfs                772M   16K  772M   1% /run/user/42
tmpfs                772M     0  772M   0% /run/user/0
```

## 查看特定目录磁盘使用情况 - `du`

| 选项 | 用途 |
|:-------|:-----|
|  | 显示当前目录磁盘使用状态 |
| -h | 以用户易读的格式显示|
| -c | 显示当前目录所有文件的总大小|
| -s | 显示每个输出参数的总计|

```bash
# 显示磁盘状态
[root@server-test-211 kz]# du
12	./test
20	.

```

```bash
# 显示当前目录耗存大小
[root@server-test-211 kz]# du -c
12	./test
20	.
20	total
```

```bash
# 易读格式显示
[root@server-test-211 kz]# du -h
12K	./test
20K	.

```