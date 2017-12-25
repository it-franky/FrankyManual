
#### README

* 视频学习：小甲鱼零基础入门学Python | python从入门到精通视频(马哥)

* 纸质书：Python基础教程(第2版)

* 电子书：Python基础教程(第2版)

* 项目开发：OPMS,ElephantIsland


#### 知识体系图

![](http://olkk02yki.bkt.clouddn.com/Python_20170625111036.png)

>注意：如果熟悉其他计算机语言，可能会习惯于每行以分号结束。Python则不用，一行就是一行，不管多少。如果喜欢的话，可以加上分号，但是不会有任何作用（除非同一行还有更多的代码），而且这也不是通行的做法。

#### 开发环境

1. virtualenv用于创建独立的Python环境，多个Python相互独立，互不影响，它能够：

- 在没有权限的情况下安装新套件

- 不同应用可以使用不同的套件版本

- 套件升级不影响其他应用。

2. Virtaulenvwrapper是virtualenv的扩展包，用于更方便管理虚拟环境，它可以做：

- 将所有虚拟环境整合在一个目录下

- 管理（新增，删除，复制）虚拟环境

- 快速切换虚拟环境

**Windows下安装**

```
pip install virtualenvwrapper-win 

## Optional: Add anenvironmentvariable WORKON_HOME to specify the path to store environments. By default, this is %USERPROFILE%\Envs.
## 默认是在C:\Users\Administrator\Envs目录下
## Windows下设置WORKON_HOME环境变量可参考JAVA_HOME环境变量设置
```

命令列表

workon:列出虚拟环境列表

lsvirtualenv:同上

mkvirtualenv :新建虚拟环境

workon [虚拟环境名称]:切换虚拟环境

rmvirtualenv :删除虚拟环境

deactivate: 离开虚拟环境

```python

-3 ** 2
-9

(-3) ** 2
9

```
注意，幂运算符比取反（一元减运算符）的优先级要高，所以-3\*\*2等同于-(3\*\*2)。如果想计算(-3)**2，就需要显式说明。

> 注意，

> 注意，nan是一个特殊值的简写，意思是"not a number"（非数值）

str、repr和反引号是将Python值转换为字符串的3种方法。函数str让字符串更易于阅读，而repr(和反引号)则把结果字符串转换为合法的Python表达式。


#### 变量

1. 变量名可以包括字母、数字和下划线（_）。变量不能以数字开头，所以Plan9是合法变量名，而9Plan不是。

2. 在使用变量之前，需要对其先赋值。

3. 字母可以是大写或小写，但大小写是不同的。也就是说franky和Franky对Python来说是完全不同的两个名字。

4. 等号(=)是赋值的意思，左边是名字，右边是值，不可写反。

#### 字符串

- 字符串就是引号内的一切东西，也叫做文本，文本和数字是截然不同的。

- 创建一个字符串，就要在字符两边加上引号，可以是单引号或者双引号。

- 字符串中出现单引号或双引号，一种比较常用的就是使用转义符号（\）对字符串中的引号进行转义。

```python
'Let\'s go!'
```

- 原始字符串：如果一个字符串中需要转义的字符较多就需要加很多个反斜杠，使用原始字符串只需要在字符串前边加一个英文字母r即可。**注意：原始字符串最后不能加'\'**

```python
>>>str=r'C:\now'
```

- 三重引号字符串：用于跨越多行的字符串，引号可以是单引号也可以是双引号。

```python
str='''我喜欢python
我喜欢python
我喜欢python
'''

str="""我喜欢python
我喜欢python
我喜欢python
"""

```

#### String Methods

函数|描述
---|---
capitalize()|Return a copy of the string with its first character capitalized and the rest lowercased.
casefold()|把整个字符串的所有字符改为小写
center(width[, fillchar])|Return centered in a string of length width. Padding is done using the specified fillchar (default is an ASCII space). The original string is returned if width is less than or equal to len(s).
count(sub[, start[, end]]) |Return the number of non-overlapping occurrences of substring sub in the range [start, end]. Optional arguments start and end are interpreted as in slice notation.
encode(encoding="utf-8", errors="strict") |
endswith(suffix[, start[, end]]) |Return True if the string ends with the specified suffix, otherwise return False. suffix can also be a tuple of suffixes to look for. With optional start, test beginning at that position. With optional end, stop comparing at that position.
expandtabs(tabsize=8) |
find(sub[, start[, end]]) |Return the lowest index in the string where substring sub is found within the slice s[start:end]. Optional arguments start and end are interpreted as in slice notation. Return -1 if sub is not found.
index(sub[, start[, end]]) |Like find(), but raise ValueError when the substring is not found.
islower() |Return true if all cased characters in the string are lowercase and there is at least one cased character, false otherwise.
istitle() |Return true if the string is a titlecased string and there is at least one character, for example uppercase characters may only follow uncased characters and lowercase characters only cased ones. Return false otherwise.
isupper()|Return true if all cased characters in the string are uppercase and there is at least one cased character, false otherwise
join(iterable) |Return a string which is the concatenation of the strings in the iterable iterable. A TypeError will be raised if there are any non-string values in iterable, including bytes objects. The separator between elements is the string providing this method.
ljust(width[, fillchar]) |Return the string left justified in a string of length width. Padding is done using the specified fillchar (default is an ASCII space). The original string is returned if width is less than or equal to len(s).
lower() |Return a copy of the string with all the cased characters [4] converted to lowercase.
lstrip([chars]) |Return a copy of the string with leading characters removed. The chars argument is a string specifying the set of characters to be removed. If omitted or None, the chars argument defaults to removing whitespace. The chars argument is not a prefix; rather, all combinations of its values are stripped.
partition(sep) |Split the string at the first occurrence of sep, and return a 3-tuple containing the part before the separator, the separator itself, and the part after the separator. If the separator is not found, return a 3-tuple containing the string itself, followed by two empty strings.
replace(old, new[, count]) |Return a copy of the string with all occurrences of substring old replaced by new. If the optional argument count is given, only the first count occurrences are replaced.


#### Python的数值类型

布尔类型True = 1 ; False = 0

```python
True + True
2
>>>
True * False
0
True == 1
True

False == 0
True
>>>
```

#### Python的比较操作符

符号|含义
---|---
>  | 左边大于右边
>= | 左边大于等于右边
<  | 左边小于右边
<= | 左边小于等于右边
== | 左边等于右边
!= | 左边不等于右边

#### Python的逻辑操作符

符号|含义
---|---
AND| 


#### Python的条件分支语法

```python

if 条件 :
    条件为真（True）执行的操作
else :
    条件为假（False）执行的操作

while 条件 :
    条件为真（True）执行的操作
```

#### 断言（assert）

assert这个关键字我们称之为“断言”，当这个关键字后边的条件为假的时候，程序自动崩溃并抛出AssertionError的异常。

一般来说我们可以用Ta在程序中置入检查点，当需要确保程序的某个条件一定为真才能让程序正常工作的话，assert关键字就非常有用了。


#### For 循环

```python
for 目录 in 列表 
    循环体
```

```python
#!/usr/bin/env python
#coding=utf-8

#根据给定的年月日以数字形式打印日期

months = [
    'January',
    'February',
    'March',
    'April',
    'May',
    'June',
    'July',
    'August',
    'September',
    'October',
    'November',
    'December'
]

#以1~31的英文序数后两位作为结尾的列表

endings = ['st','nd','rd'] + 17 * ['th'] \
        + ['st','nd','rd'] + 7 * ['th'] \
        + ['st']

year = raw_input('Year: ')
month = raw_input('Month(1-12): ')
day = raw_input('Day(1-31): ')

month_number = int(month)
day_number = int(day)

#将月份和天数减1，以获得正确的索引
month_name = months[month_number-1]
ordinal = day + endings[day_number-1]

print month_name + ' ' + ordinal + ',' + year

```

>这里有点英语的小知识

```
第1 first 1st 
第2 second 2nd 
第3 third 3rd 
第4 fourth 4th 
第5 fifth 5th 
第6 sixth 6th 
第7 seventh 7th 
第8 eighth 8th 
第9 ninth 9th 
第10 tenth 10th 
第11 eleventh 11th 
第12 twelfth 12th 
第13 thirteenth 13th 
第14 fourteenth 14th 
第15 fifteenth 15th 
第16 sixteenth 16th 
第17 seventeenth 17th 
第18 eighteenth 18th 
第19 nineteenth 19th 
第20 twentieth 20th 
第21 twenty-first 21st 
第22 twenty-second 22nd 
第23 twenty-third 23rd 
第24 twenty-fourth 24th 
第25 twenty-fifth 25th 
第26 twenty-sixth 26th 
第27 twenty-seventh 27th 
第28 twenty-eighth 28th 
第29 twenty-ninth 29th 
第30 thirtieth 30th 
第31 thirty-first 31st
```

分片操作的实现需要提供两索引作为边界，第1个索引的元素是包含在分片内的，而第2个则不包含在分片内。


### 语句
#### print
#### import
#### 赋值语句

##### 隐式赋值
import,from,def,class,for,函数参数

##### 序列解包

```python
# 当赋值符号(=)的左侧为元组或列表时，Python会按照位置把右边的对象和左边的目标自左向右逐一进行配对儿
>>> x,y,z = 1,2,3
>>> print(x,y,z)
1 2 3

>>> x,y,z = [1,2,3]
>>> print(x,y,z)
1 2 3

# 个数不同时会触发异常
>>> x,y,z = 1,2
Traceback (most recent call last):
  File "<pyshell#15>", line 1, in <module>
    x,y,z = 1,2
ValueError: not enough values to unpack (expected 3, got 2)
>>> 
>>> x,y,z = 1,2,3,4
Traceback (most recent call last):
  File "<pyshell#16>", line 1, in <module>
    x,y,z=1,2,3,4
ValueError: too many values to unpack (expected 3)

# 星号运算符
>>> x,y,*z=[1,2,3,4,5]
>>> print(x,y,z)
1 2 [3, 4, 5]
>>> 
>>> x,y,*z=1,2,3,4,5
>>> print(x,y,z)
1 2 [3, 4, 5]

# 可以使用切片的方式进行赋值
>>> l1 = [1,2,3,4,5]
>>> x,y,z=l1[0],l1[1],l1[2:]
>>> print(x,y,z)
1 2 [3, 4, 5]
```

##### 链式赋值
```python
x = y = 3
```
##### 增强赋值

```python
# +=,-=,*=,/=,//=,%=
x = 2
x += 1
x *= 3
```

#### 函数、方法调用

#### 条件

##### 条件测试
False None 0 "" () [] {} 会被解释器看作假(false)。

##### if词句

##### 三元运算符

a if b else c

expression1 if boolean_expression else expression2


#### 循环

##### while循环

```python
while boolean_expression:
    while_suite
else:
    else_suite

```

##### for循环

##### 迭代工具
range(),xrange(),zip()-并行迭代

#### pass,del,exec,eval
#### break,continue,def,return,yield,global,raise
assert
with/as


### sys.getrefcount()

增加对象的引用计数场景：
    对象创建时
    将对象添加进容器时，类似list.append()
    当对象被当作参数传递给函数时
    为对象创建另外变量名

减少引用计数：
    引用此对象的某变量名被显式销毁：del x
    给引用对象的某变量名重新赋值
    从容器中移除对象时，类似list.pop()
    容器本身被销毁


### 迭代器

iterable 可迭代对象，实现了__iter__()或__getitem__()方法的类

__iter__方法会返回一个迭代器(iterator)，所谓的迭代器就是具有__next__方法（这个方法在调用时不需要任何参数）的对象。在调用__next__方法时，迭代器会返回它的下一个值。如果__next__方法被调用，但迭代器没有值可以返回，就会引发一个StopIteration异常。

注意：正式的说法是，一个实现了__iter__方法的对象是可迭代的，一个实现了__next__方法的对象则是迭代器。

### 生成器

### enumerate



### 文件和流

#### 打开文件
#### 文件模式


### 函数
def functionName(parameters):
    suite

#### 全局函数：定义在模块中
#### 局部函数：嵌套于其它函数中
#### lambda函数：表达式，匿名函数
#### 方法：与特定数据类型关联的函数，并且只能与数据类型关联一起使用。