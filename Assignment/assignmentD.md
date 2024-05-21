# Assignment #D: May月考

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)


## 1. 题目

### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：在每个节点对起止点进行标记，当一个位置有多个起止点时，采用数字累加的方式



代码

```python
L, M = map(int, input().split())
treeList = [0 for i in range(L + 1)]
treeNum = 0
for i in range(M):
    intervalBegin, intervalEnd = map(int, input().split())
    treeList[intervalBegin] += 1
    treeList[intervalEnd] -= 1
tag = 0
for i in range(L + 1):
    if tag == 0 and treeList[i] == 0:
        treeNum += 1
    tag += treeList[i]
print(treeNum)

```



代码运行截图 ==（至少包含有"Accepted"）==

<img width="964" alt="截屏2024-05-21 19 11 02" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/578c235d-f4b1-49b3-8fbf-81d0738439eb">




### 20449: 是否被5整除

http://cs101.openjudge.cn/practice/20449/


代码

```python
def isDividedby5(A):
    answer = ""
    for i in range(len(A)):
        if int(A[: i + 1], 2) % 5 == 0:
            answer += "1"
        else:
            answer += "0"
    print(answer)


A = input()
isDividedby5(A)

```



代码运行截图 ==（至少包含有"Accepted"）==

<img width="962" alt="截屏2024-05-21 19 20 56" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/67a03861-7171-4294-8706-1acb0c9dd18c">




### 01258: Agri-Net

http://cs101.openjudge.cn/practice/01258/



思路：



代码

```python
from heapq import heappop, heappush


while True:
    try:
        n = int(input())
    except:
        break
    mat, cur = [], 0
    for i in range(n):
        mat.append(list(map(int, input().split())))
    d, v, q, cnt = [100000 for i in range(n)], set(), [], 0
    d[0] = 0
    heappush(q, (d[0], 0))
    while q:
        x, y = heappop(q)
        if y in v:
            continue
        v.add(y)
        cnt += d[y]
        for i in range(n):
            if d[i] > mat[y][i]:
                d[i] = mat[y][i]
                heappush(q, (d[i], i))
    print(cnt)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="963" alt="截屏2024-05-21 19 29 49" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/242a3476-4d36-444c-aa0b-93fbc62dea63">




### 27635: 判断无向图是否连通有无回路(同23163)

http://cs101.openjudge.cn/practice/27635/



思路：



代码

```python
def is_connected(graph, n):
    visited = [False] * n
    stack = [0]
    visited[0] = True

    while stack:
        node = stack.pop()
        for neighbor in graph[node]:
            if not visited[neighbor]:
                stack.append(neighbor)
                visited[neighbor] = True

    return all(visited)

def has_cycle(graph, n):
    def dfs(node, visited, parent):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                if dfs(neighbor, visited, node):
                    return True
            elif parent != neighbor:
                return True
        return False

    visited = [False] * n
    for node in range(n):
        if not visited[node]:
            if dfs(node, visited, -1):
                return True
    return False

n, m = map(int, input().split())
graph = [[] for _ in range(n)]
for _ in range(m):
    u, v = map(int, input().split())
    graph[u].append(v)
    graph[v].append(u)

connected = is_connected(graph, n)
has_loop = has_cycle(graph, n)
print("connected:yes" if connected else "connected:no")
print("loop:yes" if has_loop else "loop:no")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="953" alt="截屏2024-05-21 19 31 39" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/1aef3096-69a8-40c9-8335-2cbe529ccce2">






### 27947: 动态中位数

http://cs101.openjudge.cn/practice/27947/



思路：



代码

```python
import heapq

def dynamic_median(nums):
    min_heap = []
    max_heap = []

    median = []
    for i, num in enumerate(nums):
        if not max_heap or num <= -max_heap[0]:
            heapq.heappush(max_heap, -num)
        else:
            heapq.heappush(min_heap, num)
        if len(max_heap) - len(min_heap) > 1:
            heapq.heappush(min_heap, -heapq.heappop(max_heap))
        elif len(min_heap) > len(max_heap):
            heapq.heappush(max_heap, -heapq.heappop(min_heap))
        if i % 2 == 0:
            median.append(-max_heap[0])

    return median

T = int(input())
for _ in range(T):
    nums = list(map(int, input().split()))
    median = dynamic_median(nums)
    print(len(median))
    print(*median)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==


<img width="978" alt="截屏2024-05-21 19 35 02" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/a5ae819b-7eb6-4f7b-8464-356b0f1a8f03">



### 28190: 奶牛排队

http://cs101.openjudge.cn/practice/28190/



思路：



代码

```python
from bisect import bisect_right as bl
lis,q1,q2,ans=[int(input())for _ in range(int(input()))],[-1],[-1],0
for i in range(len(lis)):
    while len(q1)>1 and lis[q1[-1]]>=lis[i]:q1.pop()
    while len(q2)>1 and lis[q2[-1]]<lis[i]:q2.pop()
    id=bl(q1,q2[-1])
    if id<len(q1):ans=max(ans,i-q1[id]+1)
    q1.append(i)
    q2.append(i)
print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="953" alt="截屏2024-05-21 19 36 38" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/eb458856-30a5-4fe5-8ff5-db1be8fd7703">




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

看完题解后，有部分答案还是挺有值得学习的地方，数算不能自己孤军奋战，需要积极学习别人的写法以提升自己



