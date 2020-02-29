## 搜索二维矩阵II
**题目**：
编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。


**示例**：
```
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。
```

算法1：沿对角线的二分查找
- 对角线的每一个元素对应一行和一列
- 因此每个对角线进行两次二分查找

**submission 1**:
```python
class Solution:
    def bnsearch(self, matrix, target, l, r, vertical, index):
        while l<=r:
            mid = (l+r) // 2
            if vertical:
                if matrix[mid][index] == target:
                    return True
                elif matrix[mid][index] < target:
                    l = mid + 1
                elif matrix[mid][index] > target:
                    r = mid - 1
            if not vertical:
                if matrix[index][mid] == target:
                    return True
                elif matrix[index][mid] < target:
                    l = mid + 1
                elif matrix[index][mid] > target:
                    r = mid - 1
        return False

    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix:
            return False
        rows = len(matrix)
        cols = len(matrix[0])
        i, j = 0, 0
        while i < rows and j < cols:
            if target == matrix[i][j]:
                return True
            elif target < matrix[i][j]:
                if self.bnsearch(matrix,target,0,j-1,False,i) or self.bnsearch(matrix, target, 0, i-1, True, j):
                    return True
            elif target > matrix[i][j]:
                if self.bnsearch(matrix,target,j+1,cols-1,False,i) or self.bnsearch(matrix, target, i+1, rows-1, True, j):
                    return True
            i += 1
            j += 1
        return False
```


**改进思路1**：
缩小搜索范围
- 从右上角开始
  - target < 当前，列减小
  - target > 当前，行增大

- 也可以从左下角开始
  - target < 当前，行减小
  - target > 当前，列增大

**submission 2**：
```python
class Solution:

    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix:
            return False
        i, j = 0, len(matrix[0])-1
        while i < len(matrix) and j >= 0:
            if target == matrix[i][j]:
                return True
            elif target > matrix[i][j]:
                i += 1
            elif target < matrix[i][j]:
                j -= 1
        return False
```

<font color="#FF0000">**Attention**</font>:

- 
