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



代码运行截图

<img width="966" alt="截屏2024-04-09 18 46 12" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/4b487a07-05f0-4cc1-938e-9538292ee43d">




### 18160: 最大连通域面积

matrix/dfs similar, http://cs101.openjudge.cn/practice/18160



思路：



代码

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==





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



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 04089: 电话号码

trie, http://cs101.openjudge.cn/practice/04089/

Trie 数据结构可能需要自学下。



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 04082: 树的镜面映射

http://cs101.openjudge.cn/practice/04082/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==





