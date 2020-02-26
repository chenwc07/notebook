## 实现 Trie (前缀树)
**题目**：
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

说明:

-你可以假设所有的输入都是由小写字母 a-z 构成的。
-保证所有输入均为非空字符串。

**示例**：
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```

算法1：加入node类并用递归建树

**submission 1**:
```python
class TrieNode():
    def __init__(self, char=None):
        self.char = char
        self.children = {}
        self._is_word = False

        
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.dictionary = TrieNode()


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        if not word:
            return
        self._insert(self.dictionary, word)
        

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        def _search(root, word):
            if not word:
                return root._is_word
            if word[0] not in root.children:
                return False
            return _search(root.children[word[0]], word[1:])
        return _search(self.dictionary, word)

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        def _startsWith(root, prefix):
            if not prefix:
                return True
            if prefix[0] not in root.children:
                return False
            return _startsWith(root.children[prefix[0]], prefix[1:])
        return _startsWith(self.dictionary, prefix)

    def _insert(self, root, word):
        if not word:
            root._is_word = True
            return
        if word[0] in root.children:
            self._insert(root.children[word[0]], word[1:])
            return
        if word[0] not in root.children:
            root.children[word[0]] = TrieNode(word[0])
            self._insert(root.children[word[0]], word[1:])
            return
```


**改进思路1**：
用嵌套的字典表示树。极度简洁。

**submission 2**：
```python
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.lookup = {}


    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        tree = self.lookup
        for s in word:
            if s not in tree:
                tree[s] = {}
            tree = tree[s]
        tree['#'] = '#'


    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        tree = self.lookup
        for s in word:
            if s not in tree:
                return False
            tree = tree[s]
        return '#' in tree


    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        tree = self.lookup
        for s in prefix:
            if s not in tree:
                return False
            tree = tree[s]
        return True
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
