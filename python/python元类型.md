# python元类型

>参考：
>
>https://www.cnblogs.com/intimacy/p/8119449.html
>
>http://python.jobbole.com/88795/

#### 前语

- 无处不对象
- 对象属性：id、类型、值
- 所有对象都是类创建出来的

#### 元类

- python一切皆对象
- 元类就是负责来创建类的的东西
- 元类是类，所有的类都是由它来创建，(类也是对象)
- type其实就是一个元类（内建元类）

#### type()函数

- 一个参数：返回类型
- 三个参数：返回新的类型对象 【 动态创建对象】

```python
>>> type(1)
<type 'int'> #返回类型

>>> type(type(i))
<type 'type'> #type的类型是type
```

#### 元类的作用

- 创建API

  ```python
  #Django ORM模型
  class Person(models.Model):
      name=models.CharField()
      age=models.IntegerFiled() #得到了一个IntegerFiled对象
  ```

#### 动态创建类

- 方法一：用`class Foo()` 创建返回

- 方法二：用 `type(类名，父类，属性）`来创建

  ```python
  #两者之间转换
  class Foo(object):
  	  bar = True
  
  Foo = type('Foo', (), {'bar':True})
  ```

#### `__metaclass__`属性

- 创建类的时候可以为其添加`__metaclass__`属性

- 通过指定的`metaclass`创建的具体函数

- `metaclass`指定内容：1. type  2. type子类 

  ```python
  #python 2.x
  class Foo(object):
      __metaclass__ =something
      [...]
  
  #python 3.x
  class Foo(object,metaclass=something..):
      [...]
  ```

  |          new           |    init    |
  | :--------------------: | :--------: |
  |        静态方法        |  实例方法  |
  | 返回创建的实例 cls实例 |   不返回   |
  |       创建新实例       | 初始化实例 |

- python内部创建类的机理

  - 在类定义代码中查找`__metaclass__`属性
  - 若找到：用指定的metaclass创建Foo对象
  - 找不到：MODULE(模块级别)找并创建Foo类对象（老式类，未继承父类的类）
  - 还找不到：通过Bar(第一个父类)的metaclass(可能是type)来创建类

- 【注意】：`__metaclass__`属性不会被继承  而`__class__`会被继承

- 【总结】`metaclass`的作用：

  - 拦截类的生成
  - 修改类
  - 返回修改后的类

#### 自定义元类

- 应用场景：API 创建和上下文相符合的类

- 实例：让所有模块下的类的属性都要大写

- 思路：

  - 所有的模块通过指定的metaclass创建
  - 指定metaclass让所有的属性大写

  ```python
  #拦截对象的生成并修改所有的属性为大写
  def upper__attr(future__calss__name,future_class_parents,future_class_attr):
      '''
      	返回一个类对象，其所有的属性都是大写
      '''
      
     #选不以__开头的对象 并将其大写
  	uppercase_attr={}
      for name,val in future_class_attr.items():
          if not name.startswith('__'):
              uppercase_attr[name.upper()]=val
          else:
              uppercase_attr[name]=val
      
      #使用type创建定制对象 并返回
      return type(future_class_name,future_class_parents,uppercase_attr)
  
  #影响模块里的所有类
  __metaclass__ = upper_attr
  
  class Foo():
      #虽然 不会影响带 "object"的类
      #但是可以通过 定义 __metaclass__来实现
      onattr="myattr"
  
  #####################结果验证#########################
  hasattr(Foo,'onattr')  #false
  hasattr(Foo,'ONEATTR') #ture
  Foo().ONEATTR          #myattr
  
  
  
  #########################metaclass类##################
  # 重写__new__方法
  # 属性名字简写
  # super关键字
  class UpperAttrMetaclass(type):
      def __new__(cls, clsname, bases, dct):
  
          uppercase_attr = {}
          for name, val in dct.items():
              if not name.startswith('__'):
                  uppercase_attr[name.upper()] = val
              else:
                  uppercase_attr[name] = val
  
          return super(UpperAttrMetaclass, cls).__new__(cls, clsname, bases, uppercase_attr)
  ```

  

#### 其他相关方法

```python
class god():
    pass

#创建对象
Chinese=type('person',(god,),{"country":'china'})

#方法1 __class__ 查看对象由那个生成
Chinese().__class__  #<class '__main__.person'>
Chinese().__class___.__class__ #<type 'type'>

#方法2 __bases__ 查看对象的父类 字
chinese.__bases__  #（<class '__main__.god'>

#方法3 __dict__ 查看类字典数据
chinese.__dict__  #{'__module__': '__main__', 'country: 'china', '__doc__': None}

```



#### 版本区别

|                    py2.x                    |              py3.x               |
| :-----------------------------------------: | :------------------------------: |
|            新类需要继承object类             |         默认继承object类         |
| `class Foo(object):__metaclasss__=someting` | `class  Foo(metaclass=someting)` |



#### 总结

看到一篇很好的博客，里面用来道家思维解释。

> 道生一，一生二，二生三，三生万物

- **道**就是`type`
- **一**就是 `metaclass`元类，类生成器
- **二**就是 `class`类 实例生成器
- **三**就是 `instance`实例
- **万物**就是 各种属性 方法
