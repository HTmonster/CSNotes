 linux命令  常用

1. **tar**命令

  > - -c : 建立一个压缩文件
  > - -x: 解开一个压缩文件
  > - -t: 查看压缩文件
  > - -z: 是否gzip属性 ，是否需要gzip压缩
  > - -j: 是否bzip2属性，是否需要bzip2压缩
  > - -v: 压缩过程中显示文件
  > - -f: 使用档名   后面立即跟
  > - -p: 使用文件的原来属性
  > - -P：使用绝对路径压缩
  > - -N: 比日期新的才会被压缩
  > - -exclude FILE:  不要打包FILE文件

   ```shell
  # 案例一  将 /etc下的文件全部打包为 /tmp/etc.tar
  
  tar -cvf /tmp/etc.tar  /etc   #仅打包
  tar -zcvf /tmp/etc.tar  /etc   #gzip打包压缩
  tar -jcvf /tmp/etc.tar  /etc   #bzip2打包压缩
  
  # 案例二  查阅/tmp/etc.tar.gz中有哪些文件 
  tar -ztvf /tmp/etc.tar.gz
  
  # 案例三 将/tmp/etc.tar.gz 解压缩到 /usr/local/src下
  cd /usr/local/src
  tar -zxvf /tmp/etc.tar.gz
  
  # 案例四  在/tmp 目录下 只将/tmp/etc.tar.gz 内的etc/passwd解开
  cd /tmp
  tar -zxvf /tmp/etc.tar.gz etc/passwd
  
  # 案例五 将/etc内的所有文件备份下来 并且保持权限
  tar -czvpf  /tmp/etc.tar.gz /etc
  
  # 案例六 在/home目录中  比2019.3.1新的备份
  tar -N "2019/03/01" -zcvf home.tar.gz /home
  
  # 案例七 要备份/home /etc  但是不要 /home/dmtsai
  tar -exclude /home/dmtsai -zcvf /home/*/etc
   ```

2. **grep**命令

   `grep [-acinv]  [--color=auto]  'string' filename`

   > - -a : 将binary文件以text文件方式搜索
   > - -A：显示该列和该列之后的内容
   > - -b: 标识出该列的第一个字符的位编号
   > - -B：显示该列和之前的内容
   > - -c：计算找到的次数
   > - -C：显示该列和该列前后的内容
   > - -d: 指定查找目录而不是文件时候使用这个参数
   > - -i: 忽略大小写
   > - -n:顺序输出行号
   > - -r: 递归查询
   > - -v: 方向 （即选出没有字符串的哪一行）
   > - --color=auto : 加颜色

   ```shell
      #案例 将/etc/passwd 有出现root的行取出
     	 grep root /etc/passwd
   
       #案例 在文件中查找字符串（不区分大小写）
       grep -i "str" demo_file
   
       #案例 输出匹配的行及之后的三行
       grep -A 3 -i "str" demo_file
   
       #案例 在一个文件夹中递归查询包含指定字符串的文件
       grep -r "str" *
   ```

