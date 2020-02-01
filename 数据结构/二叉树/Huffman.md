## Huffman Tree
定义：有实数集 W = {w1 ,w2, …,wm}，T是一棵扩充二叉树
包含m个分别以 wi（i = 1, 2, …, m）为权的外部结点，且其带权
外部路径长度WPL 达到最小，则称 T 为数据集 W 的最优二叉树或哈夫曼树

### 构造哈夫曼树的算法
给定一组实数，对应的哈夫曼树可以通过哈夫曼算法得到
* 输入实数集W = {w1 ,w2, …,wm}
* 维护包含 构造中维护包含m棵二叉树的集合F，开始时F = {T1, T2, …, Tm}，其中Ti是一棵只包含权为wi的根结点的单点二叉树
* 算法过程中重复执行下面两个步骤，直到F中剩下一棵树为止：
  * 构造一棵新二叉树，其左右子树是从集合F中选取的两棵权值最小的二叉树，其根结点的权值设置为这两棵子树的根结点的权值之和
  * 将所选的两棵二叉树从F从删除，把新构造的二叉树加入F。

### 算法实现
```python
class HTNode(BinTNode):
    def __lt__(self, othernode):
        return self.data < othernode.data

class HuffmanPrioQ(PrioQueue):
    def number(self):
        return len(self._elems)

def HuffmanTree(weights):
    qu = HuffmanPrioQ()
    for w in weights:
        qu.enqueue(HTNode(w))
    while qu.number() > 1:
        t1 = qu.dequeue()
        t2 = qu.dequeue()
        x = t1.data + t2.data
        qu.enqueue(HTNode(x, t1, t2))
    return qu.dequeue()
```

