# Docker

## 简介

### 新兴的虚拟化方式

### 优势

- 启动快
- 资源利用率高
- 快速交付与部署

	- 开发者  使用一个标准的镜像构建一套开发容器
	- 运维者  直接使用这个容器来部署代码
	- 快速创建 快速迭代
	- 整个过程可见

- 高效虚拟化

	- 内核级别
	- 不需要额外的hypervisor

- 迁移和拓展方便

	- 物理机
	- 虚拟机
	- 公有云
	- 私有云
	- 个人电脑
	- 服务器

- 管理简单

	- 修改以增量方式分发和更新

### 与虚拟机的对比

## 基本概念

### 镜像 Image

- 一个只读的模板
- 可以创建容器
- 简单的机制来创建和更新

### 容器 Container

- 运行应用
- 镜像创建的运行实例

	- 启动
	- 开始
	- 停止
	- 删除

- 容器间隔离

### 仓库 Repository

- 集中存放镜像的场所
- 分类

	- 私有
	- 公有

		- Docker Hub 国外
		- Docker Pool 国内

## 镜像

### 从仓库获取镜像

- docker pull命令

	- 默认仓库 Docker Hub
	- 可以自己指定仓库地址

### 上传镜像到仓库

- docker push

### 管理本地主机的镜像

- 显示本地镜像 docker images

	- 仓库来源 REPOSITORY
	- 镜像的标记 TAG
	- ID号 IMAGE ID
	- 创建时间 CREATED
	- 镜像大小 VIRTUAL SIZE

- 修改镜像标签 docker tag
- 创建镜像文件

	- 提交修改后的镜像 docker commit 

		- -m 指定提交的说明信息
		- -a 指定更新的用户信息
		- 指定容器ID tag等信息

	- 利用Dockerfile来创建镜像  docker build

		- -t  添加标签 指定新的镜像用户信息
		- 依据Dockerfile中的指令一条条执行

	- 本地文件系统导入镜像

		- 例如使用模版 openvz

- 镜像与本地文件交互

	- 镜像文件保存到本地文件

		- docker save 

			- -o  目标文件名

	- 从本地文件载入镜像文件

		- docker load

			- docker load --input  文件名
			- docker load < 文件名

- 移除本地镜像

	- docker rmi

	  rm 是移除容器 
	  *移除镜像前需要移除依赖的所有容器
	  

### 镜像实现的原理

- 多个层次
- 增量修改和维护
- Union FS将不同的层结合到镜像中

	- 不借助LVM RAID将多个disk挂到同一目录下
	- 将只读的分支和可写的分支联合在一起

## 容器

### 简介

- 独立运行
- 一个或一组应用及其运行环境

### 容器操作

- 运行容器

	- 1. 基于镜像新建一个容器并启动

		- docker run

			- -t 分配一个伪终端并绑定到标准输入上
			- -i 让容器标准输入保持打开
			- -d 以守护态运行
			- -v 数据卷挂载
			- --name 自定义容器命令
			- --link 容器互联

	- 2. 将终止容器重新启动

		- docker start

- 终止容器

	- docker stop

- 重新运行

	- docker restart

- 进入容器

	- docker attach 命令
	- nsenter工具

- 导入和导出

	- 导出容器

		- docker export

	- 导入容器

		- docker import 

			- 通过本地文件 cat  xxx.tar | sudo docker import - xxxx/xxx
			- 通过URL  sudo docker import URL

- 删除容器

	- docker rm

		- -f 删除运行中的容器

- 查看信息

	- docker ps 容器信息

		- -a 查看终止状态的容器

	- docker logs 输出信息

## 仓库

### 简介

- 集中存放镜像的地方

### 公有仓库

- 搜索

	- docker search

- 登录

	- docker login

### 本地仓库

### 仓库配置文件

- 模版

	- config_sample.yml

## 数据管理

### 简介

- docker内部及容器之间管理数据

### 管理方式

- 数据卷

	- 简介

		- 一个可供一个或多个容器使用特殊目录

	- 特性

		- 可以在容器之间共享和重用
		- 修改立即生效
		- 更新不会影响镜像
		- 一直存在直到没有容器使用

	- 创建

		- docker run  -v 目录

- 数据卷容器

	- 简介

		- 一个正常的容器
		- 专门为其他容器提供挂载

	- 操作

		- 创建

			- docker run -v 名称

		- 挂载

			- docker run --volumes-from 

		- 备份

			- tar

		- 恢复

			- untar

## 网络

### 简介

- 运行网络应用
- 外部访问

### 创建

- -P 参数 随机映射端口 49000-49900
- -p参数 指定映射的端口

### 查看

- docker port  端口

### 容器互联

- --name
- --link

### 高级网络配置

## Dockerfile

### # 注释 

### 基础镜像信息

- FROM 镜像基础

### 维护者信息

- MAINTAINER 维护者信息

### 镜像操作指令

- RUN 创建中运行

	- RUN <command>
	- RUN ["executeble","param1" ,"param2"]

### 容器启动时命令

- CMD 容器启动后运行的程序

	- CMD ["executeable","param1","param2"]
	- CMD commanda param1 param2
	- CMD ["param1","param2"]

- ADD 复制本地文件 URL tar文件 到容器中
- EXPOSE 向外部开放端口
- ENV 指定一个环境变量
- COPY 复制本地目录到容器中
- ENTRYPOINT 容器启动后执行的命令
- VOLUME 挂载点
- USER 运行容器时候的用户名或UID
- WORKDIR 为RUN CMD ENTRPOINT指定配置工作目录
- ONBUILD 配置镜像为其他新创建镜像的基础镜像时执行的命令

## docker run 后台操作

### 子主题 1

- 检查本地是否存在指定的镜像，不存在就从公有仓库下载
- 利用镜像创建并启动一个容器
- 分配一个文件系统，并在只读的镜像层外面挂载一层可读写层
- 从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去
- 从地址池配置一个ip 地址给容器
- 执行用户指定的应用程序
- 执行完毕后容器被终止

## 差别

### load

- 加载镜像文件
- 保持完整记录
- 体积大

### improt

- 加载容器文件
- 丢弃所有的元数据和历史记录
- 仅容器的当时的快照

*XMind - Trial Version*