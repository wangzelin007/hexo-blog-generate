---
title: python问题记录001
tags: [python]
toc: true
mathjax: true
date: 2019-02-25 10:55:25
categories: python
---
@property 方法？

如何判断对象是可迭代对象
```
from collections import Iterable
isinstance([1,2,3], Iterable)
```

生成器 (一边循环一边计算)
```
定义生成器的两种方法 () 和 yeild
generator 执行流程：普通函数执行是顺序执行，遇到return或者最后一行语句就返回。
generator 每一调用next()执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。
没有更多元素时，抛出StopIteration错误。
```

map
```
让序列中的每个元素依次调用函数
map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
```

reduce
```
把函数作用在一个序列上，reduce 会把结果和序列的下一个元素做累计计算
reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)
```