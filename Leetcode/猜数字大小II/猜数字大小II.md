## 猜数字大小II
**题目**：
我们正在玩一个猜数游戏，游戏规则如下：

我从 1 到 n 之间选择一个数字，你来猜我选了哪个数字。

每次你猜错了，我都会告诉你，我选的数字比你的大了或者小了。

然而，当你猜了数字 x 并且猜错了的时候，你需要支付金额为 x 的现金。直到你猜到我选的数字，你才算赢得了这个游戏。

给定 n ≥ 1，计算你至少需要拥有多少现金才能确保你能赢得这个游戏。

**示例**：
```
n = 10, 我选择了8.

第一轮: 你猜我选择的数字是5，我会告诉你，我的数字更大一些，然后你需要支付5块。
第二轮: 你猜是7，我告诉你，我的数字更大一些，你支付7块。
第三轮: 你猜是9，我告诉你，我的数字更小一些，你支付9块。

游戏结束。8 就是我选的数字。

你最终要支付 5 + 7 + 9 = 21 块钱。
```

算法：动态规划（比较难，状态转移涉及到最小化最大值，参考[题解](https://leetcode-cn.com/problems/guess-number-higher-or-lower-ii/solution/dong-tai-gui-hua-c-you-tu-jie-by-zhang-xiao-tong-2/)）

**submission 1**:
```python
class Solution:
    def getMoneyAmount(self, n: int) -> int:
        dp = [[float('inf') for _ in range(n+1)] for _ in range(n+1)]
        for i in range(1,n+1):
            dp[i][i] = 0
        for j in range(2,n+1):
            for i in range(j-1,0,-1):
                for k in range(i+1,j):
                    dp[i][j] = min(dp[i][j], max(dp[i][k-1],dp[k+1][j])+k)
                dp[i][j] = min(dp[i][j], dp[i+1][j]+i)
                dp[i][j] = min(dp[i][j], dp[i][j-1]+j)
        return dp[1][n]
```

<font color="#FF0000">**Attention**</font>:

- 
