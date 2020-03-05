## 路径总和III
**题目**：
给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。


**示例**：
```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1.  5 -> 3
2.  5 -> 2 -> 1
3.  -3 -> 11
```

我的解法：BFS遍历，在遍历过程中记录所有的和

**submission 1**:
```python
from collections import deque
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:
        if not root:
            return 0
        queue = deque([(root, [0])])
        count = 0
        while queue:
            node, lst = queue.popleft()
            tmp_lst = []
            for i in lst:
                tmp = i+node.val
                if tmp == sum:
                    count += 1
                tmp_lst.append(tmp)
            tmp_lst.append(0)
            if node.left:
                queue.append((node.left, tmp_lst))
            if node.right:
                queue.append((node.right, tmp_lst))
        return count
```


**改进思路1**：
同样的思路，改用递归dfs

**submission 2**：
```python
from collections import deque
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:
        if not root:
            return 0
        def dfs(root, sums):
            left, right = 0, 0
            temp = [root.val + num for num in sums] + [root.val]
            if root.left:
                left = dfs(root.left, temp)
            if root.right:
                right = dfs(root.right, temp)
            return temp.count(sum)+left+right
        return dfs(root, [])
```


**改进思路2**：
双递归
- 先简化为以根结点为起点的路径和有多少，递归求解此问题
- 再对每一个节点求解上述问题，第二层递归
- 重复计算很多，优化空间大

**submission 3**：
```python
from collections import deque
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:
        if not root:
            return 0
        #count = self.dfs(root,sum)
        return self.dfs(root,sum) + self.pathSum(root.left, sum) + self.pathSum(root.right, sum)

    def dfs(self, root, sum):
        if not root:
            return 0
        count = 0
        if sum-root.val == 0:
            count += 1
        return count + self.dfs(root.left, sum-root.val) + self.dfs(root.right, sum-root.val)
```


**改进思路3**：前缀和+hashmap优化
- [前缀和](https://leetcode-cn.com/problems/path-sum-iii/solution/qian-zhui-he-di-gui-hui-su-by-shi-huo-de-xia-tian/)

**submission 4**：
```python
from collections import deque
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:
        if not root:
            return 0
        hashmap = {0:1}

        def dfs(root, cursum, hashmap):
            if not root:
                return 0
            cursum += root.val
            res = hashmap.get(cursum-sum,0)
            hashmap[cursum] = hashmap.get(cursum,0)+1
            res += dfs(root.left, cursum, hashmap)
            res += dfs(root.right, cursum, hashmap)
            hashmap[cursum] -= 1
            return res
        return dfs(root,0,hashmap)
```


<font color="#FF0000">**Attention**</font>:

- 
