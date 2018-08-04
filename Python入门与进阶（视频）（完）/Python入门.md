### 1.基本数据类型

Number

整数: int

浮点数: float

type() 判断数据类型

除法用两次会省略小数变为整型

5/2 是float 2.5

5//2 是int 2

但是除数是小数还是会是float

5//2.0 是float 2.0

二进制用 0b开头 0b10 => 2

八进制用 0o 0o11 9

十六进制0x 0x1F 31

复数在后面加j

bin() 转换为二进制

int() 转为十进制

hex() 转为十六进制

oct()转为八进制

boolean 类型在py里属于数字的一种

True False 开头要大写

bool() 把参数转为布尔值

空字符串，0，[],{},None 返回false

js 中 [],{} 会返回true



字符串 str



三引号: 三个单引号或者三个单引号，多行字符串

单双引号换行用 \ 结尾

字符串前面加r 就不是普通字符串了 就是原始的字符串 里面的特殊符号也不会被转译了



字符串可以用 * 乘

可以用下标取 'hello'[0] 是h 'hello'[-1] 是d

‘hello’[0:4] 第二个数字结束位置之前的 hell

'hello'[0:-2] hel



省略第一个就是从开头开始

'hello'[:2] he



省略第二个就是一直到末尾

'hello'[1:] ello



第三个参数是步长



列表 list

[1,2,3,4]

用 下标取返回的是元素 [0]  => 1

用引号返回的是列表 [-1:]  => [4]

列表可以用 + *



元组 tuple

（1,2,3,4）

用 下标取返回的是元素 [0]  => 1

用引号返回的是列表 [-1:]  => (4)

可以用 + *

如果元组里面就一个元素 用type的时候会将括号识别为运算优先作用 type((1))

要识别需加个逗号 type((1,))



字符串 列表 元组都可看做 序列

序列都可以使用[]来取值 

[] 里用 : 称为切片

序列里每个元素都会分配序号

3 in [1,2,3] 返回 True

3 not in [1,2,3] 返回 False

len() 参数序列 返回长度

max() min() 取大取小  对字符串就是判断 ASCII 码

ord() 查看字符的ascll码



集合 set

无序 无重复

支持 len(), in, not in

{1,2,3}

集合用减号 求差值

{1,2,3} - {3}   {1,2}

用 & 求交

{1,2,3} & {3} {3}

用 | 求并

{1,2,3,4} | {4,5}    {1,2,3,4,5}

要定义空的集合要用 set() 不能{}



字典 dict

{'Q': '新月打击', 'W':'苍白之瀑'}

{'Q': '新月打击', 'W':'苍白之瀑'}['Q']   =>  '新月打击'

key 不能相同

key 必须是不可变的类型 如字符串,数字,元组

空字典 {}

