# Linux 系统服务管理

#### chkconfig 服务管理工具

> CentOS6 的管理工具
>
> 预设服务 /etc/init.d

###### 系统服务控制

`service 服务名 start|stop|restart`
这里的服务名就是/etc/init.d/目录下的这些文件了。

###### 所有的服务和级别的开启状态

`chkconfig --list`

```shell
[root@localhost init.d]# chkconfig --list

注意：该输出结果只显示 SysV 服务，并不包含原生 systemd 服务。SysV 配置数据可能被原生 systemd 配置覆盖。 
      如果您想列出 systemd 服务,请执行 'systemctl list-unit-files'。
      欲查看对特定 target 启用的服务请执行
      'systemctl list-dependencies [target]'。

netconsole      0:关 1:关 2:关 3:关 4:关 5:关 6:关
network         0:关 1:关 2:开 3:开 4:开 5:开 6:关
nginx           0:关 1:关 2:开 3:开 4:开 5:开 6:关
```

###### 更改某级别下的开启状态

```shell
chkconfig --level 3 network off
chkconfig --list|grep network
这里用–level指定级别，后面是服务名，然后是off或者on。选项–level后面还可以指定多个级别

chkconfig --level 345 network off
另外还可以省略级别，默认是针对级别2、3、4和5操作的。

chkconfig network on
chkconfig还有一个功能，就是可以把某个服务加入系统服务或者删除。

chkconfig --add network
chkconfig --del network
```



#### systemd服务管理

> CentOS7 的管理工具
>
> 支持多个服务并发启动   启动方式更快
>
> 服务对应的脚本 /usr/lib/systemd/system/

```shell
systemctl enable crond.service #让某个服务开机启动（.service可以省略）
systemctl disable crond.service #不让开机启动
systemctl status crond.service #查看服务状态
systemctl start crond.service #启动某个服务
systemctl stop crond.service #停止某个服务
systemctl restart crond.service #重启某个服务
systemctl is-enabled crond #查看某个服务是否开机启动
```

