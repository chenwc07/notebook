## 数组中的第K个最大元素
**题目**：
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例**：
```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```
```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

算法1：排序

**submission 1**:
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        nums.sort()
        return nums[-k]
```


**改进思路1**：
优先队列（堆）
- 维护一个大小为k的小顶堆
- 遍历数组，大于堆顶就替换，小于堆顶就不管
- 遍历完后，堆中就是k个大元素，堆顶就是第k大的元素    。


**submission 2**：
```python
import heapq
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = []
        for i in range(k):
            heapq.heappush(heap,nums[i])
        
        for j in range(k,len(nums)):
            if nums[j] > heap[0]:
                heapq.heapreplace(heap, nums[j])
        return heap[0]
```

算法3：快速选择法
- 利用快速排序的原理选择位于第k大位置的pivot
- 
```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        l,r = 0,len(nums)-1
        target = len(nums)-k
        while True:
            mid = self._partition(nums,l,r)
            if mid == target:
                return nums[mid]
            if mid < target:
                l = mid+1
            else:
                r = mid-1
        
    def _partition(self,nums,l,r):
        pivot = nums[l]
        i = l
        for j in range(l+1, r+1):
            if nums[j] < pivot:
                i += 1
                nums[i], nums[j] = nums[j], nums[i]
        nums[i],nums[l] = nums[l],nums[i]
        return i
```

<font color="#FF0000">**Attention**</font>:

- [heapq的使用](https://docs.python.org/2/library/heapq.html)
