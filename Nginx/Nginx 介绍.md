# Nginx 介绍

#### 简介

- 轻量级别的web服务器
- 高性能
- web和反向代理服务器
- IMAP/POP3/SMTP代理服务器

#### 安装

##### 源码安装

```shell
wget http://nginx.org/download/nginx-1.xx.xx .tar.gz -P /usr/src
```

- **安装步骤**

  - 配置
    - --prefix=path 安装的路径
    - --help  配置参数
    - 依赖包：` yum install gcc pcre-devel zlib zlib-devel`
  - 编译
    - make
  - 安装
    - make install

- **安装后的目录**

  ```shell
    nginx path prefix: "/usr/local/nginx"
    nginx binary file: "/usr/local/nginx/sbin/nginx"
    nginx modules path: "/usr/local/nginx/modules"
    nginx configuration prefix: "/usr/local/nginx/conf"
    nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
    nginx pid file: "/usr/local/nginx/logs/nginx.pid"
    nginx error log file: "/usr/local/nginx/logs/error.log"
    nginx http access log file: "/usr/local/nginx/logs/access.log"
    nginx http client request body temporary files: "client_body_temp"
    nginx http proxy temporary files: "proxy_temp"
    nginx http fastcgi temporary files: "fastcgi_temp"
    nginx http uwsgi temporary files: "uwsgi_temp"
    nginx http scgi temporary files: "scgi_temp"
    
    
    nginx
  ├── client_body_temp
  ├── conf                                                      #Nginx所有配置文件
  │   ├── fastcgi.conf                                          #fastcgi相关参数配置文件
  │   ├── fastcgi.conf.default                                  #备份文件
  │   ├── fastcgi_params                                        #fastcgi参数文件
  │   ├── fastcgi_params.default
  │   ├── koi-utf
  │   ├── koi-win
  │   ├── mime.types                                            #媒体类型
  │   ├── mime.types.default
  │   ├── nginx.conf                                            #主配置文件
  │   ├── nginx.conf.default
  │   ├── scgi_params                                           #scgi参数
  │   ├── scgi_params.default
  │   ├── uwsgi_params                                          #uwsgi相关参数
  │   ├── uwsgi_params.default
  │   └── win-utf
  ├── fastcgi_temp                                         #fastcgi临时数据目录
  ├── html                                                 #默认站点目录
  │   ├── 50x.html                                              #错误页面替代文件 502界面
  │   └── index.html                                            #默认首页文件
  ├── logs                                                  #日志目录
  │   ├── access.log                                            #访问日志文件
  │   ├── error.log                                             #错误日志文件
  │   └── nginx.pid                                             #pid文件 所有进程的id
  ├── proxy_temp                                            #临时目录
  ├── sbin                                                  #命令目录
  │   └── nginx                                                 #启动命令
  ├── scgi_temp                                             #临时目录
  └── uwsgi_temp                                            #临时目录
  ```

#### Nginx启动

- 查看端口状态方法
  - `lsof -i port`
  - `netstat -ntpl`
- 启动
  - sbin目录下 `nginx 端口 监听地址 协议`

#### Nginx关闭

- sbin目录下：`./nginx -s stop`

#### Nginx重启

- sbin目录下： `./nginx -s reload`



