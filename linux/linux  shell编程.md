# linux  shell编程

#### bash特点

> bash是Redhat/CentOS系统默认安装的shell

##### 1. 记录命令历史

- 命令记录在home目录下的.bash_history文件中（正常退出才保存）

###### 分类

```shell
[1]    !!      #上条命令
[2]    ！n     #执行历史命令的第n条
[3]    !xx     #最近执行的xx命令
```

##### 2. 指令和文件名补全

- tab键

##### 3. 别名

- 可以把一个很长的指令变为一个其他的标记

  ```shell
  alias [命令别名]=['具体的命令']   #别名
  unalias [别名]                  #解除别名
  ```

##### 4. 通配符

- \* 匹配0个或多个字符
- ？匹配一个字符

##### 5. 输入输出重定向

```shell
>  输出重定向
<  输入重定向
>> 追加输入
2> 错误重定向
```

##### 6. 管道操作

- |符号

##### 7. 作业控制

- Ctrl+Z  暂停一个进程  （fg命令恢复）（bg后台执行）
- Ctrl+C 停止进程





#### shell特殊符号

| 符号         | 意义                              |
| ------------ | --------------------------------- |
| \            | 脱意字符 将特殊符号转化为普通字符 |
| ；           | 一行中运行多个命令                |
| ~            | 用户的家目录                      |
| &            | 把命令放在后台执行                |
| \> >> 2> 2>> | 重定向符号                        |
| []           | 中间字符任意一个                  |
| && \|\|      | 多条命令中间的特殊符号            |



#### shell本地变量

- 字母或数字 不能数字开头

- 中间不能有空格 可以有下划线__

- 不能使用标点符号  不能使用关键字

  ```shell
  name=value
  
  #引用使用$name
  
  #一般使用情况
  d=`date +%H:%M:%S`
  echo "The script begin at $d."
  echo "We'll sleep 4 secondes"
  sleep 4
  d1=`date +%H:%M:%S`
  echo "The script end date $d1.
  
  #获取用户的输入
  read -p "Please input a number:" x
  read -p "Please input a number:" y
  sum=$[$x+$y]
  echo "The sum of two numbers is: $sum"
  ```

  

#### shell 控制结构

##### if判断

```shell
if condition; then
	statements
else
	statements
fi
```

##### 循环结构

```shell
#! /bin/bash

#for 循环结构
for x in one two three four
do
	echo number $x
done

#while 循环结构
while [ condition ]
do
	statements
done

#until 循环结构
until [ condition]
do
	statement
done

# break 命令不执行当前循环体内break 下面的语句从当前循环退出.
# continue 命令是程序在本循体内忽略下面的语句,从循环头开始执行
```



#### shell函数

```shell
function my_funcname
{
	code block
}

#或者
my_funcname() {
	code block
}

#参数引用  $1  $2
#返回值 retrun  $?
```

