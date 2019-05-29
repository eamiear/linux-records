# 目录管理

## 创建目录 - `mkdir`

```bash
[root@server-test-211 kz]# mkdir user

[root@server-test-211 kz]# ls
admin.html  index.html  test  test.html  user

```

## 删除目录 - `rmdir` | `rm`

### `rmdir` 只能删除空目录

```bash
# 删除空目录
[root@server-test-211 kz]# rmdir user
[root@server-test-211 kz]#
```

```bash
# 删除非空目录
[root@server-test-211 kz]# rmdir test
rmdir: failed to remove ‘test’: Directory not empty
[root@server-test-211 kz]#

```

### `rm` 删除目录文件

| 选项 | 用途 |
|:-------|:-----|
| -r/-R | 递归删除|
| -f | 强制删除|

```bash
[root@server-test-211 kz]# rm -rf user

[root@server-test-211 kz]# ls
admin.html  index.html  test  test.html

```