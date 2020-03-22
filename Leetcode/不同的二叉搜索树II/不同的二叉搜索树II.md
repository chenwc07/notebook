## 不同的二叉搜索树 II
**题目**：
给定一个整数 n，生成所有由 1 ... n 为节点所组成的二叉搜索树。

**示例**：
```
输入: 3
输出:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释:
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

算法1：递归

**submission 1**:
```python
class Solution:
    def generateTrees(self, n: int) -> List[TreeNode]:
        def backtrack(start, end):
            if start > end:
                return [None]
            all_trees = []
            for i in range(start, end+1):
                left_trees = backtrack(start,i-1)
                right_trees = backtrack(i+1, end)

                for l in left_trees:
                    for r in right_trees:
                        root = TreeNode(i)
                        root.left = l
                        root.right = r
                        all_trees.append(root)

            return all_trees
        return backtrack(1, n) if n else []
```


<font color="#FF0000">**Attention**</font>:

- 
