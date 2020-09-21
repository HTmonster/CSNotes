# Linux 监控系统性能

> 参考文章：
>
> https://linuxstory.org/command-line-tools-to-monitor-linux-performance/

#### 系统进程监控

##### top命令

> top 命令
>
> 显示正在运行的实际运行的   更新到列表
>
> [CPU的使用   内存的使用  交换内存  缓存大小 缓冲区大小  过程控制 用户]

`-b 批处理 -c 显示完整的治命令 -I 忽略失效过程-s 保密模式-S 累积模式-i<时间> 设置间隔时间-u<用户名> 指定用户名 -p<进程号> 指定进程 -n<次数> 循环显示的次数`

```shell
[root@TG1704 log]# top

top - 14:06:23 up 70 days, 16:44,  2 users,  load average: 1.25, 1.32, 1.35

Tasks: 206 total,   1 running, 205 sleeping,   0 stopped,   0 zombie

Cpu(s):  5.9%us,  3.4%sy,  0.0%ni, 90.4%id,  0.0%wa,  0.0%hi,  0.2%si,  0.0%st

Mem:  32949016k total, 14411180k used, 18537836k free,   169884k buffers

Swap: 32764556k total,        0k used, 32764556k free,  3612636k cached

  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND                                                                
28894 root      22   0 1501m 405m  10m S 52.2  1.3   2534:16 java                 
18249 root      18   0 3201m 1.9g  11m S 35.9  6.0 569:39.41 java                 2808 root      25   0 3333m 1.0g  11m S 24.3  3.1 526:51.85 java         
25668 root      23   0 3180m 704m  11m S 14.0  2.2 360:44.53 java               574 root        25   0 3168m 611m  10m S 12.6  1.9 556:59.63 java                 1599 root      20   0 3237m 1.9g  11m S 12.3  6.2 262:01.14 java                 
```

##### htop

> 类似top  但是交互更好
>
> 不自带 需要安装

#### 虚拟内存统计

> vmstat 命令
>
> 显示虚拟内存  内核线程  磁盘  系统进程  IO模块  中断 CPU活跃状态等

```shell
<strong># vmstat
procs -----------memory---------- ---swap-- -----io---- --system-- -----cpu-----
 r  b   swpd   free  inact active   si   so    bi    bo   in   cs us sy id wa st
 1  0      0 810420  97380  70628    0    0   115     4   89   79  1  6 90  3  0
```



#### io统计与监控

##### iotop 实时监控磁盘输入输出的进程

- 实时监控

```shell
Total DISK read:       0.00 B/s | Total DISK write:       0.00 B/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    command
    1 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init [3]
    2 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kthreadd]
    3 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [migration/0]
    4 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [ksoftirqd/0]
    5 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [watchdog/0]
    6 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [migration/1]
    7 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [ksoftirqd/1]
    8 rt/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [watchdog/1]
    9 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [events/0]
   10 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [events/1]
   11 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [khelper]
2572 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [bluetooth]
```

##### iostat 输入输出统计

- 收集与展示 统计
- 查找存储设备性能问题【设备 本地磁盘 】

```shell
# iostat
 
Linux 2.6.18-238.9.1.el5 (tecmint.com)         09/13/2012
avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           2.60    3.65    1.04    4.29    0.00   88.42
 
Device:            tps   Blk_read/s   Blk_wrtn/s   Blk_read   Blk_wrtn
cciss/c0d0       17.79       545.80       256.52  855159769  401914750
cciss/c0d0p1      0.00         0.00         0.00       5459       3518
cciss/c0d0p2     16.45       533.97       245.18  836631746  384153384
cciss/c0d0p3      0.63         5.58         3.97    8737650    6215544
cciss/c0d0p4      0.00         0.00         0.00          8          0
cciss/c0d0p5      0.63         3.79         5.03    5936778    7882528
cciss/c0d0p6      0.08         2.46         2.34    3847771    3659776
```



#### 网络监控

##### tcpdump 网络数据包分析

- 捕获和过滤TCP/IP包

```shell
tcpdump -i eth0

tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes
22:08:59.617628 IP tecmint.com.ssh > 115.113.134.3.static-mumbai.vsnl.net.in.28472: P 2532133365:2532133481(116) ack 3561562349 win 9648
22:09:07.653466 IP tecmint.com.ssh > 115.113.134.3.static-mumbai.vsnl.net.in.28472: P 116:232(116) ack 1 win 9648
22:08:59.617916 IP 115.113.134.3.static-mumbai.vsnl.net.in.28472 > tecmint.com.ssh: . ack 116 win 64347
```

##### netstat 网络统计

- 监控数据包传入和传出
- 统计界面  命令行数据

```shell
# netstat -a | more
Active Internet connections (including servers)
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)
tcp        0      0  *.*                    *.*                    CLOSED
tcp4       0      0  *.*                    *.*                    CLOSED
tcp        0      0  *.*                    *.*                    CLOSED
tcp4       0      0  *.*                    *.*                    CLOSED
tcp        0      0  *.*                    *.*                    CLOSED
tcp4       0      0  *.*                    *.*                    CLOSED
tcp4       0      0  loopback.32848         loopback.32849         ESTABLISHED
tcp4       0      0  loopback.32849         loopback.32848         ESTABLISHED
```



#### 显示打开的文件列表

> lsof 命令
>
> 以列表形式此案时打开的文件和进程
>
> 文件 【磁盘文件】【网络套接字】【管道】【设备】【进程】

```shell

# lsof
 
COMMAND     PID      USER   FD      TYPE     DEVICE     SIZE       NODE NAME
init          1      root  cwd       DIR      104,2     4096          2 /
init          1      root  rtd       DIR      104,2     4096          2 /
init          1      root  txt       REG      104,2    38652   17710339 /sbin/init
init          1      root  mem       REG      104,2   129900     196453 /lib/ld-2.5.so
init          1      root  mem       REG      104,2  1693812     196454 /lib/libc-2.5.so
init          1      root  mem       REG      104,2    20668     196479 /lib/libdl-2.5.so
init          1      root  mem       REG      104,2   245376     196419 /lib/libsepol.so.1
init          1      root  mem       REG      104,2    93508     196431 /lib/libselinux.so.1
init          1      root   10u     FIFO       0,17                 953 /dev/initctl
```

