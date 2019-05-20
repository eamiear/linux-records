# 包管理工具 - `yum`

## 查看 `yum` 版本

```bash
[root@server-test-211 kz]# yum --version
3.4.3

```

## 列出已安装包

### 已安装包列表输出到控制台

```bash
[root@server-test-211 kz]# yum list installed
```

### 已安装包列表输出到文件

```bash
[root@server-test-211 kz]# yum list installed > installed_software.txt

```

```bash
[root@server-test-211 kz]# ls -l
total 112
-rw-r--r--. 1 root root      0 May 15 16:13 admin.html
-rw-r--r--. 1 root root     48 May 16 11:47 index.html
-rw-r--r--. 1 root root 104658 May 20 09:54 installed_software.txt

```

### 查看已安装某软件包的详情信息

```bash
[root@server-test-211 kz]# yum list git
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.cn99.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.163.com
Available Packages
git.x86_64
```

## 安装软件

### 在线安装

> `yum install package_name`

```bash
[root@server-test-211 kz]# yum install jenkins
```

### 本地安装

> `yum localinstall package_name.rpm`

下载 `rpm` 安装文件到本机

```bash
[root@server-test-211 kz]# yum localinstall git-2.8.4-1.ep7.x86_64.rpm

```

## 更新软件

### 查看已安装可更新的软件

```bash
[root@server-test-211 kz]# yum list updates

```

### 更新指定的已安装包

> `yum update package_name`

```bash
[root@server-test-211 kz]# yum update git

```

### 更新全部已安装可更新的软件包

```bash
[root@server-test-211 kz]# yum update

```

## 卸载软件

### 删除软件包并保留配置、数据文件

> `yum remove package_name`

```bash
[root@server-test-211 kz]# yum remove git

```

### 删除软件及其所有文件

> `yum erase package_name`

```bash
[root@server-test-211 kz]# yum erase git

```

## 处理损坏的包依赖关系

> 安装多个软件包时，软件包的依赖关系相互覆盖

### 查看包依赖关系

`yum deplist package_name`

```bash
[root@server-test-211 kz]# yum deplist  git
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirrors.cn99.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.163.com
package: git.x86_64 1.8.3.1-20.el7
  dependency: /bin/bash

```

### 清理损坏依赖

```bash
[root@server-test-211 kz]# yum clean all
```