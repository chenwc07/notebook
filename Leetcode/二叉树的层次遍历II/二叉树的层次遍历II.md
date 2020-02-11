## 二叉树的层次遍历
**题目**：
给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

**示例**：
```
例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其自底向上的层次遍历为：

[
  [15,7],
  [9,20],
  [3]
]
```

思路：层次遍历再反序输出

**submission 1**:
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
from collections import deque
class Solution:
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []

        deq = deque([root])
        result = []
        while deq:
            temp = []
            for i in range(len(deq)):
                p = deq.popleft()
                temp.append(p.val)
                if p.left:
                    deq.append(p.left)
                if p.right:
                    deq.append(p.right)
            result.append(temp)
        return result[::-1]
```


**改进思路1**：
可以但是没有必要的DFS遍历，关键点在于记录结点的层数，且stack后进先出的特点。

**submission 2**：
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
        if not root:
            return []

        st = []
        st.append((0, root))
        result = []
        while st:
            current_depth, p = st.pop()
            if p:
                if current_depth == len(result):
                    result.append([])
                result[current_depth].append(p.val)
                st.append((current_depth+1, p.right))
                st.append((current_depth+1, p.left))
        return result[::-1]
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
