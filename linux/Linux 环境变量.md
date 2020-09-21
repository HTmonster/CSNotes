# Linux 环境变量

#### 环境变量分类

- **系统环境变量**
  - 对所有用户起作用
- **用户环境变量**
  - 对当前用户起作用



#### 环境变量存储

- 系统环境变量

  ```shell
  /etc/profile   #系统为每个用户设置环境信息     【用户第一次登录时候执行】
  /etc/bashrc    #为每一个 bash shell用户
  ```

- 用户环境变量

  ```shell
  ~/.bash_profile #每个用户专属的shell 信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc 文件.
  ~/.bashrc #该文件包含专用于你的bash shell 的bash 信息,当登录时以及每次打开新的shell 时,该该文件被读取.
  ~/.bash_logout  #当每次退出系统(退出bash shell)时,执行该文件。
  ```



#### 定制环境变量

##### 显示环境变量

- 显示一个变量
  - echo $PATH
- 显示所有变量
  - env

**设置环境变量**

```shell
[azureuser@mono tmp]$ export NAME="geffzhang"
[azureuser@mono tmp]$ echo $NAME
Geffzhang
# 重回系统需要重置
# 持久的方法 修改配置文件
```

##### 显示本地定义的shell变量

```shel
set
BASH=/bin/bash
BASHOPTS=checkwinsize:cmdhist:expand_aliases:extquote:force_fignore:hostcomplete:interactiv
e_comments:login_shell:progcomp:promptvars:sourcepath
BASH_ALIASES=()
BASH_ARGC=()
BASH_ARGV=()
BASH_CMDS=()
BASH_LINENO=()
BASH_SOURCE=()
```

##### 清除环境变量

```shell
[azureuser@mono tmp]$ unset NAME
```





