# Assignment #8: 图论：概念、遍历，及 树算

2024 spring, Complied by 李思哲 物理学院


**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 19943: 图的拉普拉斯矩阵

matrices, http://cs101.openjudge.cn/practice/19943/

请定义Vertex类，Graph类，然后实现


代码

```python
class Vertex:
    def __init__(self, key):
        self.id = key
        self.connectedTo = {}

    def addNeighbor(self, nbr, weight=0):
        self.connectedTo[nbr] = weight


class Graph:
    def __init__(self):
        self.vertList = {}
        self.numVertices = 0

    def addVertex(self, key):
        self.numVertices = self.numVertices + 1
        newVertex = Vertex(key)
        self.vertList[key] = newVertex
        return newVertex

    def addEdge(self, f, t, weight=0):
        if f not in self.vertList:
            nv = self.addVertex(f)
        if t not in self.vertList:
            nv = self.addVertex(t)
        self.vertList[f].addNeighbor(self.vertList[t], weight)


def buildLaplaceMatrix(graph):
    laplaceMatrix = []
    n = graph.numVertices
    for i in range(n):
        laplaceMatrix.append([])
        for j in range(n):
            laplaceMatrix[i].append(
                len(graph.vertList[j].connectedTo) * int(i == j)
                - int(graph.vertList[i] in graph.vertList[j].connectedTo)
            )
    return laplaceMatrix


graph = Graph()
n, m = map(int, input().split())
for i in range(n):
    graph.addVertex(i)
for i in range(m):
    a, b = map(int, input().split())
    graph.addEdge(a, b)
    graph.addEdge(b, a)
laplaceMatrix = buildLaplaceMatrix(graph)
for i in range(n):
    print(*laplaceMatrix[i])

```




### 18160: 最大连通域面积

matrix/dfs similar, http://cs101.openjudge.cn/practice/18160



思路：



代码

```python
def dfs(matrix, row, col, visited):
    if row < 0 or row >= len(matrix) or col < 0 or col >= len(matrix[0]) \
            or matrix[row][col] != 'W' or visited[row][col]:
        return 0

    visited[row][col] = True
    size = 1

    for dr in [-1, 0, 1]:
        for dc in [-1, 0, 1]:
            size += dfs(matrix, row + dr, col + dc, visited)

    return size


def max_connected_area(matrix):
    max_area = 0
    visited = [[False for _ in range(len(matrix[0]))] for _ in range(len(matrix))]

    for row in range(len(matrix)):
        for col in range(len(matrix[0])):
            if matrix[row][col] == 'W' and not visited[row][col]:
                area = dfs(matrix, row, col, visited)
                max_area = max(max_area, area)

    return max_area


def main():
    T = int(input())
    for _ in range(T):
        N, M = map(int, input().split())
        matrix = [input().strip() for _ in range(N)]
        print(max_connected_area(matrix))


if __name__ == "__main__":
    main()

```



代码运行截图 ==（至少包含有"Accepted"）==

<img width="967" alt="截屏2024-04-16 22 16 49" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/a48d19d8-ee9b-43dc-b39d-0166c400818c">




### sy383: 最大权值连通块

https://sunnywhy.com/sfbj/10/3/383



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 03441: 4 Values whose Sum is 0

data structure/binary search, http://cs101.openjudge.cn/practice/03441



思路：字典



代码

```python
from collections import defaultdict

def find_0_sum(A, B, C, D):
    ABdict = defaultdict(int)
    num = 0
    for a in A:
        for b in B:
            ABdict[a + b] += 1
    for c in C:
        for d in D:
            if - c - d in ABdict:
                num += ABdict[- c - d]
    return num


n = int(input())
A, B, C, D = [], [], [],[]
for i in range(n):
    a, b, c, d = map(int, input().split())
    A.append(a)
    B.append(b)
    C.append(c)
    D.append(d)
print(find_0_sum(A, B, C, D))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 04089: 电话号码

trie, http://cs101.openjudge.cn/practice/04089/

Trie 数据结构可能需要自学下。



思路：



代码

```python
class TrieNode:
    def __init__(self):
        self.child={}


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, nums):
        curnode = self.root
        for x in nums:
            if x not in curnode.child:
                curnode.child[x] = TrieNode()
            curnode=curnode.child[x]

    def search(self, num):
        curnode = self.root
        for x in num:
            if x not in curnode.child:
                return 0
            curnode = curnode.child[x]
        return 1


t = int(input())
p = []
for _ in range(t):
    n = int(input())
    nums = []
    for _ in range(n):
        nums.append(str(input()))
    nums.sort(reverse=True)
    s = 0
    trie = Trie()
    for num in nums:
        s += trie.search(num)
        trie.insert(num)
    if s > 0:
        print('NO')
    else:
        print('YES')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="976" alt="截屏2024-04-16 22 36 28" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/9abf024e-6889-4bd6-b840-489fb92add58">




### 04082: 树的镜面映射

http://cs101.openjudge.cn/practice/04082/



思路：



代码

```python
from collections import deque

class TreeNode:
    def __init__(self, x):
        self.x = x
        self.children = []

def create_node():
    return TreeNode('')

def build_tree(tempList, index):
    node = create_node()
    node.x = tempList[index][0]
    if tempList[index][1] == '0':
        index += 1
        child, index = build_tree(tempList, index)
        node.children.append(child)
        index += 1
        child, index = build_tree(tempList, index)
        node.children.append(child)
    return node, index

def print_tree(p):
    Q = deque()
    s = deque()

    while p is not None:
        if p.x != '$':
            s.append(p)
        p = p.children[1] if len(p.children) > 1 else None

    while s:
        Q.append(s.pop())

    while Q:
        p = Q.popleft()
        print(p.x, end=' ')
        if p.children:
            p = p.children[0]
            while p is not None:
                if p.x != '$':
                    s.append(p)
                p = p.children[1] if len(p.children) > 1 else None
            while s:
                Q.append(s.pop())


n = int(input())
tempList = input().split()

root, _ = build_tree(tempList, 0)

print_tree(root)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="995" alt="截屏2024-04-16 22 35 26" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/71d06542-e834-4773-a2f3-57d67672f312">




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

近期期中考试较忙，仅完成了个别题目，剩余题目，近期抓紧补上


