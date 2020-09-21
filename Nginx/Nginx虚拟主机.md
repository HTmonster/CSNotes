# Nginx虚拟主机

#### 简介

- 将一台物理服务器分成多个虚拟的服务器   
- 每一个虚拟主机有独立的域名和独立的目录
- 虚拟主机的区分方法：
  - IP
  - port 端口
  - Domain 域名

#### 基于IP的多虚拟主机

- 需要多个ip 

- 多个ip费用高

  ```python
  #基于IP的虚拟主机
  server {
  	listen 192.168.10.42:80;
  	location / {
  		root html/abc;
  		index index.html index.htm index.php;
  	}
  }
  server {
  	listen 192.168.10.52:80;
  	location / {
  		root html/cbd;
  		index index.html index.htm;
  	}
  }
  ```

#### 基于端口的多虚拟主机

- 只需要一个IP

- 端口变更问题 只使用内部用户

  ```python
  server {
  	listen 80;
  	server_name www.abc.com;
  	location / {
  		root html/abc;
  		index index.html index.htm index.php;
  	}
  }
  server {
  	listen 8080;
  	server_name www.abc.com;
  	location / {
  		root html/cbd;
  		index index.html index.htm;
  	}
  }
  ```

  

#### 基于域名的多虚拟主机

- 一个网址一个域名

  ```python
  server {
  	listen 80;
  	server_name www.abc.com;
  	location / {
  		root html/abc;
  		index index.html index.htm index.php;
  	}
  }
  server {
  	listen 80;
  	server_name www.cbd.com;
  	location / {
  		root html/cbd;
  		index index.html index.htm;
  	}
  }
  ```

  