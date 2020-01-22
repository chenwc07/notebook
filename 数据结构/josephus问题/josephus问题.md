## josephus问题
假设有n个人围坐一圈，现在要求从第k个人开始报数，报到第m个数的人退出，然后从下一个人开始继续报数并按同样的规则退出，直至所有人退出。要求按顺序输出各出列人的编号。

思路1：
基于Python的list和固定大小的数组的概念，把list看作元素个数固定的对象，只修改元素的值而不改变表的结构。

* 初始
  * 建立一个包含n个人的编号的表
  * 找到第k个人，从那里开始
* 处理过程中把相应元素修改为0的方式表示已出列，重复：
  * 数m个人，遇到表的末端就转回下标0继续
  * 把表示第m个人的表元素修改为0
* n个人出列即结束

```python
def josephus_A(n, k, m):
    people = list(range(1,n+1))
    i = k - 1
    for num in range(n):
        count = 0
        while count < m:
            if people[i] != 0:
                count += 1
            if count == m:
                print(people[i])
                people[i] = 0
            i = (i + 1) % n # 这句必须在输出之后，因为是“报数到第k个人输出”，否则下标会继续移动
```

思路2：
采用顺序表，每退出一个人则将表中对应的元素删除。
```python
def josephus_L(n, k, m):
    people = list(range(1,n+1))
    i = k - 1
    for num in range(n,0,-1):  # num可以表示表的长度
        i = (i + m - 1) % num
        print(people.pop(i))
```

思路3：
用循环链表，编程更加直观。
```python
class Josephus(LCList):
    def turn(self, m):
        for i in range(m):
            self._rear = self._rear.next
    
    def __init__(self, n, k, m):
        LCList.__init__(self)
        for i in range(n):
            self.append(i+1)
        self.turn(k-1)
        while not self.is_empty():
            self.turn(m-1)
            print(self.pop())
```