### ARTS 分享第7周

#### Algorithm

level: easy

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 

Input: 19
Output: true
Explanation: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

```python
from functools import reduce
class Solution:
    def isHappy(self, n: int) -> bool:
        result = reduce(lambda x,y :x+y ,[int(i)**2 for i in str(n)])
        if result == 1:
            return True
        else:
            self.isHappy(result)
```

#### Review
全栈开发者实际上会卡在中级，无法深入 很有意思的一篇文章，
作者根据亲身经历讲述全栈职位由于要学的东西多，
变化快，导致很难深入学习某一个领域。而且由于变化快，
导致需要持续快速学习。无法深入则无法形成自己的专长。

https://habr.com/en/post/436596/
#### Tip
问题: 单体应用，牵一发动全身，应用膨胀，开发耦合度高，协作效率低下
服务化:把本地调用改造成远程rpc调用
微服务:更细粒度的服务化
服务拆分粒度更细，服务独立部署，服务独立维护，服务治理要求高
拆分:将不同的功能模块拆分(纵向拆分)，是否有公共的部分（横向拆分)
弊端:架构复杂性
服务如何定义？服务之间的调用通过接口来描述定义，约定内容包括接口名，接口参数，接口返回值
服务如何发布订阅?注册中心
服务如何监控？业务埋点，数据收集，数据处理，数据展示全链路监控
服务如何治理？熔断
故障如何定位？能够将一次用户请求进行标记，然后在多个依赖服务进行传递
#### Share
一探B站后台架构, 他山之石, 何以攻玉? -- 仅从一个一线Golang开发者的角度谈B站4.22代码
https://www.jianshu.com/p/b8e29b68252f?from=timeline&isappinstalled=0