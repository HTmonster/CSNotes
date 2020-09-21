# Nginx重写

#### 功能介绍

- rewrite 功能是Nginx服务器提供的一个重要功能

- 用于URL重写
- 用途：修改了网站结构后 1. 用户客户端不用修改书签 2.不用修改友情链接
- 实现模块：`ngx_http_rewrite_module`
- 功能依赖： PCRE模块 

#### 应用场景

- 域名变更   （京东）
- 用户跳转     （链接跳转）
- 伪静态场景    （便于CDN缓存动态页面数据）

#### 重写原理

![1552306550967](C:\Users\Theo_hui\AppData\Roaming\Typora\typora-user-images\1552306550967.png)

#### 重写实现

##### 指令

1. `set` 设置变量

   ```python
   #Syntax:
   set $variable value;
   #Default:
   —
   #Context:
   server, location, if
    
   #将http://www.ayitula.com
   #重写为http://www.ayitula.com/baism
   location / {
   	set $name baism;
   	rewrite ^(.*)$ http://www.ayitula.com/$name;
   }
   ```

2. `if`  语句的判断

   ```python
   #Syntax:
   if (condition) { ... }
   #Default:
   —
   #Context:
   server, location
   
   #模糊匹配  ~ !~  ~*
   #精确匹配   =  !=
   
   location / {
   	root html;
   	index index.html index.htm;
       #chrome浏览器返回403
       #nginx内置变量
   	if ($http_user_agent ~* 'Chrome') {
   	return 403;
   	}
   }
   
   ```

3. `return` 返回 值或者 URL

   ```python
   #Syntax: 
       return code [text];
   	return code URL;
   	return URL;
   
   #Default:
   	—
   #Context: 
   	server, location, if
   
       location / {
   		root html;
   		index index.html index.htm;
   		if ($http_user_agent ~* 'Chrome') {
   			return 403;
   			#return http://www.jd.com;
   		}
   	}
   ```

4. `break` 终止后续的规则

   ```python
   #Syntax: 
   	break;
   #Default:
   	—
   #Context:
   	server, location, if
   
       location / {
   		root html;
   		index index.html index.htm;
   		if ($http_user_agent ~* 'Chrome') {
   			break;#后面不起作用
   			return 403;
   		}
   	}
   ```

5. `rewrite` 重定向URL

   ```python
   rewrite <regex> <replacement> [flag];
   
   #关键字   正则       替代内容    flag标记
   
   #flag:
   last #本条规则匹配完成后，继续向下匹配新的location URI规则
   break #本条规则匹配完成即终止，不不再匹配后⾯面的任何规则
   redirect #返回302临时重定向，浏览器器地址会显示跳转后的URL地址
   permanent #返回301永久重定向，浏览器器地址栏会显示跳转后的URL地址
   
   ```

   

