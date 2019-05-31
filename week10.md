#### Althgoimal

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

```python
class Solution:
    def romanToInt(self, s: str) - > int:
        mem = {'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
        vals =[mem[c] for c in s] +[0]
        total = 0
        for i in range(len(s)):
            if vals[i] < vals[i+1]:
                total -= vals[i]
            else:
                total += vals[i]
        return total
```

#### Review
https://medium.com/faun/microservices-mesh-part-ii-istio-basics-b9c343594a05
services mesh istio 基础
1，深入data plane 和sidecar
Istio定义了两个关键的架构术语： data plane:通过应用移动的数据，传递给不同的服务实例并由服务处理。
control plane：确定如何实例化服务以及保持服务的遥测和信息的位置。
sidecar代理拦截进入服务的流量，并允许您以智能方式路由它，sidecar允许添加新的功能，比如负载平衡，处理TLS，版本控制，分阶段部署，收集使用指标，无需重新设计系统。sidecar 它们允许您在应用程序中构建弹性并添加额外级别的可伸缩性.服务之间的中央通信endpoints
微服务常见问题就是pod是相互隔离的，如果微服务出现问题，请求可能会被缓慢处理或丢弃。 使用sidecars，您可以在一个地方添加超时，更智能的负载平衡和额外的监控。
使用Istio时，与控制平面交互的主要方式是通过Kubernetes。例如使用kubectl将pod升级到新版本,版本更新将通过更新本地控制平面变量开始


#### Tips
https://yq.aliyun.com/articles/19
地理围栏算法解析
1.如何判断点在多边形内，通过射线法，从该点出发沿x轴画一条直接，如果交点数为奇数，则在多边形内部，如果交点数为偶数，则在多边形外部，复杂度为O(N)
2.R树索引加速判断
1.外包矩形表示多边形


#### Share

nginx 在线配置
https://nginxconfig.io/