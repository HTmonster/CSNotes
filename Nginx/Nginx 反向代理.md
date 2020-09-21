# Nginx 反向代理

#### 正向代理 反向代理 透明代理

##### 正向代理

![img](https://s1.51cto.com/attachment/201210/105641260.jpg)

> 代理服务器Z代替  访问方（用户A） 去访问  服务器（服务器B）

![img](https://s1.51cto.com/attachment/201210/105737336.jpg)

- 用来访问无法访问的服务器
- 加速访问服务器
- Cache作用
  - 如果用户访问的数据已经被访问过了
  - 就可以直接在代理服务器中取
  - 而不用访问服务器
- 授权管理 （防火墙）
- 隐藏访问者的踪迹
  - 肉鸡

##### 反向代理

![img](https://s1.51cto.com/attachment/201210/110207878.jpg)

> 客户端向反向代理的命令空间（name-space)中发送普通请求
>
> 反向代理判断向何处转交请求
>
> 将获得内容返回客户端

- 隐藏和保护原始服务器 【堡垒机】
  - 防火墙和反向代理服务器共同保护原始服务器
- 负载均衡
  - ![img](https://s1.51cto.com/attachment/201210/110311352.jpg)
  - 代理服务器集群
  - 让不同的代理服务器去应答不同的用户
- cache的作用

##### 透明代理

![img](https://s1.51cto.com/attachment/201210/110500391.jpg)

> 客户端不需要知道代理服务器的存在
>
> 改编报文   传送真实报文
>
> 【匿名代理】

#### 反向代理应用场景

- 堡垒机  安全
- 内网发布  
  - 多个内网环境
  - 对外统一IP
- 缓存场景

#### 方向代理实现

- **location** 中使用 `proxy_pass`进行设置

  ```python
  location / {
      index index.php index.html index.htm; #定义⾸首⻚页索引⽂文件的名称
      proxy_pass http://mysvr ;#请求转向mysvr
      定义的服务器器列列表
      proxy_set_header Host $host;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      client_max_body_size 10m; #允许客户端请求的最⼤大单⽂文件字节数
      client_body_buﬀer_size 128k; #缓冲区代理理缓冲⽤用户端请求的最⼤大字节数，
      proxy_connect_timeout 90; #nginx跟后端服务器器连接超时时间(代理理连接超时)
      proxy_send_timeout 90; #后端服务器器数据回传时间(代理理发送超时)
      proxy_read_timeout 90; #连接成功后，后端服务器器响应时间(代理理接收超时)
      proxy_buﬀer_size 4k; #设置代理理服务器器（nginx）保存⽤用户头信息的缓冲区⼤大⼩小
      proxy_buﬀers 4 32k; #proxy_buﬀers缓冲区，⽹网⻚页平均在32k以下的话，这样设置
      proxy_busy_buﬀers_size 64k; #⾼高负荷下缓冲⼤大⼩小（proxy_buﬀers*2）
      proxy_temp_file_write_size 64k; #设定缓存⽂文件夹⼤大⼩小，⼤大于这个值，将从upstream服务器器传
  }
  s
  ```

  