# 神经网络  nn

## nn.Module

### 层

### 方法 forword(input)

### 属性  [net].parameters()  可以训练的参数

## torch.optim 更新优化器

### 包含

- SGD
- Nesterov-SGD
- Adam
- RMSProp
- ...

### 使用

- 1. 选择  optimizer = optim.SGD(net.parameters(),lr=0.01)
- 2. 清空梯度 optimizer.zero_grad()
- 3.输入训练  反向传播
- 4.更新参数  optimizer.step()

*XMind: ZEN - Trial Version*