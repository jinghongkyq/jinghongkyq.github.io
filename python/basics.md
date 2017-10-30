#### python函数参数前面单星号（*）和双星号（**）的区别
[cite](http://www.cnblogs.com/arkenstone/p/5695161.html)
```
def foo(param1, *param2):
def bar(param1, **param2):
```
这两种用法其实都是用来将任意个数的参数导入到python函数中。

* 单星号（*）：*agrs 将所以参数以元组(tuple)的形式导入：
```
>>> def foo(param1, *param2):
        print param1
        print param2
>>> foo(1,2,3,4,5)
1
(2, 3, 4, 5)
```
此外，单星号的另一个用法是解压参数列表：
```
>>> def foo(bar, lee):
        print bar, lee
>>> l = [1, 2]
>>> foo(*l)
1 2
```

* 双星号（**）：**kwargs 将参数以字典的形式导入
```
>>> def bar(param1, **param2):
        print param1
        print param2
>>> bar(1,a=2,b=3)
1
{'a': 2, 'b': 3}
```

当然这两个用法可以同时出现在一个函数中：例如
```
>>> def foo(a, b=10, *args, **kwargs):
        print a
        print b
        print args
        print kwargs
>>> foo(1, 2, 3, 4, e=5, f=6, g=7)
1
2
3 4
{'e': 5, 'g': 7, 'f': 6}
```
