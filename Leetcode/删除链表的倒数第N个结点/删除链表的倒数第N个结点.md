## 删除链表的倒数第N个结点
**题目**：
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

你能尝试使用一趟扫描实现吗？

**示例**：
```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

算法1：利用间隔为n的双指针，当前方的指针到达末尾时，说明该删除后方指针的下一个结点。

**submission 1**:
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        p, q = head, head
        for _ in range(n+1):
            if q:
                q = q.next
            else:
                head = head.next
                return head
        while q:
            p = p.next
            q = q.next
        p.next = p.next.next
        return head
```


**改进思路1**：
利用链表头部添加的哑节点来使得删除头节点的特殊情况变成一般情况，就不用特别考虑了。

**submission 2**：
```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        temp_head = ListNode(0)
        temp_head.next = head
        p, q = temp_head, temp_head
        for _ in range(n+1):
            if q:
                q = q.next
        while q:
            p = p.next
            q = q.next
        p.next = p.next.next
        return temp_head.next
```



<font color="#FF0000">**Attention**</font>:

- 
