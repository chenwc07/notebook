## 环形链表II
**题目**：
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

**示例**：
```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```
```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```
```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```


算法1：哈希表，时间复杂度O(n)，空间复杂度也是O(n)
**submission 1**:
```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        if not head:
            return None
        hashmap = set()
        p = head
        while p.next:
            hashmap.add(p)
            p = p.next
            if p in hashmap:
                return p
        return None
```


**改进思路1**：

快慢指针法：
- 快指针走两步，慢指针走一步，直到第一次相遇。
- 此时设立两个新指针，一个在链表头，一个在相遇点，两个指针按同样的速度往前走，相遇点就是所求的入环点。

**submission 2**：
```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        if not head:
            return None
        fast, slow = head, head
        while True:
            if not fast or not fast.next:
                return None
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                break
        slow = head
        while fast != slow:
            fast = fast.next
            slow = slow.next
        return fast
```


<font color="#FF0000">**Attention**</font>:

- 
