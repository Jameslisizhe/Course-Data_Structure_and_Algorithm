# Assignment #A: 图论：算法，树算及栈

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 20743: 整人的提词本

http://cs101.openjudge.cn/practice/20743/


代码

```python
from collections import deque

def translate(s):
    stack = []
    queue = deque()
    for char in s:
        if char != ")":
            stack.append(char)
        else:
            while (a := stack.pop()) != "(":
                queue.append(a)
            while queue:
                stack.append(queue.popleft())
    return "".join(stack)

s = input()
print(translate(s))
```



### 02255: 重建二叉树

http://cs101.openjudge.cn/practice/02255/



代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def build_tree(preorder, inorder):
    if not preorder:
        return None
    root = TreeNode(preorder[0])
    index = inorder.index(preorder[0])
    root.left = build_tree(preorder[1 : index + 1], inorder[:index])
    root.right = build_tree(preorder[index + 1 :], inorder[index + 1 :])
    return root


def postorder(node):
    if not node:
        return ""
    return postorder(node.left) + postorder(node.right) + node.value


while True:
    try:
        preorder, inorder = input().split()
        print(postorder(build_tree(preorder, inorder)))
    except EOFError:
        break

```



代码运行截图

<img width="949" alt="截屏2024-04-30 20 19 57" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/344210af-816b-4de3-9259-3e15ab5c094b">




### 01426: Find The Multiple

http://cs101.openjudge.cn/practice/01426/

要求用bfs实现



代码

```python
def findMultiple(n):
    t = 0
    while True:
        t += 1
        m = int(bin(t)[2:])
        if m % n == 0:
            return m

while True:
    n = int(input())
    if n:
        print(findMultiple(n))
    else:
        break

```



代码运行截图

<img width="952" alt="截屏2024-04-30 20 46 43" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/7f904b90-6649-45ff-b784-19600fc6ef99">




### 04115: 鸣人和佐助

bfs, http://cs101.openjudge.cn/practice/04115/



思路：



代码

```python
from collections import deque

M, N, T = map(int, input().split())
graph = [list(input()) for i in range(M)]
direc = [(0,1), (1,0), (-1,0), (0,-1)]
start, end = None, None
for i in range(M):
    for j in range(N):
        if graph[i][j] == '@':
            start = (i, j)
def bfs():
    q = deque([start + (T, 0)])
    visited = [[-1]*N for i in range(M)]
    visited[start[0]][start[1]] = T
    while q:
        x, y, t, time = q.popleft()
        time += 1
        for dx, dy in direc:
            if 0<=x+dx<M and 0<=y+dy<N:
                if (elem := graph[x+dx][y+dy]) == '*' and t > visited[x+dx][y+dy]:
                    visited[x+dx][y+dy] = t
                    q.append((x+dx, y+dy, t, time))
                elif elem == '#' and t > 0 and t-1 > visited[x+dx][y+dy]:
                    visited[x+dx][y+dy] = t-1
                    q.append((x+dx, y+dy, t-1, time))
                elif elem == '+':
                    return time
    return -1
print(bfs())

```



代码运行截图

<img width="959" alt="截屏2024-04-30 21 12 41" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/f734a52b-9694-4383-bdcf-4f2ce0bc5337">




### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/



思路：



代码

```python
def bfs(x, y):
    # 定义方向的偏移量
    directions = [(0, -1), (0, 1), (1, 0), (-1, 0)]
    # 初始化队列，将起点加入队列
    queue = [(x, y)]
    # 初始化距离字典，将起点的距离设为0，其他节点设为无穷大
    distances = {(x, y): 0}	# 不用heap，则需要用二维表

    while queue:
        # 弹出队列中的节点
        current_x, current_y = queue.pop(0)

        # 遍历四个方向上的相邻节点
        for dx, dy in directions:
            new_x, new_y = current_x + dx, current_y + dy

            # 判断新节点是否在合法范围内
            if 0 <= new_x < m and 0 <= new_y < n:
                # 判断新节点是否为墙
                if d[new_x][new_y] != '#':
                    # 计算新节点的距离
                    new_distance = distances[(current_x, current_y)] + abs(int(d[new_x][new_y]) - int(d[current_x][current_y]))

                    # 如果新节点的距离小于已记录的距离，则更新距离字典和队列
                    if (new_x, new_y) not in distances or new_distance < distances[(new_x, new_y)]:
                        distances[(new_x, new_y)] = new_distance
                        queue.append((new_x, new_y))

    return distances

# 读取输入
m, n, p = map(int, input().split())
d = []
for _ in range(m):
    row = input().split()
    d.append(row)

for _ in range(p):
    # 读取起点和终点坐标
    x1, y1, x2, y2 = map(int, input().split())

    # 判断起点和终点是否为墙
    if d[x1][y1] == '#' or d[x2][y2] == '#':
        print('NO')
        continue

    # 使用BFS计算最短距离
    distances = bfs(x1, y1)

    # 输出结果，如果终点在距离字典中，则输出对应的最短距离，否则输出'NO'
    if (x2, y2) in distances:
        print(distances[(x2, y2)])
    else:
        print('NO')

```



代码运行截图

<img width="977" alt="截屏2024-04-30 21 14 04" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/5e72aa5b-ed91-426d-88bd-0d06d79994f5">




### 05442: 兔子与星空

Prim, http://cs101.openjudge.cn/practice/05442/



思路：



代码

```python
import heapq

def prim(graph, start):
    mst = []
    used = set([start])
    edges = [
        (cost, start, to)
        for to, cost in graph[start].items()
    ]
    heapq.heapify(edges)

    while edges:
        cost, frm, to = heapq.heappop(edges)
        if to not in used:
            used.add(to)
            mst.append((frm, to, cost))
            for to_next, cost2 in graph[to].items():
                if to_next not in used:
                    heapq.heappush(edges, (cost2, to, to_next))

    return mst

def solve():
    n = int(input())
    graph = {chr(i+65): {} for i in range(n)}
    for i in range(n-1):
        data = input().split()
        star = data[0]
        m = int(data[1])
        for j in range(m):
            to_star = data[2+j*2]
            cost = int(data[3+j*2])
            graph[star][to_star] = cost
            graph[to_star][star] = cost
    mst = prim(graph, 'A')
    print(sum(x[2] for x in mst))

solve()

```



代码运行截图

<img width="960" alt="截屏2024-04-30 21 16 02" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/ba2a6ec7-aac4-4b88-834c-59c7d7379a2a">




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

前几道作业题目较为简单，后几道的算法较难，通过题解复习并加深了对bfs的理解



