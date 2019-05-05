### ARTS分享第五周

### Althogriam

level:easy 
Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'.

Examples:
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"

```python
class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        if [a for a in letters if ord(a)>ord(target)]:
            return min([a for a in letters if ord(a)>ord(target)])
        else:
            return min(letters
```
best answer 
```python

import bisect
 def nextGreatestLetter(self, letters, target):
        a = bisect.bisect_left(letters, target)
        if a < len(letters) and letters[a] == target:
            a = bisect.bisect_right(letters, target)
        if a >= len(letters):
            a %= len(letters) 
        return letters[a]
```
#### Review
全周期开发者
https://medium.com/netflix-techblog/full-cycle-developers-at-netflix-a08c31f83249

Edge Engineering负责aws，是以运营为重点的团队和SRE专家，拥有部署+运营+支持软件生命周期的部分，发布新功能意味着开发人员会与运营团队协调指标，警报和容量方面的问题。
然后为运营团队分发代码进行部署和运营,当事情进展不顺利时，开发人员和Edge Engineering沟通成本越来越高。从devops运动获得灵感。完整周期开发人员会像SWE，
SDET和SRE一样思考和行动。有时他们会创建解决业务问题的软件，有时他们会为此编写测试用例，有时他们会自动化该系统的操作方面



#### Tip
python数据模型

```python
class Ploynomail:
    def __init__(self, *coeffs):
        self.coeffs = coeffs
        
    def __repr__(self):
        return 'Ploynomail(*{})'.format(self.coeffs)
    
    def __add__(self, other):
        return Ploynomail(*(x + y for x, y in zip(self.coeffs, other.coeffs)))
    
    def __len__(self):
        return len(self.coeffs)

```

​	

特殊的只读属性: `__self__` 为类实例对象本身，`__func__` 为函数对象；`__doc__` 为方法的文档 (与 `__func__.__doc__` 作用相同)；[`__name__`](https://docs.python.org/zh-cn/3/library/stdtypes.html#definition.__name__) 为方法名称 (与 `__func__.__name__` 作用相同)；`__module__` 为方法所属模块的名称，没有则为 `None` 



#### Share
redis思维导图
https://github.com/Weiwf/redis-mindmap