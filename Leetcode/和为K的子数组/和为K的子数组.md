## 和为K的子数组
**题目**：
给定一个整数数组和一个整数 k，你需要找到该数组中和为 k 的连续的子数组的个数。

**示例**：
```
输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
```
```
说明 :

数组的长度为 [1, 20,000]。
数组中元素的范围是 [-1000, 1000] ，且整数 k 的范围是 [-1e7, 1e7]。
```

算法：hashmap保存的前缀和
- if prefixSum[j] == prefixSum[i], Sum[i+1:j+1] == 0
- prefixSum[j] - prefixSum[i] == k, Sum[i+1:j+1] == k
- 用哈希表记录前缀和出现的次数，并每次查找prefixSum[j] - k = prefixSum[i]出现的次数，对应的次数就是连续数组的个数。

**submission 1**:
```python
from collections import defaultdict
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        if not nums:
            return 0
        n = len(nums)
        hashmap = defaultdict(int)
        hashmap[0] = 1
        count = 0
        prefixSum = 0
        for num in nums:
            prefixSum += num
            if prefixSum-k in hashmap:
                count += hashmap[prefixSum-k]
            hashmap[prefixSum] += 1
        return count
```


<font color="#FF0000">**Attention**</font>:

- 
