---
title: yield学习-1
date: 2019-01-23 15:05:55
tags:
---

python爬虫中会经常出现yield，yield是啥呢？他有啥作用呢？

自己的理解
1. 具有return的功能
2. 使用yield 的函数是一个生成器。
3. 具备事件触发的特性，使用yield实现异步通信

### yield 生成器和return功能

```python
def fab(max): 
   n, a, b = 0, 0, 1 
   L = [] 
   while n < max: 
       L.append(b) 
       a, b = b, a + b 
       n = n + 1 
   return L

if __name__ == "__main__":
    Fab = fab(5)
    print(type(Fab))
    for n in Fab:
        print(n)
```

运行程序得到如下结果：

```python
<class 'list'>
1
1
2
3
5
```

这里`Fab`是类型是一个列表，可以想象，如果传的参数max越大，就会产生一个巨大的列表，占用较大的内存空间。所以我们可以考虑把fab 改写成 iterable对象。具体实现方法就是内置函数`__iter_`_, `next`

来实现，最简单的方法是直接使用`yield`

上面的代码用yield实现:

```python
def fab1(max): 
   n, a, b = 0, 0, 1 
   L = [] 
   while n < max: 
       yield b 
       a, b = b, a + b 
       n = n + 1 
   return L

if __name__ == "__main__":
    Fab = fab1(5)
    print(type(Fab))
    for n in Fab:
        print(n)
    for n in Fab:
        print("zouqi")
        print(n)

```

输出结果如下：

```python
<class 'generator'>
1
1
2
3
5
```

可以看到`type(Fab)`返回的是一个生成器的实例，大家一定注意到在这个实例中循环了两次Fab ,第二次是打印任何数据，这是生成器的特性决定的.

### yield异步通信及协程

在python中比较典型的的应用是生产者消费者模式，此外在python2中协程主要是gevent，在python3中已经自己实现了协程语法`yield from`及其封装`asyncio.coroutine` 协程作为下一篇博客来写。
