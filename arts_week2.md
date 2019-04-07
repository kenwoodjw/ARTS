### ARTS 分享第二周

#### Algorithm

344. Reverse String
level:easy

Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

You may assume all the characters consist of printable ascii characters.

 

Example 1:

Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
Example 2:

Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]

```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything. modify s in-place instead."""
        left,right = 0, len(s)-1
        while left<right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
```

#### Review

https://medium.com/system-design-blog/what-is-api-gateway-68a11d4ab322

什么是api gateway?

当client直接与微服务通信会导致很多问题

1.api提供的粒度不是client所需，一个操作请求多个服务，导致延迟严重

2.网络性能不同

3.复杂的客户端代码

4.客户端和后端之间创建紧密耦合。客户需要知道如何分解各个服务。添加新服务或重构现有服务变得更加困难

5.服务端需要实现通用的权限认证，ssl等

6.服务必须仅使用http或websocket

apigateway的好处

1.API网关可以将多个单独的请求聚合到一个请求中

2.提高客户端性能，api gateway运行在相同网络

3.简化客户端

4.允许服务使用非Web友好协议

5.从单个服务中卸载通用功能。将这些功能合并到一个地方非常有用，而不是让每个服务都负责实现它们，比如身份认证。

#### Tips

python中的弱引用的使用

概念：弱引用是指不能确保其引用的对象不会被垃圾回收器回收的引用。一个对象若只被弱引用所引用，则可能在任何时候被回收。

作用：减少循环引用，减少内存中不必要的对象存在的数量

例子：创建缓存实例

希望相同参数创建的对象是单例的。在很多库中都有实际的例子，比如logging模块,使用相同的名称创建的logger实例永远只有一个

```python

import logging
a = logging.getLogger('foo')
b = logging.getLogger('bar')
a is b # False
c = logging.getLogger('foo')
a is c # True
```

为了达到这样的效果，你需要使用一个和类本身分开的工厂函数

```python
class Spam:
    def __init__(self, name):
        self.name = name
        
# Caching support
import weakref
_spam_cache = weakref.WeakValueDictionary()
def get_spam(name):
    if name not in _spam_cache:
        s = Spam(name)
        _spam_cache[name] = s
    else:
        s = _spam_cache[name]
    return s

a = get_spam('foo')
b = get_spam('bar')
a is b # False
c = get_spam('foo')
a is c # True
```



更优雅的解决方法，重新定义类的 `__new__()`方法,问题是`__init__()`每次都会被调用，不管实例是否被缓存了。

```python
import weakref

class Spam:
    _spam_cache = weakref.WeakValueDictionary()
    def __new__(cls, name):
        if name in cls._spam_cache:
            return cls._spam_cache[name]
        else:
            self = super().__new__(cls)
            cls._spam_cache[name] = self
            return self
    def __init__(self, name):
        print("Initializing Spam")
        self.name = name
        
s = Spam('Dave')
t = Spam('Dave')
s is t # True

```



#### Share

## 无责任书评：《深入理解计算机系统》这本神书到底好在哪儿？

https://mp.weixin.qq.com/s/EJ98zgPvc7xE6p__Rs-HyA