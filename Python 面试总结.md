Python 面试总结

爬虫模块、框架、反爬机制(IP代理池、验证码、UA)



### python is 和 == 的区别

Python中对象包含的三个基本要素，分别是：id(身份标识)、type(数据类型)和value(值)

```
==是python标准操作符中的比较操作符，用来比较判断两个对象的value(值)是否相等
is也被叫做同一性运算符，这个运算符比较判断的是对象间的唯一身份标识，也就是id是否相同
```

只有数值型和字符串型的情况下，a is b才为True，当a和b是tuple，list，dict或set型时，a is b为False

```
>>> a = 1 #a和b为数值类型
>>> b = 1
>>> a is b
True
>>> id(a)
14318944
>>> id(b)
14318944
>>> a = 'cheesezh' #a和b为字符串类型
>>> b = 'cheesezh'
>>> a is b
True
>>> id(a)
42111872
>>> id(b)
42111872
>>> a = (1,2,3) #a和b为元组类型
>>> b = (1,2,3)
>>> a is b
False
>>> id(a)
15001280
>>> id(b)
14790408
>>> a = [1,2,3] #a和b为list类型
>>> b = [1,2,3]
>>> a is b
False
>>> id(a)
42091624
>>> id(b)
42082016
```

