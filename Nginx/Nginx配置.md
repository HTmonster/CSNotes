# Nginx配置



#### 主配置文件讲解

```python
...              #全局块  #【全局的指令】｛运行用户组，pid存放路径，日志路径，配置文件，允许生成数据

events {         #events块
   ...                  #【服务器与用户】
                           #｛进程最大连接数，事件驱动模型，是否多个网路连接，网络连接序列化｝
}

http      #http块       #/*可以嵌套多个server 配置代理 缓存 日志定义 第三方模块*/
{
    ...   #http全局块
    server        #server块   #/*配置虚拟主机的相关参数*/
    { 
        ...       #server全局块
        location [PATTERN]   #location块   #配置请求的路由 页面的处理情况
        {
            ...
        }
        location [PATTERN] 
        {
            ...
        }
    }
    server
    {
      ...
    }
    ...     #http全局块
}
```

#### 主配置文件例子

```python
#启动子进程程序默认用户
#user  nobody;
#一个主进程和多个工作进程。工作进程是单进程的，且不需要特殊授权即可运行；这里定义的是工作进程数量
worker_processes  1;

#全局错误日志的位置及日志格式
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    #每个工作进程最大的并发数
    worker_connections  1024;
}


#http服务器设置
http {
    #设定mime类型，类型由mime.type文件定义
    include       mime.types;
    
    #
    default_type  application/octet-stream;

    #日志格式
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';
    #$remote_addr与$http_x_forwarded_for用以记录客户端的ip地址；
    #$remote_user：用来记录客户端用户名称；
    #$time_local： 用来记录访问时间与时区；
    #$request： 用来记录请求的url与http协议；
    #$status： 用来记录请求状态；成功是200，
    #$body_bytes_sent ：记录发送给客户端文件主体内容大小；
    #$http_referer：用来记录从那个页面链接访问过来的；
    #$http_user_agent：记录客户浏览器的相关信息；

    #全局访问日志路径 
    #access_log  logs/access.log  main;
    #sendfile指令指定 nginx 是否调用sendfile 函数（zero copy 方式）来输出文件，对于普通应用，必须设为on。如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络IO处理速度，降低系统uptime。
    sendfile        on;
    
    #此选项允许或禁止使用socke的TCP_CORK的选项，此选项仅在使用sendfile的时候使用
    #tcp_nopush     on;

    #长连接超时时间
    #keepalive_timeout  0;
    keepalive_timeout  65;

    #开启压缩
    #gzip  on;

    #配置虚拟主机
    server {
        #虚拟主机使用的端口
        listen       80;
        #虚拟主机域名
        server_name  localhost;

        #虚拟主机支持的字符集
        #charset koi8-r;

        #虚拟主机的访问日志路径
        #access_log  logs/host.access.log  main;

        #定义web根路径
        location / {
            #根目录路径
            root   html;
            #索引页
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #

        #根据错误码 返回对应的页面
        error_page   500 502 503 504  /50x.html;

        #定义页面路径
        location = /50x.html {
            root   html;
        }

        #定义反向代理服务器 数据服务器是lamp模型
        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}


        #定义PHP为本机服务的模型  
        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #拒绝apache DR目录及子目录下的.htaccess文件访问
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    #https的配置方案
    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}

```