3. **find**命令

   `find [OPTION][起始路径][条件][处理动作]`

   > OPTION: 处理符号连接
   >
   > -H: 除了处理命令行参数外，不跟随其他符号连接
   >
   > -L: 跟随所有符号连接
   >
   > -P: 不跟随符号连接  【默认】
   >
   > 
   >
   > 条件：
   >
   > （一）：通过文件名字
   >
   > -name:  按照名称查找
   >
   > -iname: 不区分名字大小写
   >
   > -regex : 基于正则表达式搜索  《匹配整个路径》
   >
   > （二）：通过文件从属关系
   >
   > -user USERNAME: 查找指定用户的所有文件
   >
   > -group GRPNAME: 查找指定组的所有文件
   >
   > -uid UID: 指定UID的所有文件
   >
   > -gid GID:指定GID的所有文件
   >
   > -nouser:没有属主的文件
   >
   > -nogroup:没有属组的文件
   >
   > （三）：根据文件类型
   >
   > -type: [f:普通文件 d:目录文件  I:符号链接文件  b:块设备文件  c: 字符设备文件  p:管道文件  s:套接字文件]
   >
   > （四）：根据文件大小
   >
   > -size[+|-]#UNIT    k,M,G
   >
   >    \# UNIT (UNIT-1,UNIT)
   >
   >    \# UNIT  [0,         UNIT-1]
   >
   >    \# UNIT  [UNIT,    oo]
   >
   > （五）：根据时间戳
   >
   > -atime [+|-]#: 文件最后访问时间  -amin：以分组为单位
   >
   > -mtime [+|-]#: 文件最后修改时间 -min:以分钟为单位
   >
   > -ctime  [+|-]#: 文件最后改变时间 -ctime:以分钟为单位
   >
   > -daystart: 时间条件的开始先决条件
   >
   > （六）：根据权限查找
   >
   > -perm [/|-] mode:   1.mode 精确匹配  2./mode 只要一组用户匹配到一个权限  3.  -mode 并且的关系
   >
   > 处理动作：
   >
   > -ptint: 输出到标准输出  【默认】
   >
   > -ls: 列出文件详细信息
   >
   > -delete: 删除
   >
   > -fls: 长文件格式信息保存到指定文件中
   >
   > -ok COMMAND {} \;   对每个文件执行命令 需要用户进行确认
   >
   > -exec COMMAND {} \;   对每个文件进行执行命令

   ```shell
   #查找指定文件名的文件(不区分大小写)
   $ find -iname "MyProgram.c"
   
   #对找到的文件执行某个命令
   $ find -iname "MyProgram.c" -exec md5sum {} \;
   
   #查找home目录下的所有空文件
   $ find ~ -empty
   ```

4. **ssh**命令

   ```shell
   #登录到远程主机
   $ ssh -l jsmith remotehost.example.com
   
   #调试ssh客户端
   $ ssh -v -l jsmith remotehost.example.com
   
   #显示ssh客户端版本
   $ ssh -V
   ```

5. **sed**命令

   > https://www.cnblogs.com/ctaixw/p/5860221.html

   - sed是非交互式编辑器。不会修改文件，除非shell重定。默认情况下，打印到屏幕。
   - sed编辑器逐行处理文件（或输入），并将结果发送到屏幕。
   - 具体过程如下：
     1. 当前正在处理的行保存在一个临时缓存区中（也称为模式空间）;
     2. 处理临时缓冲区中的行;
     3. 完成后把该行发送到屏幕上。
     4. 处理完一行就将其从临时缓冲区删除，然后将下一行读入，进行处理和显示。
     5. 处理完输入文件的最后一行后，sed便结束运行。
     6. sed把每一行都存在临时缓冲区中，对这个副本进行编辑，所以不会修改原文件。

   命令格式：` sed [option] 'sed command' file'`

   脚本格式：`sed [option] -f 'sed script' flie`

   > option
   >
   > - -n: 只打印模式匹配的行
   > - -e: 直接在命令行模式上进行sed动作  【默认】
   > - -f: 脚本
   > - -r: 支持拓展表达式
   > - -i: 直接修改文件内容
   >
   > 查询方式
   >
   > 1）使用行号
   >
   > | x                 | x为行号                      |
   > | ----------------- | ---------------------------- |
   > | x,y               | 表示行号从x到y               |
   > | /pattern          | 查询包含模式的行             |
   > | /pattern /pattern | 查询包含两个模式的行         |
   > | pattern/,x        | 在给定行号上查询包含模式的行 |
   > | x,/pattern/       | 通过行号和模式查询匹配的行   |
   > | x,y!              | 查询不包含指定行号x和y的行   |
   >
   > 2)使用正则表达式
   >
   > 
   >
   > 编辑命令  sed command
   >
   > | p          | 打印匹配行（和-n选项一起合用）                               |
   > | ---------- | ------------------------------------------------------------ |
   > | =          | 显示文件行号                                                 |
   > | a\         | 在定位行号后附加新文本信息                                   |
   > | i\         | 在定位行号后插入新文本信息                                   |
   > | d          | 删除定位行                                                   |
   > | c\         | 用新文本替换定位文本                                         |
   > | w filename | 写文本到一个文件，类似输出重定向 >                           |
   > | r filename | 从另一个文件中读文本，类似输入重定向 <                       |
   > | s          | 使用替换模式替换相应模式                                     |
   > | q          | 第一个模式匹配完成后退出或立即退出                           |
   > | l          | 显示与八进制ACSII代码等价的控制符                            |
   > | {}         | 在定位行执行的命令组，用分号隔开                             |
   > | n          | 从另一个文件中读文本下一行，并从下一条命令而不是第一条命令开始对其的处理 |
   > | N          | 在数据流中添加下一行以创建用于处理的多行组                   |
   > | g          | 将模式2粘贴到/pattern n/                                     |
   > | y          | 传送字符，替换单个字符                                       |

   ```shell
   # 打印三行
   sed -n '3p' filename
   
   # 打印100到300行的
   sed  -n '100,300' filename
   
   # 过滤掉#开头还有空格的行
   sed -n '/^#/ !{/^$/!p}' filename
   
   # 删除文件中所有#开头的注释行
   sed  '/^#/ d' filename
   
   # 在nihao 的行后附加 haha
   sed '/nihao/a haha' filename
   
   # 在nihao 的行后下一行 haha
   sed '/nihao/i haha' filename
   ```

