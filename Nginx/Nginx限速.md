# Nginx限速

#### 简介

- 限制一个用户在一个给定时间段内产生的HTTP请求数（GET请求或者POST请求）
- 限制用于安全（防止暴力破解 防范DDos攻击）

#### 应用场景

- DDOS防御
- 下载IO保护  

#### 限速原理

> 漏桶原理

- 请求从上方进入水桶，从下方流出
- **【缓存处理】**来不及的请求保存在水桶中，**【匀速处理】**以固定的速率流出
- **【多余请求丢弃】**桶满后请求丢弃

#### 限速实现

- `limit_req_zone` 用来限制单位时间内的请求数，速率限制

- `limit_req_conn` 用来限制同一时间内的连接数， 并发限制

  ##### 速率请求

  > 基于IP对下载速率做限制限制每秒处理理1次请求，对突发超过5个以后的请求放⼊入缓存区

  ```shell
  http {
  	limit_req_zone binary_remote_addr zone=baism:10m rate=1r/s;
  	server {
  		location /search/ {
  		limit_req zone=baism burst=5 nodelay;
  	}
  }
  
  # 第一个参数：$binary_remote_addr
  # 表示通过remote_addr这个标识来做限制，“binary_”的目的是缩写内存占用量量，是限制同一客户端ip地址。
  # 第⼆个参数：zone=baism:10m表示生成一个大小为10M，名字为one的内存区域，用来存储访问的频次信息。
  # 第三个参数：rate=1r/s表示允许相同标识的客户端的访问频次，这里限制的是每秒1次，还可以有比如30r/m的。
  
  #limit_req zone=baism burst=5 nodelay;
  #第一个参数：zone=baism
  #设置使⽤用哪个配置区域来做限制，与上面limit_req_zone里的name对应。
  #第二个参数：burst=5，重点说明⼀一下这个配置，burst爆发的意思，这个配置的意思是设置一个大小为5的缓冲区当有大量请求（爆发）过来时，超过了了访问频次限制的请求可以先放到这个缓冲区内。
  #第三个参数：nodelay，如果设置，超过访问频次而且缓冲区也满了的时候就会直接返回503，如果没有设置，则所有请求会等待排队。
  ```

  ##### 并发限制

  ```shell
  #基于IP做连接限制限制同⼀一IP并发为1
  #下载速度为100K
  limit_conn_zone $binary_remote_addr zone=addr:10m;
  server {
  	listen 80;
  	server_name localhost;
  	
  	location / {
  		root html;
  		index index.html index.htm;
  	}
  	location /abc {
  		limit_conn addr 1;  #IP数量限制为1
  		limit_rate 100k;    #下载速度限制为100k
  	}
  }
  
  ```

  ##### 综合案例

  ```shell
  http {
  	include mime.types;
  	default_type application/octet-stream;
  	sendfile on;
  	keepalive_timeout 65;
  	
  	#基于IP做连接限制限制同⼀一IP并发为1
  	#下载速度为100K
  	limit_conn_zone $binary_remote_addr zone=addr:10m;
  	#基于IP对下载速率做限制限制每秒处理理1次请求，对突发超过5个以后的请求放⼊入缓存区
  	limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
  	
  	server {
  		listen 80;
  		server_name localhost;
  	location / {
  		root html;
  		index index.html index.htm;
  	}
  	
  	location /abc {
  		limit_req zone=one burst=5 nodelay;
  		limit_conn addr 1;
  		limit_rate 100k;
  	}
  }
  
  ```

  

