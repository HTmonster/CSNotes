# python2 与 python3 的区别

#### 核心类差异

|      比较项      |            python2             |         python3         |
| :--------------: | :----------------------------: | :---------------------: |
| **默认编码方式** | ASCII string类型（str unicode) |         unicode         |
|   **引入方式**   |            相对引入            |        绝对引入         |
|      **类**      |             老式类             | 新式类（必须继承object) |
|     **缩进**     |    1 tab= 8 space 可以共存     |    tab space不能共存    |

#### 废弃类差异

| python2                                        | python3            |
| ---------------------------------------------- | ------------------ |
| print 语句                                     | print函数          |
| exec语句                                       | exec函数           |
| execfile                                       | 废弃               |
| <>                                             | 废弃 !=            |
| long整型                                       | 废弃 使用int       |
| xrange                                         | 废弃 使用range     |
| 迭代器 next函数                                | next(iterator)     |
| 字典对象 keys() values() item() zip() 返回list | 不再返回list       |
| raw_input()                                    | 废弃 使用 input    |
| 字典对象 has_key                               | 废弃 使用in        |
| file函数                                       | 废弃 使用open      |
| 异常 StandardError                             | 废弃 使用Exception |

#### 修改类差异

| 比较项            | python2                                                      | python3                                                      |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 浮点数除法 /   // | /：结果为整形 若有一个浮点数 则结果为浮点数  //:返回结果的最大整数 | /：真除法 //：同python2                                      |
| 异常              | `raise IOError,"file error"#抛出异常``except NameError,err: #捕捉异常` | `raise IOError("file error")#抛出异常``except NameError as err: #捕捉异常` |
| for循环变量       | 会修改外部同名称变量                                         | 不会修改                                                     |
| round函数         | 返回 float                                                   | 返回int                                                      |
| 比较操作          | 任意两个对象                                                 | 同一数据类型对象                                             |

