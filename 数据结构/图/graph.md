## Graph
### 邻接矩阵实现
```python
infinity = float("inf")

class AdjGraphError(TypeError):
    pass

class Graph():
    def __init__(self, mat, unconn=0):
        vnum = len(mat)
        for x in mat:
            if len(x) != vnum:
                raise ValueError
        self._mat = [mat[i][:] for i in range(vnum)]
        self._unconn = unconn
        self._vnum = vnum

    def vertex_num(self):
        return self._vnum

    def _invalid(self, v):
        return v < 0 or v >= self._vnum

    def add_vertex(self, v):
        raise AdjGraphError(
            "Adj Matrix does not support 'add_vertex'")

    def add_edge(self, vi, vj, val=1):
        if self._invalid(vi) or self._invalid(vj):
            raise AdjGraphError
        self._mat[vi][vj] = val

    def get_edge(self, vi, vj):
        if self._invalid(vi) or self._invalid(vj):
            raise AdjGraphError
        return self._mat[vi][vj]

    def out_edges(self, vi):
        if self._invalid(vi):
            raise AdjGraphError
        return self._out_edges(self._mat[vi], self._unconn)

    @staticmethod
    def _out_edges(row, unconn):
        edges = []
        for i, val in enumerate(row):
            if val != unconn:
                edges.append((i, val))
        return edges

    def __str__(self):
        return "[\n" + "\n".join(map(str, self.mat)) + "\n]"\
               + "\nUnconnected: " + str(infinity)
```

### 邻接表实现
```python
class GraphAL(Graph):
    def __init__(self, mat=[], unconn=0):
        vnum = len(mat)
        for x in mat:
            if len(x) != vnum:
                raise ValueError
        self._mat = [Graph._out_edges(mat[i], unconn) for i in range(vnum)]
        self._vnum = vnum
        self._unconn = unconn

    def add_vertex(self): # For new vertex, return an index allocated
        self._mat.append([])
        self._vnum += 1
        return self._vnum - 1

    def add_edge(self, vi, vj, val = 1):
        if self._vnum == 0:
            raise AdjGraphError
        if self._invalid(vi) or self._invalid(vj):
            raise AdjGraphError
        row = self._mat[vi]
        for i in range(len(row)):
            if row[i][0] == vj: # replace a value for mat[vi][vj]
                self.mat[vi][i] = (vj, val)
                return
            if row[i][0] > vj:
                break
        else:  # break则不执行else
            i += 1
        self._mat[vi].insert(i, (vj, val))

    def get_edge(self, vi, vj):
        if self._invalid(vi) or self._invalid(vj):
            raise AdjGraphError
        for i, val in self._mat[vi]:
            if i == vj:
                return val
        return self._unconn

    def out_edges(self, vi):
        if self._invalid(vi) or self._invalid(vj):
            raise AdjGraphError
        return self._mat[vi]
```

### 遍历算法
#### 非递归深度优先遍历
```python
def DFS_graph(graph, v0):
    vnum = graph.vertex_number()
    visited = [0]*vnum
    visited[v0] = 1
    DFS_seq = [v0]
    st = SStack()
    st.push((0, graph.out_edges(v0)))
    while not st.is_empty():
        i, edges = st.pop()
        if i < len(edges):
            v, e = edges[i]
            st.push((i+1, edges))
            if not visited[v]:
                visited[v] = 1
                DFS_seq.append(v)
                st.push((0, graph.out_edges(v)))
    return DFS_seq
```

### 生成树
#### DFS生成树（递归定义）
```python
def DFS_span_forest(graph):
    vnum = graph.vertex_num()
    span_forest = [None]*vnum

    def dfs(graph, v):
        nonlocal span_forest
        for u, w in graph.out_edges(v):
            if span_forest(u) is None:
                span_forest[u] = (v, w)
                dfs(graph, u)
    
    for v in range(vnum):
        if span_forest[v] is None:
            span_forest[v] = (v, 0)
            dfs(graph, v)
    return span_forest
```

### 最小生成树
#### Kruskal算法
**基本方法：**
* 初始时取包含G中所有n个顶点但没有任何边的孤立点子图T=(V,{})，T里的每个顶点自成一个连通分量。通过不断扩充T的方式构造G的最小生成树。
* 将边集E中的边按权值递增的顺序排序，在构造中的每一步顺序地检查这个边序列，找到下一条（最短的）两端点位于T的两个不同连通分量的边e，把e加入T。这导致两个连通分量由于边e的连接而变成了一个连通分量。
* 每次操作使T减少一个连通分量。不断重复这个动作加入新边，直到T中所有顶点都包含在一个连通分量里为止，这个连通分量就是G的一棵最小生成树。

