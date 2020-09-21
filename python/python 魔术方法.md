# python 魔术方法

> 参考：
>
> https://segmentfault.com/a/1190000007256392

#### 简介

- 被 __ 包围的方法 称为魔术方法

#### 构造与初始化

- `__init__`      对象初始化时候调用  将传入的参数初始化实例	  返回None
- `__new__`        对象初始化时候调用   创建类并返回类的实例      返回实例

#### 属性访问与控制

- `__getattr__(self,name)`  定义访问一个不存在的属性时的行为

- `__setattr__(self,name,value)` 定义对属性进行复制和修改操作时的行为

- `__delattr__(self,name)` 定义删除属性的行为

- `__getattribute__(self,name)` 定义自己的属性被访问时候的行为

  ```python
  class Access(object):
  
      def __getattr__(self, name):
          print '__getattr__'
          return super(Access, self).__getattr__(name)
  
      def __setattr__(self, name, value):
          print '__setattr__'
          return super(Access, self).__setattr__(name, value)
  
      def __delattr__(self, name):
          print '__delattr__'
          return super(Access, self).__delattr__(name)
  
      def __getattribute__(self, name):
          print '__getattribute__'
          return super(Access, self).__getattribute__(name)
  
  access = Access()
  access.attr1 = True  # __setattr__调用
  access.attr1  # 属性存在,只有__getattribute__调用
  try:
      access.attr2  # 属性不存在, 先调用__getattribute__, 后调用__getattr__
  except AttributeError:
  ```

  #### 描述器对象

  描述器对象不能独立存在，需要被另一个所有者持有。

  描述器要实现以下的三种方法

  - `__get__(self,instance,owner)`  对其读值时候调用
  - `__set__(self,instance,value)`  对其修改值时候调用
  - `__delete__(self,instance)` 对其删除时候调用

    ```python
    class Meter(object):
        '''Descriptor for a meter.'''
        def __init__(self, value=0.0):
            self.value = float(value)
        def __get__(self, instance, owner):
            return self.value
        def __set__(self, instance, value):
            self.value = float(value)
    
    class Foot(object):
        '''Descriptor for a foot.'''
        def __get__(self, instance, owner):
            return instance.meter * 3.2808
        def __set__(self, instance, value):
            instance.meter = float(value) / 3.2808
    
    class Distance(object):
        meter = Meter()
        foot = Foot()
    
    d = Distance()
    print d.meter, d.foot  # 0.0, 0.0
    d.meter = 1
    print d.meter, d.foot  # 1.0 3.2808
    d.meter = 2
    print d.meter, d.foot  # 2.0 6.5616
    ```

   
