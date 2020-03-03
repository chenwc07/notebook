## 前 K 个高频元素
**题目**：
给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

说明：

- 你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
- 你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。


**示例**：
```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```
```
输入: nums = [1], k = 1
输出: [1]
```


算法：哈希+优先队列

**submission 1**:
```python
import heapq
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        for num in nums:
            count[num] = count.get(num, 0) + 1
        res = heapq.nlargest(k, count.keys(), key = count.get) # count.keys()是iter对象，也是排序的目标，而key参数则是排序的依据，就是count.keys()中的元素x，按照key(x)的大小进行排序。
        return res

# or
import heapq
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        for num in nums:
            count[num] = count.get(num, 0) + 1
        res = heapq.nlargest(k, count, key = lambda x:count[x])
        return res
```


算法2：哈希+桶排序
- 先用哈希计数
- 以频率为下标，频率对应的数(的列表)为元素，建立桶
- 从大到小遍历桶，直到结果中有k个元素为止


**submission 2**：
```python
import heapq
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = {}
        for num in nums:
            count[num] = count.get(num, 0) + 1
        bucket = [[] for _ in range(len(nums)+1)]
        for key, value in count.items():
            bucket[value].append(key)
        res = []
        i = 0
        while i<k:
            if len(bucket[-1]) == 0:
                bucket.pop()
                continue
            else:
                res.append(bucket[-1].pop())
                i += 1
        return res
```



<font color="#FF0000">**Attention**</font>:

- 
