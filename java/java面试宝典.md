# java面试宝典

## 基础知识

### 程序基础

- 开发与运行环境

	- JDK与JRE

		- JDK

			- java develop kit JAVA的开发工具
			- 不仅包含JRE 还包含

				- javac (compile)编译 .java->.class
				- java   运行 运行.class文件
				- javaw 应用自己的GUI窗口 不启用控制台

		- JRE

			- java运行的环境  核心 JVM （jvm.dll)

	- 路径搜索

		- rt.jar (jre/lib/rt.jar)
		- CLASSPATH路径
		- 动态路径 -cp  -classpath

- 语言概述

	- java与C++区别

		- 运行和编译区别

			- java

				- 中间字节码
				- jvm
				- 跨平台特性
				- 无需垃圾回收

					- java.lang.Object  finalize方法
					- java.lang.System  gc方法  显式调用开始请求垃圾回收线程
					- java,lang.Runtime  gc方法 单例模式

			- C++

				- 生成机器可以执行的文件
				- 无跨平台特性
				- 语言层面垃圾回收

	- JVM

		- 软件模拟出来的计算机
		- 执行java程序
		- 有自己想象中的硬件（处理器 堆栈 寄存器）相对应的指令系统

- 生成部署和配置

	- 打包

		- jar { c t x u f}{v m e 0 N i}[-c 目录] 文件名

	- java Web
	- EJB

### 语法基础

- 基本类型和语法

	- 变量

		- 分类

			- 静态变量

				- static修饰
				- 生存周期 类决定

			- 成员变量

				- 非static修饰
				- 生存周期 对象决定

			- 局部变量

				- 定义在方法里
				- 作用范围  ｛｝决定

		- 数据类型

			- 基本数据类型

				- byte

					- 封装类  Byte

				- short

					- 封装类 Short

				- int

					- 封装类 Interger

				- float

					- 封装类 Float

				- double

					- 封装类 Double

				- boolean

					- 封装类 Boolean

				- char

					- 封装类 Character

			- 引用数据类型

				- 与C++指针的区别

					- java

						- 引用其值为地址的数据元素
						- 初始值 null
						- 不可计算
						- 不会内存泄露

					- c++

						- 一个放地址的变量
						- 初始值为
						- 可以计算 ++ --
						- 可能内存泄露

	- main方法

		- 定义在类中
		- 公开
		- 静态
		- 无返回值
		- 参数为字符串数组

	- equal与==

		- ==

			- 基本数据类型

				- 比较值

			- 引用数据类型

				- 比较对象地址

		- equal

			- java.lang.Object方法 
			- 可以被重写
			- 对于字符串 比较字符串序列是否相等

	- 循环机制

		- for
		- while
		- do while

	- 注释

		- 单行注释 //
		- 多行注释 /*  */
		- 文档 注释 /**  */

- 对象和类型

	- 多态

		- “多种形态”发送消息给对象 让对象自己决定自行决定如何响应

	- 静态成员

		- static修饰
		- 包括

			- 静态成员变量
			- 静态方法
			- 静态代码块

		- 特点

			- 类加载时候进行创建和初始化
			- 一个类只有一份
			- 类的所有实例可以访问

	- 父类构造

		- super

	- 接口与抽象类

		- 抽象类

			- 静态数据 与抽象方法的集合

		- 接口

			- 特殊形式的抽象类

	- 内部类

		- 静态内部类

			- 隶属与外部类 使用时候相当与一个独立的外部类

		- 成员内部类
		- 局部内部类

			- 定义在方法中

		- 匿名内部类

- 包和访问控制

	- 访问控制

		- private
		- protected
		- public
		- defualt

### 数据类型及类型转换

- 整型

	- int

		- 基础数据类型 
		- 字节长度4
		- 保留在栈中

	- Integer

		- 包装类
		- 不能直接计算

	- long

		- 字节长度8

