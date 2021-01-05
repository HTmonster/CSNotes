# 张量  tensor

## 构造

### 未初始化矩阵 torch.empty

```python
empty_array=torch.empty(5,3) # 5*3的矩阵
# tensor([[8.4490e-39, 8.7245e-39, 1.1112e-38],
#         [8.9082e-39, 9.5510e-39, 8.7245e-39],
#         [8.4490e-39, 8.7245e-39, 1.0102e-38],
#         [1.0653e-38, 8.7245e-39, 9.0918e-39],
#         [1.1112e-38, 9.5511e-39, 1.0102e-38]])
```

### 随机初始化矩阵 torch.rand

```python
and_array=torch.rand(5,3) 

# tensor([[0.1509, 0.2514, 0.9916],
#         [0.3242, 0.3549, 0.4535],
#         [0.8333, 0.3298, 0.3560],
#         [0.7369, 0.9526, 0.7183],
#         [0.9709, 0.8077, 0.9533]])
```

### 全0矩阵 torch.zeros

```python
zero_array=torch.zeros(5,3,dtype=torch.long)

# tensor([[0, 0, 0],
#         [0, 0, 0],
#         [0, 0, 0],
#         [0, 0, 0],
#         [0, 0, 0]])
```

### 使用数据构造 torch.tensor

```python
tensor_array=torch.tensor([3,4,5])

# tensor([3, 4, 5])
```

### 基于已经存在的tensor （属性继承）

- 新全1矩阵  [tensor].new_ones

  ```python
  new_array=tensor_array.new_ones(3,5)  #区别 会继承属性
  
  # tensor([[1, 1, 1, 1, 1],
  #         [1, 1, 1, 1, 1],
  #         [1, 1, 1, 1, 1]])
  ```

- 随机  torch.randn_like([tensor],dtype=)

  ```python
  new_rand_array=torch.randn_like(new_array,dtype=torch.float) #类型重写
  
  # tensor([[ 0.3582,  0.9081, -1.0914,  1.3835, -0.0783],
  #         [ 1.3004, -1.0613, -0.1022, -1.2130,  2.9705],
  #         [-0.0099, -2.1888,  0.3995,  0.8737, -1.0924]])
  ```

## 属性

### 维度[tensor].size()

```python
new_rand_array.size()
# torch.Size([3, 5])   元组 支持左右的元组操作
```

## 操作

### 加法

- 方式1： x+y

  ```python
  new_array+new_array.new_ones(3,5)
  
  #tensor([[2, 2, 2, 2, 2],
          # [2, 2, 2, 2, 2],
          # [2, 2, 2, 2, 2]])
  ```

- 方式2：torch.add(x,y,out=)

  ```python
  torch.add(new_array,new_array.new_ones(3,5))
  
  #tensor([[2, 2, 2, 2, 2],
          # [2, 2, 2, 2, 2],
          # [2, 2, 2, 2, 2]])
  ```

- in-place:  [tensor].add_()

### 索引

- 类似numpy [tensor][x:y,d]

  ```python
  print(new_array[:,1])
  
  # tensor([2, 2, 2])
  ```

### 改变大小

- [tensor].view()

  ```python
  y=new_array.view(15)
  print(y)
  #tensor([2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2])
  ```

### 获取值

- [tensor].item()

  ```python
  # 获取值
  print(new_array[1:2,1].item())
  # 2
  ```