6. **awk**命令

   - 文本分析工具
   - grep 查找 sed编辑 awk数据分析生成报告
   - 分行读入  空格分行切片
   - 脚本使用的多

   `awk '{pattern+action} filename'`

   -  pattern : 查找的内容  

   - ation: 匹配后的工作

     | 条件类型   | 条 件                                                     | 说 明                                                        |
     | ---------- | --------------------------------------------------------- | ------------------------------------------------------------ |
     | awk保留字  | BEGIN                                                     | 在 awk 程序一开始，尚未读取任何数据之前执行。BEGIN 后的动作只在程序开始时执行一次 |
     | awk保留字  | END                                                       | 在 awk 程序处理完所有数据，即将结束时执行?END 后的动作只在程序结束时执行一次 |
     | 关系运算符 | >                                                         | 大于                                                         |
     | <          | 小于                                                      |                                                              |
     | >=         | 大于等于                                                  |                                                              |
     | <=         | 小于等于                                                  |                                                              |
     | ==         | 等于。用于判断两个值是否相等。如果是给变童赋值，则使用"=” |                                                              |
     | !=         | 不等于                                                    |                                                              |
     | A~B        | 判断字符串 A 中是否包含能匹配 B 表达式的子字符串          |                                                              |
     | A!~B       | 判断字符串 A 中是否不包含能匹配 B 表达式的子字符串        |                                                              |
     | 正则表达式 | /正则/                                                    | 如果在“//”中可以写入字符，则也可以支持正则表达式             |

   ```shell
   # 案例  取出最近登录的5个账号
   [root@www ~]# last -n 5 <==仅取出前五行
   root     pts/1   192.168.1.100  Tue Feb 10 11:21   still logged in
   root     pts/1   192.168.1.100  Tue Feb 10 00:46 - 02:28  (01:41)
   root     pts/1   192.168.1.100  Mon Feb  9 11:41 - 18:30  (06:48)
   dmtsai   pts/1   192.168.1.100  Mon Feb  9 11:41 - 11:41  (00:00)
   root     tty1                   Fri Sep  5 14:09 - 14:10  (00:01)
   
   #取出最近登录的5个账号
   #$0:所有域 $1:第一个分隔域  分隔符：空白符
   last -n 5 | awk '{print $1}'
   root
   root
   root
   dmtsai
   root
   
   #案例 显示/etc/passwd的账户
   cat /etc/passwd  |ask -F ':' '{print $1}'
   
   #案例 显示/etc/passwd的账户及shell 其间用tab分隔
   cat /etc/passwd  |ask -F ':' '{print $1 “\t" $7}'
   ```

7. **Vim**

   打开文件并跳到第10行

   ```shell
   $ vim +10 filename.txt
   ```

   打开文件跳到第一个匹配的行

   ```shell
   $ vim +/search-term filename.txt
   ```

   以只读模式打开文件

   ```shell
   $ vim -R /etc/passwd
   ```

8. **diff**

   > 用于比较文件的内容。比较版本改动

   `diff [参数][文件/目录][文件/目录]`

   
