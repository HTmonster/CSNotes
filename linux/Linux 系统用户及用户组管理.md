# Linux 系统用户及用户组管理

#### 账号管理文件

##### 用户管理

- **passwd文件**

  ```shell
  root:x:0:0:root:/root:/bin/bash
  bin:x:1:1:bin:/bin:/sbin/nologin
  daemon:x:2:2:daemon:/sbin:/sbin/nologin
  adm:x:3:4:adm:/var/adm:/sbin/nologin
  lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
  sync:x:5:0:sync:/sbin:/bin/sync
  shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
  
  # ：分隔为7个字段
  用户名：口令[某些 加密后]：用户标识符uid：组织标识符gid:注释性描述：主目录：启动进程
  
  #uid [0-65536] 0:root 1-99:系统保留 100-：普通用户
  ```

- **shadow文件**

  ```shell
  root:*LOCK*:14600::::::
  bin:*:15513:0:99999:7:::
  daemon:*:15513:0:99999:7:::
  adm:*:15513:0:99999:7:::
  lp:*:15513:0:99999:7:::
  
  #: 分隔为9个字段
  
  用户名：密码：lastcg：min：max：warn：expire:flag
  
  
  #密码  *：用户有效但是不能登录
  #lastcg: 距离上次修改密码的间隔天数
  #min: 两次更改密码的最短时间
  #max: 下次一定要更改的间隔时间
  #warn: 口令失效前多久提醒
  #expire： 账号的什么周期
  #flag: 留作拓展
  ```

##### 用户群组管理

- **/etc/group文件**
- **/etc/gshadow文件**



#### 用户/用户组管理

##### 新增用户组

```shell
语法: groupadd [-g GID] groupname

[root@mono azureuser]# groupadd grptest1
[root@mono azureuser]# tail -n1 /etc/group
grptest1:x:503:
```

##### 删除组

```shell
命令: groupdel
[root@mono azureuser]# groupdel grptest2
[root@mono azureuser]# tail -n3 /etc/group
testgroup:x:501:
user1:x:502:
grptest1:x:503:
#这个命令没有特殊选项，但有一种情况不能删除组：用户组中还包含有用户
```

##### 增加用户

```shell
语法: useradd [-u UID] [-g GID] [-d HOME] [-M] [-s]
‘-u’自定义UID
‘-g’使其属于已经存在的某个组，后面可以跟组id, 也可以跟组名
‘-d’自定义用户的家目录
‘-M’不建立家目录
‘-s’自定义shell

[root@mono azureuser]# useradd test1
[root@mono azureuser]# tail -n1 /etc/passwd
test1:x:502:504::/home/test1:/bin/bash
[root@mono azureuser]# tail -n1 /etc/group
test1:x:504:
#‘useradd’不加任何选项直接跟用户名，则会创建一个跟用户名同样名字的组。
```

##### 删除用户

```shell
语法: userdel [-r] username
[root@mono azureuser]# ls -ld /home/user12
drwx------. 2 user12 grptest1 4096 Aug 7 23:45 /home/user12
[root@mono azureuser]# userdel user12
[root@mono azureuser]# ls -ld /home/user12
drwx------. 2 511 grptest1 4096 Aug 7 23:45 /home/user12
#‘-r’选项的作用只有一个，就是删除账户的时候连带账户的家目录一起删除。
```



#### 用户密码管理

```shell
语法: passwd [username]
```



#### 用户身份切换

```shell
 su [-] username
#后面可以跟‘-‘也可以不跟，普通用户su 不加username 时就是切换到root 用户，当然root 用户同样可以su 到普通用户。’-‘这个字符的作用是，加上后会初始化当前用户的各种环境变量

sudo
```

