### ARTS 分享第三周

#### Algorithm

1.Two Sum

level: easy

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hash_table = {}
        for i, num in enumerate(nums):
            if target - num  in hash_table:
                return [hash_table[target-num],i]
            hash_table[num] = i
```

#### Review

https://medium.freecodecamp.org/why-graphql-is-the-future-of-apis-6a900fb0bc81

为什么graphql 是未来的apis

rest存在很多问题比如：

1.很多endpoints

在rest中每个endpoint代表一种资源，如果你想构建一个get 请求，你需要一个endpoint，如果一个post请求，需要另一个endpoint。GET /posts    POST /post

2.过度获取和信息不足

如果我们只需要一小段数据，我们就必须处理整个对象。例如，如果我们只需要在REST API中获取用户的姓名、lastName和年龄，那么在不获取整个对象的情况下，我们不可能准确地获取这些数据。

如果我们想要从两种不同的资源获取数据，需要调用两个不同的endpoints

3.版本

rest api 经常看到不同的api版本

```shell
https://example.com/api/v1/users/12312
https://example.com/api/v2/users/12312
```

GraphQL的好处：

1.单一endpoint

2.GraphQL可以提取你想要的数据

3.GraphQL可以提高api的性能

#### Tips
redis默认字符串使用名为简单动态字符串(SDS)的抽象类型表示,SDS 定义
```
struct sdshdr{
    //记录buf数组中已使用字节的数量
    //等于SDS所保存字符串的长度
    int len;

    //记录buf数组中未使用字节的数量
    int free;

    //字节数组，用于保存字符串
    char buf[];
}
```
SDS 与 C字符串的区别
1.C字符串不记录自身长度，为了获取C字符串的长度，遍历整个字符串，O(n)， 获取一个SDS长度，O(1)
2.C字符串容易缓冲区溢出，SDS的api有一个执行拼接的sdscat函数，会先检查给定SDS空间是否足够，不够会先扩展
3.每次增长或缩短一个C字符串，都要对保存C字符串的数组进行内存重分配。SDS最多N次内存重分配
4.C字符串不能包含空字符串，限制C字符串只能保存文本数据，SDS可以保存文件数据或二进制数据


#### Share
分享一个github项目，收集了各种网站
https://github.com/tuteng/Best-websites-a-programmer-should-visit-zh#coding-practice-for-beginners