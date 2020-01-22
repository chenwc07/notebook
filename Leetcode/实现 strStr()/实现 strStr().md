## 实现 strStr()
**题目**：
实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1

说明:
当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。
对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。


**示例**：
```
输入: haystack = "hello", needle = "ll"
输出: 2
```
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

思路1：普通的迭代搜索

**submission 1**:
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if len(haystack) < len(needle):
            return -1
        if needle == '' or haystack == needle:
            return 0
        for i in range(len(haystack)-len(needle)+1):
            if haystack[i:i+len(needle)] == needle:
                return i
        return -1
```


**改进思路1**：
Sunday算法，加入偏移表。
所谓偏移表，就是needle中出现的所有字母的最右位置到最后一个字母的距离+1，没出现过的偏移量为```len(needle)+1```。这样，在匹配完一次字符串后，检查下一个字符，如果在偏移表中，则按照偏移表记录的偏移量进行偏移，就不用一个一个字符地往下迭代了。


**submission 2**：
```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        def shiftTable(needle):
            dict = {}
            for i in range(len(needle)-1,-1,-1):
                if needle[i] not in dict:
                    dict[needle[i]] = len(needle) - i
            dict['others'] = len(needle) + 1
            return dict
        
        if needle == '' or haystack == needle: return 0
        if len(needle) > len(haystack): return -1
        shift = shiftTable(needle)
        i = 0
        while i+len(needle) <= len(haystack):
            if haystack[i:i+len(needle)] == needle:
                return i
            elif i + len(needle) == len(haystack):
                return -1
            else:
                i += shift[haystack[i+len(needle)]] if haystack[i+len(needle)] in shift else shift['others']
        return -1
```


**改进思路2**：

**submission 3**：
```python

```

<font color="#FF0000">**Attention**</font>:

- list的下标```i```可以看作是当前位置前面有几个元素，这样对于计算各种边界条件（比如坐标+长度）比较有帮助。