![img](https://github.com/boenfu/BoenNote/blob/master/Python%E5%85%A5%E9%97%A8%E4%B8%8E%E8%BF%9B%E9%98%B6%EF%BC%88%E8%A7%86%E9%A2%91%EF%BC%89%EF%BC%88%E5%AE%8C%EF%BC%89/py1.png)





### 2.变量

只能字母数字下划线

字符串，数组是值类型 不可改变

元组也是值类型 不可改变的(但是元组内部有引用类型的值，引用类型部分是可改变的)

id() 显示变量在内存的地址 类似java的hashcode

一般用16进制来表示地址比较合适 虽然我也不知道为什么

hex(id())

### 3.运算符

2**3 平方 2的3次方 8



算数运算符 赋值运算符 关系运算符 逻辑运算符 成员运算符 身份运算符 位运算符

Python 没有自增自减

逻辑运算符

​	and 且

​	or 或

​	not 非

not > and > or 优先级

​	短路运算 能确定表达式结果就返回了

成员运算符

​	in 

​	not in

​	对于 字典来说 是判断键

身份运算符

​	is 比较两个变量的身份是否相等(内存地址)

​	 而 == 比较的是值是否相等

​	1 is 1.0 false

​	1 == 1.0 true

​	

对象的三个特征 身份 值 类型

isinstance(a,str) 判断类型的函数 判断a是不是 str

type() 不能判断子类型

isinstance  第二个参数可以是一个元组  如(int,str) 满足任意一种返回true



位运算符 （把数字当做二进制数进行运算）

​	& 按位与

​	| 按位或

​	^ 按位异或 不同则为1 相同则为0

​	~ 按位取反

​	<< 左移动

​	>> 右移动



2018年7月11日21:27:57



单行注释# 多行注释 '''

Python建议取名用下划线 不用驼峰

### 4.分支 循环 条件与枚举

if 后不跟() 直接写表达式 加 :

也不跟 {} 靠缩进区分块

else if 在Python里是 elif

控制台输入函数 input()



while和for都 可以跟一个 else 正常结束之后执行(break出去不会执行else)

不能直接for x in 10 因为in的对象需要是序列 可使用 for x in range(0,10)

range() 第三个参数的步长



### 5.包和模块

包就是文件夹，模块就是单个文件

但是一个包里面有一个特地的文件 \_\_init\_\_.py

（这个文件的作用通常是对包和模块做初始化）

\_\_init\_\_.py的模块名就是包名

导入模块

import a

使用导入的模块

a.xx

别名 import a as b

其他方式： 

from 模块名 import 变量1,变量2...

（要换行 建议用() 不用 \ ）

from 模块名 import （变量1，

变量2）

from 包名 import 模块名

from 模块名/包名 import * 导入所有

导出的模块里 可以用 \_\_all\_\_ 定义要导出的 \_\_all\_\_  = ['a']

(在init里定义的all指定的是导出的包 包含的模块)

init里面导入的模块 



模块的导入要避免循环导入

有一个入口文件的概念



2018年7月12日



### 6.函数

sorted(列表，key=一个函数，reverse=True)

reverse True倒叙 false正序 

排序 返回排序后的列表



strip()

去空格 换行符



round(a,2)

保留几位小数 同时四舍五入

def 定义函数

没有return结果 就是 None



设置递归最大次数

import sys 

sys.setrecursionlimit(10000)

函数里用return可以多个返回值 用逗号隔开 

返回的内容默认会放在元组里

也可以指定名称来取返回值 a,b = fx()

定义变量的时候也可以一次定义几个 a,b,c = 1,2,3    a=b=c=1



d = 1,2,3

序列解刨 (就像 js 的赋值解构)

a,b,c = d   必须数量对的上 不然会报错



参数的形式

1.必须参数 默认的按顺序传参

2.关键字参数 就是调用函数传参的时候指定传哪个 add(y=3,x=2)

3.默认参数 就是定义函数的时候 用=号定义

必须和关键字混合传会报错



### 7.面向对象 类

class 第一个字母大写 命名类的时候建议用驼峰而不是_

class Student():

实例化的时候不需要 new 直接 Student()

类里面定义成员函数的时候 需要传入self 相当于其他语言this

self 相当于 调用函数的那个实例对象

不要在类的内部调用自身成员函数



类的构造函数

def \_\_init\_\_(self):

对比 js constructor java 没返回的类名同名函数

虽然通常没必要 但是 可以显示调用构造函数的

def 定义的是实例方法 要定义类方法要加注解

@classmethod



类变量和实例变量

```python
class Student():
    name = ''  #类变量
    age = 0
    def __init__(self,name,age = 18):
        self.name = name #实例变量
        self.age = age

    def print_stu(self):
        print('My name is ' + self.name + \
        ',I`m ' + str(self.age) + ' years old')
```



实例.\_\_dict\_\_ 打印出的是实例的所有东西

实例.\_\_class\_\_  就能访问类变量



定义一个静态方式 加注解 

类和对象都可以调用

@staticmethod



想私有化方法或属性 就在前面加双下划线

 但如果后面也加了双下划线就不是私有了



实际上并没有真正意义上的私有变量 见代码

强行给实例的私有属性赋值 其实是给实例新赋值一个属性

```
类中定义的私有变量 存储为 _Student__score

而 强行为实例私有属性赋值 s1.__score = 10
实际上是添加了一个 __score

{'name': 'boen', 'age': 18, '_Student__score': 0, '__score': 10}
```



类要继承 就在类定义后面的括号里加入父类

继承了父类之后 子类实例化时 调用构造函数

要显式的调用父类的构造函数

方式1（只是可行 不推荐）

类调用实例方法是不好的

```
def __init__ (self, school, name, age):
	self.school = school
	Hum. __init__(self, name, age)

```

方式2 用super



```
def __init__ (self, school, name, age):
	self.school = school
	super(Student, self). __init__(name, age)
```



2018年7月13日16:32:53



### 8.正则表达式与json

Python 默认是贪婪 非贪婪在表达式后加?

字符串有 index() 类比 js indexof



正则表达式 导入 

import re

re.findall（'正则表达式', 传入字符串）

返回的是列表

中括号里面的是或关系 小括号是且关系

re.findall（） 第三个参数 是模式

如 填入 re.I 是忽略大小写

re.S 可以改变 正则表达式中 . 的行为 能匹配到换行符

第三个参数可以 re.I | re.S 跟竖线表示应用多个模式



re.sub(正则表达式, 要替换成的字符串, 原字符串, 替换数量, 模式)

替换数量设置为0表示 无数个

第二个参数 可以是一个函数 每一次匹配到 就会调用一次 

会传入 匹配到字符串信息(match 对象)

在回调函数里 对match 对象调用 xx.group() 就能拿到真正匹配到的值 进行操作

抵用 xx.span() 可以得到 在字符串中的位置



re.match() 从第一个字符串开始匹配 遇见不匹配的就结束并返回

如果第一个就不匹配 返回 none

re.search() 搜索整个字符串 直到找到第一个满足的并返回

xx.group() 可以传 分组的序号

分组是通过 正则表达式中的 () 默认整个表达式是一个组

所以xx.group(0) 和不传是一样的

多个分组序号用逗号隔开 xx.group(0,1,2)

还有一个函数 groups() 会返所有表达式中自己()起来的



json

import json

rel = json.loads(字符串)

对象会转换为字典

数组会转换为列表

null 会转换 为 None

整个过程叫 反序列化

json.dumps() 序列号 转为json字符串



### 9.枚举

py3 新增 枚举类型

要先导入

from enum import Enum

如果所有值都想强制为数字

可以继承 IntEnum

from enum import IntEnum

class VIP(Enum):

​	YELLOW= 1

​	GREEN = 2

​	BLACK = 3

​	RED = 4

​	GREEN_MAO = 2

枚举最好用大写

直接 VIP.RED 无法得到值 

得到的是 VIP.RED 类型是枚举下的一种类型

VIP.RED.value 是值 4

VIP.RED.name 是键 red



如果有值相同的枚举类型 后面的就是第一个的别名

如 GREEN_MAO  就是 GREEN 的别名

循环遍历 枚举的 时候 会忽略别名

别名也要遍历的话 要for  VIP.\_\_member\_\_



如果想唯一值 值相同报错的话 可以加注解 unique

from enum import unique

@unique

class VIP():



要转换成一个枚举类型 可以 把值传进 枚举类 如 

a = 1

print(VIP(a))   => VIP_YELLOW



### 10.闭包

能在函数外部某个地方访问或调用函数内部的内容 就产生了闭包

和 js 里差不多

xx.\_\_closure\_\_

里面放的就是闭包里调用时环境变量 （函数定义的时候）

xx.\_\_closure\_\_[0].cell+contents

里面放的就是闭包里调用时实际的变量值



闭包的意义就是保存了 函数调用时的现场

![img](https://github.com/boenfu/BoenNote/blob/master/Python%E5%85%A5%E9%97%A8%E4%B8%8E%E8%BF%9B%E9%98%B6%EF%BC%88%E8%A7%86%E9%A2%91%EF%BC%89%EF%BC%88%E5%AE%8C%EF%BC%89/py2.png)

之所以会报 引用之前未定义的错误

我猜测是因为第5句代码 可能像js一样会有变量提升

导致了先声明了局部origin 再进行 + 最后才赋值的



要想某个变量是全局作用域里面的 就加global 否则会默认定义一个局部变量（还是喜欢 js 的 let const）

想申明不是局部变量就 用关键字 nolocal

这样就不会默认去定义 而是去找了



![img](https://github.com/boenfu/BoenNote/blob/master/Python%E5%85%A5%E9%97%A8%E4%B8%8E%E8%BF%9B%E9%98%B6%EF%BC%88%E8%A7%86%E9%A2%91%EF%BC%89%EF%BC%88%E5%AE%8C%EF%BC%89/py3.png)

闭包的例子 保存了案发现场



2018年7月14日18:04:47



### 11.匿名函数

 def 

lambda 来定义匿名函数

lambda x,y: x+y

类比 js  (x,y) => x+y



### 12.三元表达式

js 里 x>y?x:y

x if x > y else y



### 13.map

第一个参数是函数 第二个是列表

第一个参数用于返回新的项

返回的是map object 可以用 list(结果) 转化还为列表

对标 js 数组的.map



map 可以接受多个列表map(方法,列表1，列表2)

方法的参数就会有两个了

最后的结果的长度是最短的那个列表的长度



### 14.reduce

py3后 

reduce需要引用 

from functools import reduce

连续计算 

第一个参数是有两个参数的函数

​	这个函数的第一个参数是上次的结果 第二次是下一个元素

第二个是列表

```python
list_x = [1,2,3,4,5,6,7,8]
r = reduce(lambda x,y:x+y, list_x)
print(r) // 36
```

第三个参数是初始值 

第一次执行的时候 x就是初始值 y就是第一个元素

未设置初始值 第一次执行 x就是第一个元素 y就是第二个元素



### 15.filter

第一个参数还是函数

返回真值就保留 假值就从数组中去掉



### 16.装饰器

是个语法糖

在函数定义上

@装饰函数的名字

就添加了装饰



*args 可变参数列表

**kw 关键字参数

类似 js ...参数

kw是一个字典

![img](https://github.com/boenfu/BoenNote/blob/master/Python%E5%85%A5%E9%97%A8%E4%B8%8E%E8%BF%9B%E9%98%B6%EF%BC%88%E8%A7%86%E9%A2%91%EF%BC%89%EF%BC%88%E5%AE%8C%EF%BC%89/py4.png)

装饰器函数基本套路

会返回一个函数 里面不仅包含了被装饰的函数 还包括了额外的业务代码

参数之所以这样写是为了应付各种传参情况

  

### 17.断点调试

vsc 里 f5开启断点/下一个断点 f10下一行 f11进入函数	

### 18.http

from urllib import request



request.urlopen() 获取一个网页

返回的内容 可以跳过 .read() 访问



### 19.用字典映射模拟switch

把内容放在字典里 用字典的get方法去取

get方法支持第二个参数 传入未找到时的默认值 可以当做switch的default



### 20.列表推导式

a = [1,2,3]

b = [ i * i for i in a]

print(b) =>  [1,4,9,16]

如果是有条件的推导

b = [ i * i for i in a if i >= 5]

( python 特有装逼写法 )

如果要推导字典,元组,集合 也可以把 中括号改成 大括号

推导字典的写法

![img](https://github.com/boenfu/BoenNote/blob/master/Python%E5%85%A5%E9%97%A8%E4%B8%8E%E8%BF%9B%E9%98%B6%EF%BC%88%E8%A7%86%E9%A2%91%EF%BC%89%EF%BC%88%E5%AE%8C%EF%BC%89/py5.png)

![img](https://github.com/boenfu/BoenNote/blob/master/Python%E5%85%A5%E9%97%A8%E4%B8%8E%E8%BF%9B%E9%98%B6%EF%BC%88%E8%A7%86%E9%A2%91%EF%BC%89%EF%BC%88%E5%AE%8C%EF%BC%89/py6.png)



### 21.类里的 len 和 bool

```
def __bool__
def __len__

len(某个对象) 实际是调用对象里的 __len__
bool(某个对象也是) 调用 __len__

__len__ 的返回值只能的数值和布尔
len调用时布尔会转换为01

但是如果显式定义了 __bool__ 方法
__len__ 就不能决定bool()的返回值了
__bool__ 只能返回布尔值
```



### 21.beautifulsoup , scrapy







 