- 实型

	- float   4个字节
	- double  8个字节
	- 精确计算

		- BigDecimal

- 布尔型

	- 非0不代表 true

- 字符型

	- char

		- unicode编码
		- 2个字节

- String型

	- StringBuffer
	- StringBuilder
	- 字符翻转

		- StringBuffer.reverse(）

### 数组和集合

- 数组 

	- 数组是一种类
	- 数组拷贝

		- system.arraycopy

	- 长度不固定

- 集合框架

	- 框架结构

		- 26、java集合框架

			- Collection接口

				- Collection接口是最基本的容器接口，继承至Iterable接口，允许元素重复，可以无序
				- List接口

					- LinkedList

						- 底层的数据结构是链表结构
						- 查询较慢，增删较快

					- ArrayList

						- 底层的数据结构使用的是数组结构
						- 查询很快，但增删较慢
						- 线程不同步

					- Vector

						- 底层是数组数据结构 
						- 线程同步
						- 无论查询还是增删都很慢，被ArrayList替代了

				- Set接口

					- HashSet类

						- 底层实现是基于HashMap
						- 不保证Set的迭代顺序
						- 不保证该顺序永久不变

					- LinkedHashSet

						- 链表和哈希表
						- FIFO 插入有序 唯一
						- 链表   ——》有序
						- 哈希表  ——》唯一

					- TreeSet

						- 红黑树
						- 唯一 有序
						- 排序

							- 自然排序

								- 实现 Comparable接口
								- 重写Compareto方法

							- 比较器排序

								- 单独创建一个比较类 继承Comparator接口
								- 重写Compare方法

						- 唯一性

							- 返回值是否为0

			- Map接口

				- HashTable

					- 时间更早  方法同步

				- HashMap类

					- 基于哈希表的Map接口实现，利用哈希算法根据hashCode()来配置存储地址

				- LinkedHashMap
				- TreeMap类

					-  基于红黑树（Red-Black tree）的NavigableMap 实现。该映射根据其键的自然顺序进行排序，或者 根据创建映射时提供的Comparator 进行排序，具体取决于使用的构造方法

				- SortedMap接口

					- 进一步提供关于键的总体排序 的 Map

			- 辅助工具类

				- Collections、Arrays类

					- 提供了一系列静态方法，用于对集合中元素进行排序、搜索以及线程安全等各种操作

						- max
						- min
						- fill  使用指定元素替换所有元素
						- sort  自然升序排序
						- binarySearch  二分法搜索
						- 。。。。。。

				- Comparable

					- Comparable用作默认的比较方式，实现了该接口的类之间可以相互进行比较，这个对象组成的集合就可以直接通过sort()进行排序了

				- Comparator接口

					- Comparator是设计模式中策略模式的一种应用

### 图形界面

- 基础

	- JFrame
	- JButton
	- JTextField   单行
	- JTextArea  多行

- 布局控制

	- BorderLayout  五个区域
	- FlowLayout  一行从左到右排序
	- GridLayout 分为几行几列
	- BoxLayout  水平一行或者竖直一列
	- CardLaout 卡片布局 每次显示一个

- 事件模型

	- 构成部分

		- 事件主体
		- 监听器 addXXXXListener
		- 事件

## 高级特性

### 输入输出流

- File类

	- isDirectory() 是不是目录
	- isFile()  是不是文件
	- list() 列出目录下的所有文件
	- getName()获得文件名
	- delete() 删除文件

- Stream类

	- InputSteram

		- read()方法

	- OutputStream

		- write()方法

	- FileInputStream
	- FileOutputStream
	- ObjectInputStream
	- ObjectOutputStream
	- BufferredInputStream
	- BufferrredOutputStream

- 字符流

	- StringReader
	- StringWriter
	- BufferedReader
	- BufferedWriter

- 对象序列化

	- 把对象内存中的数据安装一定的规则 变成一系列的字节数据  然后将字节数据写入到流中
	- 序列化

		- 类需要实现Serializable接口
		- 还需要听静态常量 serialVersionUID

	- 反序列化

### 多线程编程

- 线程类

	- 实现方法

		- 实现 java.lang.Runnable接口
		- 继承 java.lang.Tread类

- 启动

	- Tread类的start()方法

- 线程安全

	- sycharonized

- 线程池

	- 一个或多个线程的集合
	- 作用

		- 调度管理的管理线程
		- 要求执行的任务队列

### 反射机制

- 简介

	- 解剖java的类、接口、方法、属性等元素
	- 动态的知道一个陌生类的所有信息

- 作用

	- 访问java对象的属性、方法、构造方法

- class类

	- 简介

		- 代表一种被加载进入JVM的类
		- 该类的信息隐射

	- 获得方法

		- Class.forName("类的包名")
		- 类.class 静态属性
		- object类的getClass（）方法

	- Field类

		- 提供有关类或接口的属性（字段）或成员变量的信息
		- 获得方法

			- Class类的getDeclaredFiled方法
			- Class类的getDeclaredFiles方法

		- 使用方法

			- getXXX  获取对象的值
			- setXXX 设置对象的值

	- Method类

		- 获得有关类的方法（静态或者非静态）
		- 获得方法

			- Class类的getMethod方法
			- Class类的getMethods方法

		- 使用方法

			- invoke 方法调用

- 反射机制实例化类

	- 无参数构造方法

		- 1.获取class对象
		- 2. 调用class对象的newInstance方法

	- 有参数构造方法

		- 1. 获取class对象
		- 2. 获取constractor实例
		- 3. 调用newInstance方法

- 反射机制访问私有成员

	- 私有成员

		- 私有变量
		- 私有方法

	- 访问方法

		- 1.获得class对象
		- 2.使用getDeclaredFiled方法
		- 3.调用setAccessible(true)方法

- 反射机制覆盖toString

	- 1. 获得class对象
	- 2. 使用getDeclaredFileds方法获取所有对象
	- 3. 遍历所有的Filed对象
	- 4. 进行输出

### 网络编程

- TCP编程模型

	- 客户端

		- 1. 获得Socket对象 Socket ss =new Socket("IP地址","端口号")
		- 2. 获得输入输出流
		- 3. 调用 read  write方法
		- 4. 释放资源

	- 服务器端

		- 1. 创建ServerSocket对象  ServerSocket ss = new ServerSocket(int 端口号）
		- 2. 监听客户端要求  ss.accept()
		- 3.获得输入输出流

			- InputStream is =ss.getInputStream()  输入流
			- OutputStream os = ss.getOutputStream() 输出流

		- 4. 调用 read write方法进行数据的传输
		- 5. 关闭相关资源

- UDP编程模型

	- 接收端

		- 1. 创建数据Socket   DatagramSocket  ds= new DtagramSocket(端口号）
		- 2. 创建byte数据接收数据  byte[] buffer = new byte[xxxx]
		- 3. 构建数据包对象  DatagramPacket dp = new DatagramPacket(buff,1024)
		- 4. 调用recive方法获得数据  ds.receive( dp）
		- 5. 释放相关资源 ds.close()

	- 发送端

		- 1. 创建数据Socket   DatagramSocket  ds= new DtagramSocket(端口号）
		- 2. 创建byte数据接收数据  byte[] buffer = new byte[xxxx]
		- 3. 构建数据包对象  DatagramPacket dp = new DatagramPacket(str.getBytes(),0,str.length(),InetAddress.getbyName("地址号"),端口号）
		- 4. 调用send方法发送数据  ds.receive( dp）
		- 5. 释放相关资源 ds.close()

### 数据库操作

- JDBC （Java DataBase Connectivity)

	- 工作原理

		- 驱动模式设计
		- 两套接口

			- 用户使用API
			- 数据库厂商SPI

	- 操作接口和类

		- java.sql
		- javax.sql

	- 编程步骤

		- 1.注册驱动 class.forName("数据库驱动类的完整类名")
		- 2. 获取一个连接   Connection conn = Drivermanager.getConnection("URL","用户名","密码")
		- 3. 创建一个会话 Statement stmt =conn.createStatement()
		- 4. 执行SQL语句

			- 4. 1执行SQL语句（增加 修改 删除）stmt.executeUpdate("SQL语句");
			- 4.2 执行SQL语句 （查询） ResultSet rs = stmt.conn.excuteQuery("SQL语句")

		- 5. 对查询的结果进行处理  while(rs.next()){}
		- 6. 关闭连接

			- rs.close
			- stmt.close
			- conn.close

- JDBC事务

	- 过程

		- 1.在建立连接的时候关闭自动提交

			- Connection conn=Drivermanager.getConnection("URL","用户名","密码")
			- conn.setAutoCommit(false) //关闭自动事务提交

		- 2.捕获执行代码

			- 成功 则提交
			- 失败 则回滚

- 分层开发

	- 业务层
	- 数据访问对象层DAO层

		- 把数据包装成对象
		- 把对象拆分为数据

	- 数据库

- 连接池技术

	- 程序员使用Data source 数据源形式获取连接
	- 数据源对象以JNDI形式返回给程序员

- 结果集进阶

	- 在创建会话对象过程中指定结果集的类型和时候可更新   conn.createStatement(sql,type,concurrency)   conn.prepqredStatement(sql, type,concurrency)

		- type

			- TYPE_FORWARD_ONLY   结果集不能滚动
			- TYPE_SCROLL_INSENSITIVE   结果集可以滚动   对数据库变化不敏感
			- TYPE_SCROLL_SENSITIVE  结果集可以滚动 对数据库变换敏感

		- concurrency

			- CONCUR_READ_ONLY
			- CONCUR_UODATABLE

## java EE

### Web开发相关技术

- servlet

	- 概念

		- 代表服务器端的一个资源
		- Web容器的最基本组成单位
		- 信息资源的最小单位

	- javax.servlet.Servlet接口

		- 实现类

			- javax.faces.webapp.FacesServlet

				- 用于JSF的Servlet

			- javax.servlet.GenericServlet

				- 抽象类
				- 用于一般的Servlet开发

			- javax.servlet.http.HttpServlet

				- 抽象类
				- 使用最多
				- 提供不同放入方法区分HTTP请求

					- doPost()
					- doGet()
					- 等

	- 只能在web容器中存活

		- 创建
		- 初始化
		- 提供服务
		- 销毁等

	- web.xml中的配置信息

		- 定义Servlet <Servlet>标签
		- 访问URL <servlet-mapping>
		- 初始化参数  <init-param>
		- 启动时机 <load-on-startup>

	- 生命周期

		- 加载

			- 加载到虚拟机中并实例化
			- 无参数构造方法
			- 默认在第一次请求时加载
			- <load-on-startup>

		- 初始化

			- init()方法
			- 初始化代码 例如打开资源

		- 提供服务

			- HTTP请求指向Servlet时候
			- service方法

		- 销毁

			- 重新部署Web  关闭Web服务时候
			- destrory()方法
			- 释放资源的代码

- 过滤器

	- 简介

		- 把多个Servlet 的相同逻辑抽象到一块处理
		- 过滤特定资源请求信息和响应信息

	- javax.servlet.Filter接口

		- doFilter()方法

- 监听器

	- web容器中的一个组件
	- 对对象进行监听

		- request

			- 监听接口 ServletRequestListenner

		- session

			- 监听接口 HttpSessionListerner

		- application

			- 监听接口 ServletContextListener

- Web容器

	- 规范

		- 1. 目录结构规范

			- 所有内建都需要包含在一个文件夹中
			- 必须包含WEB-INF子文件夹

				- classes文件夹
				- lib文件夹
				- web描述文件 web.xml

		- 2. 类文件

			- 第三方jar文件 存放在WEB-INF/lib文件夹中

		- 3. web.xml 规范

			- Servlet
			- 过滤器
			- 监听器
			- 安全验证

		- 4. 其他资源文件

			- JSP
			- HTML
			- 图片和声音
			- 等

- JSP动态语言（Java Server Page)

	- 简介

		- 在HTML代码中 穿插JSP脚本和标签
		- 建立在Servlet规范功能之上

	- 处理过程

		- 客户端发出JSP请求
		- Web容器检验JSP语法是否正确
		- 将JSP文件转化为Servlet源码文件
		- 创建一个Servlet类的对象实例，提供服务

	- 内置对象

		- application

			- 代表整个Web应用程序

		- session

			- Http会话对象

		- request

			- 请求对象

		- response

			- 返回对象

		- out

			- 写出流文件 用于返回数据给客户端

		- page

			- 普通页面对象

		- pageContext

			- 页面上下文

		- exception

			- 用于错误页面

		- config

			- 配置对象 用于获取初始化参数等数据

	- JavaBean JSP拓展

		- 可重用性
		- JavaBean规范

			- 公开类
			- 有一个公开的无参数构造方法
			- 提供公开的 setXXX和 getXXX方法决定JavaBean的属性

	- EL和JSTL  简化JSP展现数据的开发

### Structs Spring Hibernate

- MVC设计模式

	- 模型 Model

		- 应用程序的数据
		- 处理数据的规则
		- 为视图查询模型相关状态的能力

	- 视图 View

		- 组织模型的内容
		- 从模版中获取数据
		- 将数据展现给用户

	- 控制器 Contoller

		- 接收客户端请求
		- 把请求转化为某种行为

- Structs框架

	- 简介

		- 老资格的MVC开发框架
		- Apache组织开源项目

	- 架构

		- 控制器 Contoller

			- ActionServlet

				- Structs的入口  
				- 处理所有的请求
				- 决定对应的Action

			- Action

				- 代表一次动作 （注册 购买等）

			- structs-config.xml

				- 整个Structs的配置

		- 模型 Model

			- ActionForm

				- 保存数据
				- 数据验证
				- 一般一个Action对应一个ActionForm

		- 视图层 View

			- JSP

	- 处理过程

		- 1. 客户端发出请求
		- 2. ActionServlet接收请求
		- 2.1 根据structs-config.xml来选择一个Action
		- 2.2 实例化Action 调用execute方法
		- 3. 根据返回的ActionForword找到对应的JSP
		- 4. JSP获取对应的数据 构成页面结果
		- 5.客户端接收请求并返回

	- 开发步骤

		- 1.搭建Struct开发环境 （必须的jar文件，web.xml  struct-config.xml)
		- 2. 实现view JSP文件
		- 3.实现model  创建和配置ActionForm类
		- 4. 实现Controller  创建和配置Action类

	- Action

		- 普通的Action
		- 表单中含多个参数 DispatchAction
		- 多个提交按钮时候   LookupDispatchAction
		- 客户端不便于传递参数 MappingDispatchAction

- Hibernate

	- 功能

		- 数据持久化
		- 对象关系映射模型ORM

	- 原理

		- 对JDBC进行一种包装

	- 重要接口

		- Session接口

			- 被持久化对象的增、删、查、改

		- SessionFactory接口

			- 用来生产Session的工厂类

		- Configuration接口

			- Hibernate的配置工作

		- Transaction接口

			- 事务相关操作

		- Qurey接口

			- 各种数据的查询功能

	- 实体状态

		- 瞬时态

			- new对象创建实体时候  没有id值

		- 持久态

			- 存在于Session中的对象
			- 通过save() saveOrUpdate()等方法转换过来

		- 托管状态

			- 从Session中脱离出来时候
			- 通过close() evict()等方法转化过来

	- HQL查询语言

		- 简介

			- 提供给开发者用来以面向对象思想进行实体增，删，查，改操作的查询语言

		- 基本语法

			- 待补充

		- 一对一映射

			- <one-to-one>标签

		- 一对多映射

			- <one-to-many>
			- <many-to-one>

		- 多对多映射

			- <mant-to-many>

- Spring

	- 简介

		- 轻量级别JavaEE容器

	- 依赖注入

		- 简介

			- ICO容器的核心概念
			- 通过容器管理对象数据的填充和对象之间的关系

		- ICO容器

			- 核心

				- Spring提供的Bean工厂

					- Bean 创建的各个实例
					- 负责读取Bean定义文件
					- 管理对象的加载，生成
					- 维护bean对象与其他Bean对象的依赖关系
					- 负责Bean的生命周期

		- 说明

			- 组件之间的依赖关系由容器在运行的时候决定
			- 控制权转到容器

		- 思想

			- 业务代码与程序本身结构代码分开
			- 容器不侵入到应用程序中
			- 应用程序依赖抽象的接口
			- 容器依据这些接口将所需要资源注入到应用程序中

		- 注入方法

			- 1. 通过setter方法注入

				- 按照JavaBean的可写属性的setter方法来规范定义
				- Spring利用反射机制
				- 在Bean构建好后 调用setter方法 将属性值设置给Bean

			- 2.通过构造方法

				- 在创建Bean实例的时候
				- 调用Bean构造方法
				- <constructor-arg>标签

	- 声明式事务

		- AOP思想

			- 功能比较复杂的拦截器
			- 在代码到达真正目标前进行拦截

		- 简介

			- 为普通Java类封装事务控制
			- 底层为动态代理技术

				- 针对接口

		- 优点

			- 业务对象不需要依赖任何事务技术设施

- SSH开发

	- 1. 完成Structs配置

		- web.xml
		- structs-config.xml

	- 2. 完成Hibernate配置 hibernate.cfg.xml
	- 3. 在web.xml中为spring配置应用程序上下文
	- 4. 用Spring提供的cottroller替换Structs原有controller
	- 用spring提供的SessionFactoryBean类读取hibernmate,cfg,xml 完成spring对Hibernate整合
	- 保存必须的jar文件到 WEB-INF/lib文件夹中

### EJB JPA

- EJB

	- 介绍

		- 企业级JavaBean
		- Java EE服务器端组件开发标准规范
		- 用于开发和部署分布式应用程序

	- 组成部分

		- 组件

			- 符合某种规范的Java类接口
			- 行为通过配置信息来控制
			- 一般负责具体的业务逻辑

		- 容器

			- 提供组件的温床
			- 提供中间件的服务

	- Bean分类

		- 会话Bean 

			- 实现业务逻辑
			- 负责接收客户端请求
			- 可有状态也可无状态

				- 有状态
				- 无状态

		- 实体Bean

			- 代表实体模型对象
			- 用于实现对象关系映射

		- 消息驱动Bean

			- 异步编程
			- 基于消息服务

	- 开发步骤

		- 1.完成业务接口和业务Bean类

			- Local
			- Remote
			- Stateless

		- 2.编译 

			- 引入javaee.jar文件进行编译

		- 3. 提供部署描述文件 

			- ejb-jar.xml

		- 4. 部署，打包和发布
		- 5. 检查部署成功与否
		- 6.写一个客户端程序进行检验

## 装箱与拆箱

java 5.0之后


## 对象池

### 9个 

- 8个基本数据类型的封装类
- string对象

### 作用

- 避免大量的创建销毁

## 迭代器 （Iterator)

### hasNext()

### next()

### remove()

## 泛型

### 概念

- 即“参数化类型”   类型定义为参数化 在使用/调用过程中传入具体的类型

### 特性

- 只在编译时有效  （逻辑为多个类型 实际是相同的基本类型）

### 使用

- 泛型l类
- 泛型接口
- 泛型方法

*XMind - Trial Version*