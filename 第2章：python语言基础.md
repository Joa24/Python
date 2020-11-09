```python
import numpy as np
```

# 2.python语言基础
## 2.2.4内省


```python
# 在一个变量名的前后使用问号(?)可以显示一些关于该对象的概要信息：
b = [1,2,3]
b?
```


```python
# 如果对象是一个函数或实例方法，且文档字符串已经写好，则文档字符串会显示出来：
def add_numbers(a,b):
    """
    Add two number together
    Returns
    ------
    the_sum : type of arguments
    """
    return a + b
```


```python
add_numbers?
```


```python
# 使用双问号 ?? 可以显示函数的源代码：
add_numbers??
```


```python
# ?可以像标准Unix或Windows命令行一样搜索Ipython命名空间。把一些字符和通配符(*)结合在一起，会显示素有匹配通配符表达式的命名：
np.*load*?
```

## 2.3.1.6动态引用、强类型


```python
# isinstance接受一个包含类型的元组，可以检查对象的类型是否在元组中的类型中：
a = 5;b = 4.5
isinstance(a,(int,float))
```




    True



## 2.3.1.8验证是否可迭代


```python
def isiterable(obj):
    try:
        iter(obj)
        return True
    except TypeError: # 不可遍历
        return False
```


```python
isiterable('a string')
```




    True




```python
isiterable(5)
```




    False



## 2.3.1.10二元运算符和比较运算


```python
# 检查两个引用是否指向同一个对象，可以使用is关键字。is not在检查两个对象不同时也有效
a = [1,2,3]
b = a
c = list(a)
a is b
```




    True




```python
a == c
```




    True




```python
# is和is not的常用之处是检查一个变量是否为None
a = None
a is None
```




    True



## 2.3.1.11可变对象和不可变对象


```python
# 列表、字典、Numpy数组是可变对象，可变对象包含的对象和值也可以被修改：
a_list = ['foo',2,[4,5]]
a_list[2] = (3,4)
a_list
```




    ['foo', 2, (3, 4)]




```python
# 字符串、元组是不可变对象
a_tuple = (3,5,(4,5))
a_tuple[1] = 'four'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-19-e25b975618e0> in <module>
          1 # 字符串、元组是不可变对象
          2 a_tuple = (3,5,(4,5))
    ----> 3 a_tuple[1] = 'four'
    

    TypeError: 'tuple' object does not support item assignment


## 2.3.2.2字符串


```python
# python字符串是不可变的，无法修改一个字符串
a = 'this is a string'
a[10] = 'f'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-20-b16ed5fea917> in <module>
          1 # python字符串是不可变的，无法修改一个字符串
          2 a = 'this is a string'
    ----> 3 a[10] = 'f'
    

    TypeError: 'str' object does not support item assignment



```python
b = a.replace('string','long string')
b
```




    'this is a long string'




```python
# 字符串格式化，format方法，可以用来代替字符串中的格式化参数，并产生一个新的字符串：
template = '{0:.2f} {1:s} are worth US${2:d}'
"""
{0:.2f}表示将第一个参数格式化为2位小数的浮点数
{1:s}表示将第二个参数格式化为字符串
{2:d}表示将第三个参数格式化整数
"""
template.format(4.5560,'Argentine Pesos',1)
```




    '4.56 Argentine Pesos are worth US$1'



## 2.3.2.6 None


```python
# None是python的null值类型。如果一个函数没有显示地返回值，则它会隐式地返回None：
a = None
a is None
```




    True




```python
# None还可以作为一个常用的函数参数默认值：
def add_and_maybe_multiply(a,b,c=None):
    result = a + b
    
    if c is not None:
        result = result * c
        
    return result
```

## 2.3.2.7日期和时间


```python
from datetime import datetime,date,time
```


```python
# python中内建的datatime模块，提供了datetime,date,time
dt = datetime(2011,10,29,20,30,21)
dt.day
```




    29




```python
dt.minute
```




    30




```python
# 可以分别使用date和time获取它的date、time对象
dt.date()
```




    datetime.date(2011, 10, 29)




```python
dt.time()
```




    datetime.time(20, 30, 21)




```python
# strftime方法将datetime转换为字符串
dt.strftime('%m/%d/%Y %H:%M')
```




    '10/29/2011 20:30'




