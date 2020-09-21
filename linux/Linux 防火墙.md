# Linux 防火墙

> 参考文章
>
> https://blog.51cto.com/sdwaqw/2068774

#### SElinux

> Redhat/CentOS特有安全机制

```shell
[root@localhost /]#  getenforce          //获取当前SELinux状态
Enforcing                                       //开启状态
[root@localhost /]#  setenforce 0       //临时关闭SELinux
[root@localhost /]#  getenforce
Permissive                                    //临时关闭状态
这个仅仅是临时关闭，如果要永久关闭则需要修改配置文件/etc/selinux/config, 把SELINUX=Enforce,改为disabled，修改好之后重启：

[root@localhost /]#  vim /etc/selinux/config 

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled                //修改为disabled
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected. 
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

重启之后查看SELinux状态：
[root@localhost /]# getenforce
Disabled
```

##### netfilter与firewalld

> CentOS7之前netfilter 之后firewalld

```shell
[root@localhost ~]# systemctl stop firewalld //关闭firewalld服务
[root@localhost ~]# systemctl disable firewalld //禁止firewalld服务开机启动
Removed symlink /etc/systemd/system/dbus-org.fedoraproject.FirewallD1.service.
Removed symlink /etc/systemd/system/basic.target.wants/firewalld.service.
[root@localhost ~]# yum install -y iptables-services //安装iptables-services，以便使用iptables
[root@localhost ~]# systemctl enable iptables //开机启动iptables
Created symlink from /etc/systemd/system/basic.target.wants/iptables.service to /usr/lib/systemd/system/iptables.service.
[root@localhost ~]#systemctl start iptables //启动iptables
```

##### iptables

> 常用的防火墙软件 netilter项目的一部分

###### 命令语法

iptables [选项]【参数】

###### 选项

-t<表>：指定要操纵的表；
-A：向规则链中添加条目；
-D：从规则链中删除条目；
-i：向规则链中插入条目；
-R：替换规则链中的条目；
-L：显示规则链中已有的条目；
-F：清楚规则链中已有的条目；
-Z：清空规则链中的数据包计算器和字节计数器；
-N：创建新的用户自定义规则链；
-P：定义规则链中的默认目标；
-h：显示帮助信息；
-p：指定要匹配的数据包协议类型；
-s：指定要匹配的数据包源ip地址；
-j<目标>：指定要跳转的目标；
-i<网络接口>：指定数据包进入本机的网络接口；
-o<网络接口>：指定数据包要离开本机所使用的网络接口。

###### iptables命令选项输入顺序：

iptables -t 表名 <-A/I/D/R> 规则链名 [规则号] <-i/o 网卡名> -p 协议名 <-s 源IP/源子网> --sport 源端口 <-d 目标IP/目标子网> --dport 目标端口 -j 动作

###### 表名包括：

raw：高级功能，如：网址过滤。
mangle：数据包修改（QOS），用于实现服务质量。
net：地址转换，用于网关路由器。
filter：包过滤，用于防火墙规则。

###### 规则链名包括：

INPUT链：处理输入数据包。
OUTPUT链：处理输出数据包。
PORWARD链：处理转发数据包。
PREROUTING链：用于目标地址转换（DNAT）。
POSTOUTING链：用于源地址转换（SNAT）。

###### 动作包括：

accept：接收数据包。
DROP：丢弃数据包。
REDIRECT：重定向、映射、透明代理。
SNAT：源地址转换。
DNAT：目标地址转换。
MASQUERADE：IP伪装（NAT），用于ADSL。
LOG：日志记录。

###### 案例

清除已有iptables规则

iptables -F
iptables -X
iptables -Z

查看已添加的iptables规则
iptables -NVL

将所有iptables以序号标记显示，执行：

iptables -L -n --line-numbers
比如要删除INPUT里序号为8的规则，执行：

iptables -D INPUT 8

