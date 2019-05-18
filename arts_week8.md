#### Algorithm
A binary watch has 4 LEDs on the top which represent the hours (0-11), and the 6 LEDs on the bottom represent the minutes (0-59).

Each LED represents a zero or one, with the least significant bit on the right.


For example, the above binary watch reads "3:25".

Given a non-negative integer n which represents the number of LEDs that are currently on, return all possible times the watch could represent.

Example:

Input: n = 1
Return: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
```python
"""
统计小时和分钟出现二进制1的次数
"""
class Solution:
    def readBinaryWatch(self, num: int) -> List[str]:
        result = []
        for h in range(12):
            for m in range(60):
                if (bin(h)+bin(m)).count('1') == num:
                    result.append("%d:%02d"%(h,m))
        return result
        
```
#### Review
为什么用Go，比较java和python

https://yourbasic.org/golang/advantages-over-java-python/

选择编程语言不是一件容易的事，一开始语言的功能看起来，但缺点需要时间和经验发现

作为一名cs教授和长期java和go开发者，我更倾向于go，go让我更容易写好的代码

1.极简主义

正式的Go语言规范只有50页，有很多例子，并且相当容易阅读。熟练的程序员可能只能从规范中学习Go

语言核心功能越极简，语言更易学习，go的核心功能：

内核测试框架:tesing和profiling,很小很容易学习，但仍然功能齐全，还有很多第三方模块

可以通过HTTP服务器调试和分析在生产中运行的优化二进制文件。

Go可以自动生成包含可测试示例的文档，界面很小，而且很容易学习

Go是强静态,没有隐式转换,语法开销比较小。赋值简单类型推断以及非类型数字常量想

结构化类型结构接口通过动态分派提供运行时多态。

并发是Go的一个组成部分，由goroutines，channels和select语句支持

####　Tip    

docker + Registror + consul + consul template

![avatar][image/nginx.png]

#### Share
