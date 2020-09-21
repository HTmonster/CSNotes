# Nginx默认网站 访问控制 用户验证 日志管理 防盗链

#### 默认网站

- 只有一个server时候。所有80端口的请求都发给这个服务。这个就是默认网站

#### 访问控制

- 使用`allow deny`命令进行控制

  ```python
  #location [相对的路径]
  location /a {
      allow 127.0.0.1; #允许访问的节点
      allow 192.168.10.42;
      
      deny all;        #禁止访问的节点
      
      return  404;     #返回状态码
      return  http://www.baidu.com  #返回一个网址
  }
  ```

#### 用户验证

- 使用 
  - `auth_basic string|off`  
  -  `auth_basic_user_file` 

```python
location /a {
    auth_basic "用户验证";
    auth_basic_user_file /etc/nginx/htpasswd  #用户密码的存储路径
}
```

#### 日志管理

- 访问日志
  - `log_format  log_name  string`  定义记录日志的格式   全局参数
  - `access_log   logs/access.log  main` 指定日志文件的路径以及使用何种的日志格式目录  server中定义

#### 防盗链

- 使用`valid_referes` 指示可以访问的头

- 使用`invalid_referes`处理盗链的头

  ```python
  #对于本网站的所有图片
  location ~* \. (png|gif|bmp)${
      valid_referers  none blocked *mysite.com; #可以访问的包括 不带参数的 本机的 本网站的
      #非法的返回403
      if($invalid_referes){
          return 403;
      }
  }
  ```

  