#### Algorithm
The count-and-say sequence is the sequence of integers with the first five terms as following:

1.     1
2.     11
3.     21
4.     1211
5.     111221
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence.

```python
def countAndSay(self, n):
    s = '1'
    for _ in range(n - 1):
        s = ''.join(str(len(list(group))) + digit
                    for digit, group in itertools.groupby(s))
    return s
```

#### Review

https://medium.com/faun/microservices-mesh-part-i-16ec52074dd2
什么是微服务网格?
微服务网格是一个抽象层，定义不同微服务之间的交互，网格使用不同容器之间的网络来控制应用程序的不同组件的交互方式，因为网络是微服务最基本的组件，
通过服务网络控制网络允许你完成很多有用的事情，比如你部署一个新版本的组件，你可以直接把网络设备指向新的组件。如果是扩展，可以使用服务网格指向不同服务
的不同load banlance,并增加应用程序不用组件的数量，在开始使用微服务的时候，一个常见的建议将应用程序不同的组件视为不同的api
您想部署新版本，您可以根据需要使用DNS指向新容器。或者指向新的负载均衡器。或者更改现有负载均衡器指向的容器。



### Tips

docker核心组件

<https://kenwoodjw.github.io/post/docker/>

#### Share

分布系统的事物处理
https://coolshell.cn/articles/10910.html
数据高可用   ----       多份数据        -- 一致性问题


