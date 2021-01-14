# 注意力机制Attention

> 参考：https://medium.com/@pkqiang49/%E4%B8%80%E6%96%87%E7%9C%8B%E6%87%82-attention-%E6%9C%AC%E8%B4%A8%E5%8E%9F%E7%90%86-3%E5%A4%A7%E4%BC%98%E7%82%B9-5%E5%A4%A7%E7%B1%BB%E5%9E%8B-e4fbe4b6d030

## 宏观概念

### ![Image for post](https://miro.medium.com/max/1500/0*t34bed_taVZq5NbY.png)

## 优点

### 1.参数少

### 2. 速度快

- RNN不能并行运算

### 3. 效果好

## attention原理

![Image for post](https://miro.medium.com/max/600/0*8phcA-Y03GujrIn4.png)

### 概括：代权求和

### 阶段

- 1. 查询  query与key进行相似度计算 得到权值
- 2. 归一化  权值归一化 得到可用的权重
- 3. 加权求和 权重和value进行加权求和

## 种类

![Image for post](https://miro.medium.com/max/1500/0*N42UgNYEgLOwbg9w.png)

### 根据计算区域

- Soft Attention

	- 全局计算
	- 参考了所有key的内容

- Hard Attention

	- 直接定位到其中的一个key

- Local Attention

	- 折中方案
	- 先用hard定位到其中的某个地方，再以这个点为中心得到一个窗口区域

### 根据所用信息

- General Attention 

	- 利用到了外部信息
	- 常用于构造两段文本之间的关系

- Local Attention

	- 只使用到内部信息

### 根据层次结构

- 单层Attention

	- 一个query对一段原文进行一次attention

- 多层Attention

	- 一般用于文本具有层次关系的模型

- 多头Attention

	- 多个query对一段原文进行多次attention 
	- 每个query关注到原文的不同部分

### 根据模型

- CNN+Attention

	- 原CNN

		- 卷积=attention的思想 但是是局部的 需要多层卷积区扩大视野
		- Max pooling= hard attention 直接选中某个特征

	- 结合方法

		- 1. 在输入 attention

			- 类似RGB 增加一层特征层

		- 2. 在卷积后 attention

			- 卷积层输出做attention 作为pooling层的输入

		- 3. 使用attention 代替 max pooling

			- 首先使用LSTM学到一个比较好的句向量 作为query
			- CNN学习到特征矩阵作为 key
			- query对key产生权重 进行attention

- LSTM+Attention

	- 原LSTM

		- 输入门决定那些信息进行输入 遗忘门决定那些信息进行遗忘
		- 但是长文本随着step 进行衰减

	- 结合方法

		- 对所有step的hidden state 进行加权，把注意力几种到诊断文字中比较重要的hidden stste

- 纯Attention

*XMind - Trial Version*