# python 垃圾回收 Garbage collection

#### 概要

- **引用计数**为主
- **标记-清除**和**分代收集**为辅

#### GC系统职责

- 为新生对象分配内存
- 识别垃圾对象并回收

#### 引用计数机制

- Pyobject结构体（C语言） ob_refcnt 引用计数

- 操作

  - 新引用：计数增加

  - 解除引用：计数减小

  - 引用为0：删除

    |          优点           |         缺点         |
    | :---------------------: | :------------------: |
    |          简单           | 消耗资源【引用计数】 |
    | 实时性：无引用 立马删除 |       循环引用       |
    |        内存分担         |                      |

#### 标记-清除算法

- 能够引用其他对象的对象称为容器
- 容器间才能形成循环引用
- 将每个容器链接到双向链表中
  - 对于每个容器对象，设置一个gc_refs值，将其初始化为对象的引用计数值
  - 找对象容器，找到引用的对象，将其引用值减1
  - 遍历所有后，gc_refs值大于0的对象｛存在非循环引用｝，放在另一个集合
  - 释放剩下的对象｛无法到达的对象｝

#### 分代回收

- 所有对象依据“生存时间” 分为3代

  - 0代：新创建的对象   【经过一次 垃圾回收后 放入1代】

  - 1代: 经过一次垃圾回收后 仍然存在 放入2代

  - 2代：垃圾回收

- 回收频率

- 触发垃圾回收的条件

  - 到达垃圾回收阈值,python虚拟机执行
  - 手动调用gc.collect()
  - python虚拟机退出时

#### gc 模块

- python标准库

- 提供垃圾回收接口

  ```python
  #开启关闭与判断开启结束状态
  gc.enable()
  gc.disable()
  gc.isenable()
  
  #执行垃圾回收
  gc.collection()
  
  #设计及获取阈值
  gc.set_threshold()
  gc.get_threshold()
  
  #返回被垃圾回收器管理的对象
  gc.get_objects()
  
  #获得对象直接指向的对象
  gc.get_referents(*obj)
  gc.get_referrers(*obj)
  
  #设置调试模式
  gc.set_debug(flags)
  ```

#### 内存泄露

- 情况一：对象被另一个生命周期特别长的对象所引用
  - 例如：网络服务器 单例模式  一个链接不再使用后 没有进行删除
- 情况二：循环引用的对象定义了`__del__`函数