```python
def Kruskal(graph):
    vnum = graph.vertex_num()
    reps = [i for i in range(vnum)]  # 代表元
    mst, edges = [], []
    for vi in range(vnum):
        for v, w in graph.out_edges(vi):
            edges.append((w, (vi, v)))
    edges.sort()
    for w, e in edges:
        if reps[e[0]] != reps[e[1]]:
            mst.append((e, w))  #((vi, vj), w)
            if len(mst) == vnum-1:
                break
            rep, orep = reps[e[0]], reps[e[1]]
            for i in range(vnum):
                if reps[i] == orep:
                    reps[i] = rep
    return mst
```

#### Prim算法
**基本方法**
* 从图从图G的顶点集V中任取一顶点（例如取顶点v0）放入集合U中，这时 U = {v0}，边集合TE = { }，T=(U, TE)是一棵树
* 检查所有一个顶点在集合U里、另一顶点在集合V–U的边，找出其中权最小的边 e = (u, v) (u∈U，v∈V-U)，将顶点v加入集合U，并将e加入TE。(U, TE)仍是一棵树
* 重复上面步骤直至U = V（树中包含所有顶点）。这时TE有n-1条边，T=(U, TE)就是G的一棵最小生成树

```python
def Prim(graph):
    vnum = graph.vertex_num()
    mst = [None]*vnum
    cands = PrioQueue([(0,0,0)]) # PrioQueue中的元素为(w, u, v)
    count = 0
    while count < vnum and not cands.is_empyt():
        w, u, v = cands.dequeue()
        if mst[v]:
            continue
        mst[v] = ((u, v), w)
        for vi, w in graph.out_edges(v):
            if not mst[vi]:
                cands.enqueue((w, v, vi))
        count += 1
    return mst
```

### 最短路径
#### Dijkstra
```python
def Dijkstra_shortest_path(graph, v0):
    vnum = graph.vertex_num()
    pahts = [None]*vnum   # path[v] = (v', p), v'表示前置顶点, p是该路径的长度，None表示v还不在U里
    count = 0
    cdis = PrioQueue([(0,v0,v0)]) # (p, u, v)，u表示U中顶点，v表示V-U中顶点
    while count < vnum and not cdis.is_empty():
        plen, u, v = cdis.dequeue()
        if paths[v]:
            continue
        paths[v] = (u, plen)
        for vi, w in graph.out_edges(v):
            if not path[vi]:
                cids.enqueue((plen+w, v, vi))
        count += 1
    return paths
```

#### [Floyd](https://blog.csdn.net/fengchi863/article/details/80036586)
```python
def Floyd_all_shortest_path(graph):
    vnum = graph.vertex_num()
    a = [[graph.get_edge(i,j) for j in range(vnum)] for i in range(vnum)]
    nvertex = [[-1 if a[i][j] == inf else j for j in range(vnum)] for i in range(vnum)]
    for k in range(vnum):
        for i in range(vnum):
            for j in range(vnum):
                if a[i][j] > a[i][k] + a[k][j]:
                    a[i][j] = a[i][k] + a[k][j]
                    nvertex[i][j] = nvertex[i][k]
    return a, nvertex
```

### 拓扑排序
```python
def topsort(graph):
    vnum = graph.vertex_num()
    indegree, toposeq = [0]*vnum, []
    for vi in range(vnum):
        for v, w in graph.out_edges(vi):
            indegree[v] += 1
    
    zerov = -1
    for vi in range(vnum):
        if indegree[vi] == 0:   # indegree[vi] == 0, 那么indegree[vi]没用了，可以用来记录下一个入度为0的下标
            indegree[vi] = zerov
            zerov = vi

    for n in range(vnum):
        if zerov == -1:
            return False
        vi = zerov
        zerov = indegree[zerov]
        toposeq.append(vi)
        for v, w in graph.out_edges(vi):
            indegree[v] -= 1
            if indegree[v] == 0:
                indegree[v] = zerov
                zerov = v
    return toposeq
```

### 关键路径
```python
def critical_paths(graph):
    def event_earliest_time(vnum, grpah, toposeq):
        ee = [0]*vnum
        for i in toposeq:
            for j, w in graph.out_edges(i):
                if ee[i] + w > ee[j]:
                    ee[j] = ee[i] + w
        return ee

    def event_latest_time(vnum, graph, toposeq, eelast):
        le = [eelast]*vnum
        for k in range(vnum-2, -1, -1):
            i = toposeq[k]
            for j, w in graph.out_edges(i):
                if le[j] - w < le[i]:
                    le[i] = le[j] - w
        return le
    
    def crt_paths(vnum, graph, ee, le):
        crt_actions = []  # action指的是图中的边
        for i in range(vnum):
            for j, w in graph.out_edges(i):
                if ee[i] = le[j] - w:
                    crt_actions.append((i,j,ee[i]))
        return crt_paths
    
    toposeq = toposort(graph)
    if not toposeq:
        return False
    vnum = graph.vertex_num()
    ee = event_earliest_time(vnum, grpah, toposeq)
    le = event_latest_time(vnum, graph, toposeq, ee[-1])
    return crt_paths(vnum, graph, ee, le)
```
