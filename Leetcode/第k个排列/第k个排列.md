## 第k个排列
**题目**：
给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。

按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下：
```
"123"
"132"
"213"
"231"
"312"
"321"
```
给定 n 和 k，返回第 k 个排列。

说明：

给定 n 的范围是 [1, 9]。
给定 k 的范围是[1,  n!]。


**示例**：
```
输入: n = 3, k = 3
输出: "213"
```
```
输入: n = 4, k = 9
输出: "2314"
```


算法1：找规律

**submission 1**:
```python
class Solution:
    def getPermutation(self, n: int, k: int) -> str:
        temp = [str(i) for i in range(1,n+1)]
        res = ''
        while len(temp) > 0:
            t = math.factorial(len(temp)-1) # 确定第一个数后有多少个排列，即(n-1)!
            idx = math.ceil(k/t) - 1 # 只能用ceil(k/t)-1得到index而不能用k//t, 否则在k==t时会出错
            res += temp[idx]
            temp.pop(idx)
            k %= t # 候选的长度改变, 要改变k的值
        return res
```


**改进思路1**：


**submission 2**：
```python

```


**改进思路2**：

**submission 3**：
```python

```


**改进思路3**：

**submission 4**：
```python

```


<font color="#FF0000">**Attention**</font>:

- 
