# Linux crontab定时任务

> crontab是一个定时执行程序的程序

#### 语法

```shell
crontab [-u user] file

#或
crontab [-u user] {-l|-r|-e}
-e 执行文字编辑器来设定时程表
-r 删除目前的时程表
-l 列出目前的时程表
```



#### 时程表

```shell
f1    f2    f3         f4      f5              program
分钟  小时   月份中天数   月份   一个星期中的天数     执行的程序

#*每次  a-b  从a到b   */n 每隔n个时间间隔   a,b,c表示a,b,c
```



#### 实例

```shell
#每月 每天 每小时 第0分钟 执行/bin/ls
0 * * * * /bin/ls

#在12月内 每天早上的6点到12点  每隔3个小时0分钟 执行/usr/bin/backup
0 6-12/3 * 12 * /usr/bin/backup

#周一到周五每天下午 5:00 寄一封信给 alex@domain.name
0 17 * * 1-5 mail -s "hi" alex@domain.name < /tmp/maildata
```

