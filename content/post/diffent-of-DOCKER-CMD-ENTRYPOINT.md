---
title: docker中CMD和ENTRYPOINT区别
date: 2016-11-13 15:50:41
tags: [docker, ENTRYPOINT]
---

在编写Dockerfile时，一定会被CMD指令和ENTRYPOINT搞迷惑。CMD指令不就是docker容器执行的命令么，这不和ENTRYPOINT一样么？

第一个区别很好理解entrypoint是不能在docker run 命令中被覆盖的，而cmd指令可以

另外一个问题当dockerfile既有ENTRYPOINT又有CMD时它们是什么关系 。这个问题也困扰了我好久，最近终于搞明白了。

我们先看看CMD的用法

```bash
CMD ["executable","param1","param2"] (exec form, this is the preferred form)
CMD ["param1","param2"] (as default parameters to ENTRYPOINT) 
CMD command param1 param2 (shell form) 
```

再看看ENTRYPOINT的用法

```bash
ENTRYPOINT ["executable", "param1", "param2"]
ENTRYPOINT command param1 param2
```

我们来看看CMD的第二总用法 CMD \["param1","param2"\] (as default parameters to ENTRYPOINT) 这个写得很明白了，就是做为ENTRYPOINT的参数。这种情况是在什么场景中呢？经实验得出在一个docker image 中有同时有ENTRYPOINT和CMD指令时 CMD的指令就是entrypoint的参数。

总结：
**在配置了ENTRYPOINT时，CMD就是ENTRYPOINT的参数，如果没配置ENTRYPINT时，CMD就是docker容器最终执行的命令**。
