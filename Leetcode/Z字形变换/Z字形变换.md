## Z字形变换
**题目**：
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：
```
L   C   I   R
E T O E S I I G
E   D   H   N
```

之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：

**示例**：
```
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
```
```
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

L     D     R
E   O E   I I
E C   I H   N
T     S     G
```

思路：(抄答案)按顺序遍历字符串，即可知道当前字符串属于哪一行。

**submission 1**:
```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows < 2 or len(s) <= numRows:
            return s

        strs = ['' for _ in range(numRows)]
        row = 0
        flag = 1
        for i in range(len(s)):
            strs[row]  += s[i]
            row += flag
            if row == 0 or row == numRows-1:
                flag = -flag

        ans = ''
        for ss in strs:
            ans += ss
        return ans
```


<font color="#FF0000">**Attention**</font>:

- 令人智障的题目
