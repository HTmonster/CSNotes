# 自动微分 autograd

## 简介

### 神经网络的核心

### 为Tensors上的所有操作提供自动微分

## 追踪操作

### 开始追踪

- 属性 .requires_grad=True

  开始追踪tensor的所有操作
  完成之后可以使用.backword()来自动计算所有**梯度**
  梯度积累在 .grad属性中

### 结束追踪

- .detach()  将其与计算历史记录分离
- 代码块 使用 with torch.no_grad()包装起来

## 向后传播

### [tensor].backword()

## 梯度

### .grad属性

*XMind: ZEN - Trial Version*