# python自省

> 参考：
>
> https://www.cnblogs.com/lmh001/p/9559358.html
>
> http://www.woola.net/detail/2016-08-28-python-object-introspection.html

#### 介绍

- 自省是python的一种独特能力
- 面向对象编程中，使程序能够在**运行**时候获得**对象的类python型**
- **检查事物是什么，知道他能做什么**

#### 对象属性内建方法

- `dir([obj])` : 返回obi属性名的列表（除特殊属性），obj默认当前模块对象
- `hasattr(obj,attr)`: 查看对象是否有该属性
- `getattr(obj,attr)`: 获得对象属性的值
- `setattr(obj,attr)`: 设置对象属性的值

#### 对象内建方法

- `isinstance(object,classinfo)`: 检查是不是classinfo列出的类型
- `issubclass(class,classinfo)`: 检查是不是classinfo的子类