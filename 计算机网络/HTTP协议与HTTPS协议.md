# HTTP协议与HTTPS协议

#### 概要

- 超文本传输协议
- HTTP/1.0目前  HTTP/1.1正在规范
- 客户端-服务器架构

#### 特点

- 简单快速
- 灵活
- 无连接
- 无状态

#### 请求头部

![img](https://upload-images.jianshu.io/upload_images/2964446-fdfb1a8fce8de946.png?imageMogr2/auto-orient/)

#### 状态码

- 1xx：指示信息--表示请求已接收，继续处理

- 2xx：成功--表示请求已被成功接收、理解、接受

- 3xx：重定向--要完成请求必须进行更进一步的操作

- 4xx：客户端错误--请求有语法错误或请求无法实现

- 5xx：服务器端错误--服务器未能实现合法的请求

  ```http
  200 OK                        //客户端请求成功
  400 Bad Request               //客户端请求有语法错误，不能被服务器所理解
  401 Unauthorized              //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 
  403 Forbidden                 //服务器收到请求，但是拒绝提供服务
  404 Not Found                 //请求资源不存在，eg：输入了错误的URL
  500 Internal Server Error     //服务器发生不可预期的错误
  503 Server Unavailable        //服务器当前不能处理客户端的请求，一段时间后可能恢复正常
  ```

#### 请求方法

- HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法。

- HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。

  ```http
  GET      请求指定的页面信息，并返回实体主体。
  HEAD     类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头
  POST     向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改。
  PUT  从客户端向服务器传送的数据取代指定的文档的内容。
  DELETE   请求服务器删除指定的页面。
  CONNECT  HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
  OPTIONS  允许客户端查看服务器的性能。
  TRACE    回显服务器收到的请求，主要用于测试或诊断。
  ```

  |                GET                 |                 POST                 |
  | :--------------------------------: | :----------------------------------: |
  | 参数附在URL后 ？连接（地址栏显示） | 提交的数据放在包体中（地址栏不显示） |
  |              安全性低              |               安全性高               |
  |    数据大小有限制（浏览器限制）    |            数据大小无限制            |

#### HTTP建立过程

1. 客户端连接到web服务器   80端口 TCP套接字
2. 发送HTTP请求
3. 服务器段接受请求并返回HTTP响应
4. 释放TCP连接
5. 客户端解析HTML报文

#### 浏览器输入URL后流程

- DNS解析URL地址的ip地址
- 建立TCP连接
- http连接
- 释放TCP连接
- 客户端解释HTTP请求

#### HTTPS协议

- HTTP+SSL/TLS（Secure Socket Layer/HyperText Transfer Protocol)

  ##### 作用

  1. 内容加密
  2. 身份认证
  3. 数据完整性

  ##### 缺点

  - 速度慢

  ##### 流程

  ![img](https://upload-images.jianshu.io/upload_images/2829175-9385a8c5e94ad1da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/648/format/webp)

  1. client Hello,客户端（通常是浏览器）先向服务器发出加密通信的请求

  > （1） 支持的协议版本，比如TLS 1.0版。
  >  （2） 一个客户端生成的随机数 random1，稍后用于生成"对话密钥"。
  >  （3） 支持的加密方法，比如RSA公钥加密。
  >  （4） 支持的压缩方法。

  2. 服务器收到请求,然后响应 (server Hello)

  > （1） 确认使用的加密通信协议版本，比如TLS 1.0版本。如果浏览器与服务器支持的版本不一致，服务器关闭加密通信。
  >  （2） 一个服务器生成的随机数random2，稍后用于生成"对话密钥"。
  >  （3） 确认使用的加密方法，比如RSA公钥加密。
  >  （4） 服务器证书。

  3. 客户端收到证书之后会首先会进行验证

  - 验证流程

  > 1.  公钥验签。
  > 2. 验签证书摘要，然后客户端再使用sha256对证书内容进行一次摘要，如果得到的值和验签之后得到的摘要值相同，则表示证书没有被修改过。
  > 3. 如果验证通过，显示安全。

  - 生成随机数

  > 验证通过之后，客户端会生成一个随机数pre-master secret，然后使用证书中的公钥进行加密，然后传递给服务器端

  4.  服务器收到使用公钥加密 生成交互密码

     > radom1、radom2、pre-master secret通过一定的算法得出session Key和MAC算法秘钥，作为后面交互过程中使用对称秘钥。同时客户端也会使用radom1、radom2、pre-master secret，和同样的算法生成session Key和MAC算法的秘钥。



​	 5.  然后再后续的交互中就使用session Key和MAC算法的秘钥对传输的内容进行加密和解密。
