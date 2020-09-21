# python陷阱

#### 函数默认参数

- 函数默认参数在**定义**时求值 而不是引用时候

  ```python
  import time
  
  def func(when=time.time()):
      return when
  
  ###########验证#############
  func()
  15032848.3124378
  
  func()
  15032848.3124378
  ```

  

- 【解决方法】：**默认参数设置为None**



####  x += y vs x = x + y

- 一般时候是等价的
- 【区别】：x = x + y 指向了**新对象**



#### 只有一个元素的元组

- a=(1,)而不是a=(1)
- 后者是int类型



#### 访问列表时候修改列表

- 访问列表，删除列表时候，列表在动态缩小

  ```python
  　　>>> def modify_lst(lst):
  
  　　...     for idx, elem in enumerate(lst):
  
  　　...             if elem % 3 == 0:
  
  　　...                     del lst[idx]
  
  
  #运行时候
  
  　　>>> lst = [1,2,3,6,5,4]
  
  　　>>> modify_lst(lst)
  
  　　>>> lst
  
  　　[1, 2, 6, 5, 4]
  ```

  

#### 闭包与lambda

- python属性查找规则 （LEGB local enclousing gloabal bulitin)

- 【原因】：闭包是迟绑定，在内部函数被**调用时候才进行查询**

  ```python
  def create_multipliers():
      return [lambda x:i*x for i in range(5)]
  
  #############调用##############
  create_multipliers(2) #[8,8,8,8,8]
  
  ```

- 【解决方法】：改闭包作用域为局部作用域 `[lambda x i=i:i*x for i in range(5)]`



#### ++i --i

- 这两个运算后值不变
