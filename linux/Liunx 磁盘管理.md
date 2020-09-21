# Liunx 磁盘管理

#### 查看磁盘属性信息

##### 检查磁盘占用信息情况

```shell
df
-a 显示所有文件系统的磁盘使用情况，包括0 块（block）的文件系统，如/proc 文件系
统。
-k 以k 字节为单位显示。
-i 显示i 节点信息，而不是磁盘块。
-t 显示各指定类型的文件系统的磁盘空间使用情况。
-x 列出不是某一指定类型文件系统的磁盘空间使用情况（与t 选项相反）。
-T 显示文件系统类型。

[azureuser@mono ~]$ sudo df
Filesystem   1K-blocks     Used     Available Use% Mounted on
/dev/sda1     29954008     5015480 23416916   18%  /
tmpfs         794380       16       794364     1%  /dev/shm
/dev/sdb1     72246600     184084   68392604   1%  /mnt/resource
```

##### 查看某个文件/目录所占用的空间大小

```shell
“du”用来查看某个目录或文件所占空间大小.
语法: du [-abckmsh] [文件或者目录名]
它的参数如下：
-s 对每个Names 参数只给出占用的数据块总数。
-a 递归地显示指定目录中各文件及子孙目录中各文件占用的数据块数。若既不指定-s，也不指定-a，则只显示Names 中的每一个目录及其中的各子目录所占的磁盘块数。
-b 以字节为单位列出磁盘空间使用情况（系统缺省以k 字节为单位）。
-k 以1024 字节为单位列出磁盘空间使用情况。
-c 最后再加上一个总计（系统缺省设置）。
-l 计算所有的文件大小，对硬链接文件，则计算多次。
-x 跳过在不同文件系统上的目录不予统计。
-h 系统自动调节单位，例如文件太小可能就几K，那么就以K 为单位显示，如果大到几G，则就以G 为单位显示。
通常习惯用du -sh filename 这样的形式：

azureuser@mono ~]$ du -sh
8.1M .
[azureuser@mono ~]$ du -h
2.0M ./RxDemo/lib
2.1M ./RxDemo
3.7M ./QuartzDemo
1.1M ./RazorDemo
4.0K ./.mono/registry/CurrentUser
8.0K ./.mono/registry
12K ./.mono
64K ./wcf/TestService
44K ./wcf/TestClient
112K ./wcf
1.1M ./BddifySamples
80K ./NPinyin
8.1M .
```



#### 磁盘分区

```shell
语法: fdisk [-l ] [设备名称] 选项只有一个。
“-l”后边不跟设备名会直接列出系统中所有的磁盘设备以及分区表，加上设备名会列出该
设备的分区表。

[azureuser@mono ~]$ sudo fdisk -l
Disk /dev/sda: 32.2 GB, 32212254720 bytes
255 heads, 63 sectors/track, 3916 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x00072ca8
Device Boot Start End Blocks Id System
/dev/sda1 * 1 3789 30432256 83 Linux
/dev/sda2 3789 3917 1024000 82 Linux swap / Solaris
Disk /dev/sdb: 75.2 GB, 75161927680 bytes
255 heads, 63 sectors/track, 9137 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xf2e41048
Device Boot Start End Blocks Id System
/dev/sdb1 * 1 9138 73398272 83 Linux
```



#### 磁盘格式化

```shell
命令: mke2fs, mkfs.ext2, mkfs.ext3, mkfs.ext4
当用man 查询这四个命令的帮助文档时，您会发现我们看到了同一个帮助文档，这说明四
个命令是一样的。mke2fs 常用的选项有：
‘-b’分区时设置每个数据区块占用空间大小，目前支持1024, 3576 以及4376 bytes 每个
块。
‘-i’设置inode 的大小
‘-N’设置inode 数量，有时使用默认的inode 数不够用，所以要自定设置inode 数量。
‘-c’在格式化前先检测一下磁盘是否有问题，加上这个选项后会非常慢
‘-L’默认该分区的标签label
‘-j’建立ext3 格式的分区，如果使用mkfs.ext3 就不用加这个选项了
‘-t’用来指定什么类型的文件系统，可以是ext2, ext3 也可以是ext4.
```



#### 挂载文件系统

```shell
[1]命令: mount
如果不加任何选项，直接运行“mount”命令，会显示如下信息

[azureuser@mono ~]$ mount

[2]修改/etc/fstab
```

