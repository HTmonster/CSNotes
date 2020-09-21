# Linux IO模式及select poll epoll多路复用

> 参考文章：
>
> https://segmentfault.com/a/1190000003063859



#### 文件描述符fd

- 一个用于表述指向文件引用的抽象化概念
- 非负整数
- 索引值  指向内核为每个进程维护的打开文件的记录表



#### 缓存IO(标准IO)

- 将IO的数据缓存在文件系统的页缓存
- **【缺点】**：多次拷贝 开销大



#### IO模式

###### 一次IO访问的过程

1. 等待数据准备
2. 将数据从内核拷贝到进程中

###### IO模式

- **阻塞IO blocking**
  - 默认的所有socket
  - 用户等待数据时候要被阻塞 直至数据完全交付
- **非阻塞IO non-blocking**
  - 用户请求数据 未准备好  返回error
  - 不断询问kernel
- **IO多路复用 multiplexing (event driven io)**
  - select poll epoll
  - 单个process可以处理多个网络连接IO
  - select poll epoll这个function会不断的轮询所负责的socket
  - 直到socket数据到达 通知用户进程
- **信号驱动IO（不常用）**
- **异步IO**
  - 用户发起read请求后立刻去做其他的事情
  - kernel完成之后将数据拷贝到用户的内存，完成之后发送signal



#### IO多路复用select poll epoll详解

###### 共同点

- 同步IO
- 机制：
  - 一个进程监视多个描述符
  - 某个描述符就绪，通知对应程序进行操作

###### select

```c
int select (int n, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
```

- 监视文件：writefds   readfds  exceptfds

```c
调用后 select函数阻塞
直到描述符就绪（数据可读，可写，except,超时) 函数返回
```

- 【优点】 跨平台支持
- 【缺点】单个进程监视的文件描述符熟练存在最大限制（1024）

###### poll

```c
int poll (struct pollfd *fds, unsigned int nfds, int timeout);

struct pollfd {
    int fd; /* file descriptor */
    short events; /* requested events to watch 要监视的事件 */
    short revents; /* returned events witnessed 发生了的事件*/
};
```

- 【区别】select使用三个位图表示三个fdset方式，poll使用一个pollfd指针实现
- 【优点】没有最大数量限制
- 【共同点】 select和poll都需要在返回后，`通过遍历文件描述符来获取已经就绪的socket`。

###### epoll

> select和poll的增强版本

- 更加灵活  没有描述符限制

- 使用一个文件描述符管理多个描述符   

- 将用户关系的文档描述符事件存放在内核中的一个事件表

- 内核空间用户空间复制只需要一次

```c
int epoll_create(int size)；//创建一个epoll的句柄，size用来告诉内核这个监听的数目一共有多大
int epoll_ctl(int epfd, int op, int fd, struct epoll_event *event)；
/*
epfd：epoll_create返回值
op: 操作（添加 删除 修改） 宏
fd: 要监听的文件面试符
epoll_event: 内核要监听的事件
*/
int epoll_wait(int epfd, struct epoll_event * events, int maxevents, int timeout);
/*
等待epfd上的io事件，最多返回maxevents个事件。
epfd:epoll_create返回值
*/

/*事件结构体*/
struct epoll_event {
  __uint32_t events;  /* Epoll events */
  epoll_data_t data;  /* User data variable */
};
```

- **工作模式**
  - LT模式（level trigger)[默认]
    - epoll_wait检测到描述符事件发生将事件通知给应用程序
    - **应用程序可以不立即处理该事件**
    - 下次调用epoll_wait**依旧通知**
  - ET模式 （edge trigger)
    - **应用程序必须处理该事件**
    - 下次调用epoll_wait**不通知**
- **总结**
  - select/poll  进程只有调用一定的方法后，内核才对所有监视文件描述符进行描述
  - epoll去掉了遍历文件描述符，而是通过监听回调的机制