```python
# 可以通过strptime函数转换为datetime对象：
datetime.strptime('20091031','%Y%m%d')
```




    datetime.datetime(2009, 10, 31, 0, 0)




```python
# 替代datetime时间序列中的一些值，比如将分钟、秒替换为0:
dt.replace(minute=0,second=0)
```




    datetime.datetime(2011, 10, 29, 20, 0)




```python
# datetime.datetime是不可变类型，会产生新的对象，两个不同的datetime会产生一个datetime.timedalta类型的对象：
dt2 = datetime(2011,11,15,22,30)
delta = dt2 - dt
delta
```




    datetime.timedelta(days=17, seconds=7179)



| 类型 | 描述 |
| --- |--- |
| %Y | 四位的年份|
| %y | 两位的年份 |
| %m | 两位的月份[0,12] |
| %d | 两位的天数[01,31] |
| %H | 小时值(24小时制)[00,23] |
| %I | 小时值(12小时制)[00,12] |
| %M | 两位的分钟值[00,59] |
| %S | 秒值[00,61] |
| %w | 星期值[0(星期天),6] |
| %U | 一年中第几个星期的值[00,53],星期天是每周第一天，第一个星期天前的一周是第0个星期 |
| %W | 一年中第几个星期的值[00,53],星期一是每周第一天，第一个星期一前的一周是第0个星期|
| %z | UTC时区偏置，格式为 +HHMM或 -HHMM；如是是简单市区则为空 |
| %F | %Y-%m-%d的简写 |
| %D | %m/%d/%y的简写 |

## 2.3.3.1 if、elif、else


```python
# 一个if可以接多个elif代码和一个else代码：
x = -1
if x < 0:
    print('It\'s negative')
elif x == 0:
    print('Equal to zero')
elif 0 < x < 5:
    print('Positive but samller than 5')
else:
    print('Positive and larger than or equal to 5')
```

    It's negative



```python
# 进行混合条件判断时，条件判断从左到右，并且在and or两侧的条件会有'短路'现象
a = 5;b = 7
c = 8;d = 4
if a < b or c < d:
    print('Made it')
```

    Made it



```python
# 链式比较
4 > 3 > 2 > 1
```




    True



## 2.3.3.2 for循环


```python
# 用于遍历一个集合或一个迭代器：
"""
for value in collection:
    # 用值做些什么
"""
```




    '\nfor value in collection:\n    # 用值做些什么\n'




```python
# 使用continue关键字可以跳过conitnue后面的代码进入下一次循环，
sequence = [1,2,None,4,None,5]
total = 0
for value in sequence:
    if value is None:
        continue
    total += value
    
total
```




    12




```python
# 使用break关键字可以结束一个for循环。
sequence = [1,2,0,4,6,5,2,1]
total_until_5 = 0
for value in sequence:
    if value == 5:
        break
    total_until_5 += value
    
total_until_5
```




    13




```python
# break值结束最内层的for循环；外层的for循环还会继续运行：
for i in range(4):
    for j in range(4):
        if j > i:
            break
        print((i,j))
```

    (0, 0)
    (1, 0)
    (1, 1)
    (2, 0)
    (2, 1)
    (2, 2)
    (3, 0)
    (3, 1)
    (3, 2)
    (3, 3)


## 2.3.3.3while循环


```python
# while循环会在条件符合时一直执行代码，直到条件判断为False或显式地以break结尾时才结束：
x = 256
total =0
while x > 0:
    if total > 500:
        print(x,total)
        break
    total += x
    x = x // 2
```

    4 504


## 2.3.3.5range


```python
# range函数返回一个迭代器，生成一个等差整数序列
range(10)
```




    range(0, 10)




```python
list(range(10))
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
list(range(0,20,2))
```




    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]




```python
list(range(5,0,-1))
```




    [5, 4, 3, 2, 1]




```python
# 用于根据序列的索引
val = 0
seq = [1,2,3,4]
for i in range(len(seq)):
    val += seq[i]
val
```




    10



## 2.3.3.6三元表达式


```python
# 将if-else联合起来：
"""
value = true expr if condition else false-expr
if condition:
    value = true-expr
else:
    value = false-expr
"""
x = 5
'Non-negative' if x > 0 else 'Negative'
```




    'Non-negative'




```python

```
