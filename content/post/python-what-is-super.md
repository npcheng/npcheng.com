---
title: python中super的用法
date: 2018-12-19 09:35:13
tags: [python]
---

写python时经常会用到 super ，在 django 的 cbv 模式中使用的比较频繁，有时候会有点懵，这里为啥要用super啊。 为了解决这个问题所以在网上收集了一些资料

super 用来调用父类的方法， 一般用于多重继承

python 2.7 及以下版本

```python
super(className, self).mathod()
```

python 3.6 及以下版本

```python
super().mathod()
```

单继承比较简单，这里就不写了。多重继承的情况

```python

class A(object):
    def __init__(self):
        self.n = 2

    def add(self, m):
        print('self is {0} @A.add'.format(self))
        self.n += m


class B(A):
    def __init__(self):
        self.n = 3

    def add(self, m):
        print('self is {0} @B.add'.format(self))
        super().add(m)
        self.n += 3


class C(A):
    def __init__(self):
        self.n = 4

    def add(self, m):
        print('self is {0} @C.add'.format(self))
        super().add(m)
        self.n += 4


class D(B, C):
    def __init__(self):
        self.n = 5

    def add(self, m):
        print('self is {0} @D.add'.format(self))
        super().add(m)
        self.n += 5

d = D()
print D.mro()
d.add(2)
print(d.n)
```

将输出：

```python
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <type 'object'>]
self is <__main__.D object at 0x7f251685aed0> @D.add
self is <__main__.D object at 0x7f251685aed0> @B.add
self is <__main__.D object at 0x7f251685aed0> @C.add
self is <__main__.D object at 0x7f251685aed0> @A.add
19
```

怎么来的可能有点晕，这里有个概念就mro(Method Resolution Order), 即:方法执行顺序

这个例子中：

```python
d.add(2) 的执行顺序：[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <type 'object'>]
```

这里头比较有迷惑性的是对象中的n. 最先执行的class A 中的n 是D这个对象中的n:5
add方法只会执行一次， 整个过程过程就是递归

```python
class D(B, C):          class B(A):            class C(A):             class A:
    def add(self, m):       def add(self, m):      def add(self, m):       def add(self, m):
        super().add(m)  1.--->  super().add(m) 2.--->  super().add(m)  3.--->  self.n += m
        self.n += 5   <------6. self.n += 3    <----5. self.n += 4     <----4. <--|
        (14+5=19)               (11+3=14)              (7+4=11)                (5+2=7)

```

参考资料：

- [极客学院-你不知道的python](http://wiki.jikexueyuan.com/project/explore-python/Class/super.html)
- [Python: super 没那么简单](https://mozillazg.com/2016/12/python-super-is-not-as-simple-as-you-thought.html) 
- [understanding python super with init methods](https://stackoverflow.com/questions/576169/understanding-python-super-with-init-methods)
- [你真的理解Python中MRO算法吗？](http://python.jobbole.com/85685/)
