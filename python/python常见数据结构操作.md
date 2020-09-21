# python常见数据结构操作

#### 列表List操作

```python
1、cmp(list1, list2)：比较两个列表的元素 
2、len(list)：列表元素个数 
3、max(list)：返回列表元素最大值 
4、min(list)：返回列表元素最小值 
5、list(seq)：将元组转换为列表 
列表操作包含以下方法:
1、list.append(obj)：在列表末尾添加新的对象
2、list.count(obj)：统计某个元素在列表中出现的次数
3、list.extend(seq)：在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）
4、list.index(obj)：从列表中找出某个值第一个匹配项的索引位置
5、list.insert(index, obj)：将对象插入列表
6、list.pop(obj=list[-1])：移除列表中的一个元素（默认最后一个元素），并且返回该元素的值
7、list.remove(obj)：移除列表中某个值的第一个匹配项
8、list.reverse()：反向列表中元素
9、list.sort([func])：对原列表进行排序
```



#### 字典dict操作

**一.常见方法**

```python
D.clear()                              #移除D中的所有项  
D.copy()                               #返回D的副本  
D.fromkeys(seq[,val])                  #返回从seq中获得的键和被设置为val的值的字典。可做类方法调用  
D.get(key[,default])                   #如果D[key]存在，将其返回；否则返回给定的默认值None  
D.has_key(key)                         #检查D是否有给定键key  
D.items()                              #返回表示D项的(键，值)对列表  
D.iteritems()                          #从D.items()返回的(键，值)对中返回一个可迭代的对象  
D.iterkeys()                           #从D的键中返回一个可迭代对象  
D.itervalues()                         #从D的值中返回一个可迭代对象  
D.keys()                               #返回D键的列表  
D.pop(key[,d])                         #移除并且返回对应给定键key或给定的默认值D的值  
D.popitem()                            #从D中移除任意一项，并将其作为(键，值)对返回  
D.setdefault(key[,default])            #如果D[key]存在则将其返回；否则返回默认值None  
D.update(other)                        #将other中的每一项加入到D中。  
D.values()                             #返回D中值的列表
```

**二、创建字典的五种方法**
方法一: 常规方法    
代码如下: 

```python
# 如果事先能拼出整个字典，则此方法比较方便
>>> D1 = {'name':'Bob','age':40}
```

方法二: 动态创建 
 如果需要动态地建立字典的一个字段，则此方法比较方便
```python
>>> D2 = {}  
>>> D2['name'] = 'Bob'  
>>> D2['age']  =  40  
>>> D2  
{'age': 40, 'name': 'Bob'} 
```
方法三:  dict--关键字形式       

```python
# 代码比较少，但键必须为字符串型。常用于函数赋值

>>> D3 = dict(name='Bob',age=45)  
>>> D3  
  {'age': 45, 'name': 'Bob'} 

```

方法四: dict--键值序列 

代码如下:

```python
# 如果需要将键值逐步建成序列，则此方式比较有用,常与zip函数一起使用
>>> D4 = dict([('name','Bob'),('age',40)])  
>>> D4  
{'age': 40, 'name': 'Bob'} 

或
代码如下:
>>> D = dict(zip(('name','bob'),('age',40)))  
>>> D  
{'bob': 40, 'name': 'age'}  
```

方法五: dict--fromkeys方法

```python
# 如果键的值都相同的话,用这种方式比较好，并可以用fromkeys来初始化
代码如下:
>>> D5 = dict.fromkeys(['A','B'],0)  
>>> D5  
{'A': 0, 'B': 0}  
如果键的值没提供的话，默认为None

 代码如下:
 >>> D3 = dict.fromkeys(['A','B'])  
>>> D3  
{'A': None, 'B': None}  

```

**三、字典中键值遍历方法**

```python
 D = {'x':1, 'y':2, 'z':3}          # 方法一  
for key in D:  
    print key, '=>', D[key]    
    
y => 2  
x => 1  
z => 3  
for key, value in D.items():       # 方法二  
    print key, '=>', value     
    
y => 2  
x => 1  
z => 3 

 for key in D.iterkeys():           # 方法三  
    print key, '=>', D[key]    
    
y => 2  
x => 1  
z => 3  
for value in D.values():           # 方法四  
    print value   
2  
1  
3  
for key, value in D.iteritems():   # 方法五  
    print key, '=>', value  
- y => 2  
x => 1  
z => 3

```



#### 字符串str操作

```python
1) 判断类型 - 9
    string.isspace()	如果 string 中只包含空格，则返回 True
    string.isalnum()	如果 string 至少有一个字符并且所有字符都是字母或数字则返回 True
    string.isalpha()	如果 string 至少有一个字符并且所有字符都是字母则返回 True
    string.isdecimal()	如果 string 只包含数字则返回 True，全角数字
    string.isdigit()	如果 string 只包含数字则返回 True，全角数字、⑴、\u00b2
    string.isnumeric()	如果 string 只包含数字则返回 True，全角数字，汉字数字
    string.istitle()	如果 string 是标题化的(每个单词的首字母大写)则返回 True
    string.islower()	如果 string 中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True
    string.isupper()	如果 string 中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True
2) 查找和替换 - 7
    方法	说明
    string.startswith(str)	检查字符串是否是以 str 开头，是则返回 True
    string.endswith(str)	检查字符串是否是以 str 结束，是则返回 True
    string.find(str, start=0, end=len(string))	检测 str 是否包含在 string 中，如果 start 和 end 指定范围，则检查是否包含在指定范围内，如果是返回开始的索引值，否则返回 -1
    string.rfind(str, start=0, end=len(string))	类似于 find()，不过是从右边开始查找
    string.index(str, start=0, end=len(string))	跟 find() 方法类似，不过如果 str 不在 string 会报错
    string.rindex(str, start=0, end=len(string))	类似于 index()，不过是从右边开始
    string.replace(old_str, new_str, num=string.count(old))	把 string 中的 old_str 替换成 new_str，如果 num 指定，则替换不超过 num 次
3) 大小写转换 - 5
    方法	说明
    string.capitalize()	把字符串的第一个字符大写
    string.title()	把字符串的每个单词首字母大写
    string.lower()	转换 string 中所有大写字符为小写
    string.upper()	转换 string 中的小写字母为大写
    string.swapcase()	翻转 string 中的大小写
4) 文本对齐 - 3
    方法	说明
    string.ljust(width)	返回一个原字符串左对齐，并使用空格填充至长度 width 的新字符串
    string.rjust(width)	返回一个原字符串右对齐，并使用空格填充至长度 width 的新字符串
    string.center(width)	返回一个原字符串居中，并使用空格填充至长度 width 的新字符串
5) 去除空白字符 - 3
    方法	说明
    string.lstrip()	截掉 string 左边（开始）的空白字符
    string.rstrip()	截掉 string 右边（末尾）的空白字符
    string.strip()	截掉 string 左右两边的空白字符
6) 拆分和连接 - 5
    方法	说明
    string.partition(str)	把字符串 string 分成一个 3 元素的元组 (str前面, str, str后面)
    string.rpartition(str)	类似于 partition() 方法，不过是从右边开始查找
    string.split(str="", num)	以 str 为分隔符拆分 string，如果 num 有指定值，则仅分隔 num + 1 个子字符串，str 默认包含 '\r', '\t', '\n' 和空格
    string.splitlines()	按照行('\r', '\n', '\r\n')分隔，返回一个包含各行作为元素的列表
    string.join(seq)	以 string 作为分隔符，将 seq 中所有的元素（的字符串表示）合并为一个新的字符串
```



 