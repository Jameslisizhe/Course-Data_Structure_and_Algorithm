# Assignment #F: All-Killed 满分

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)


## 1. 题目

### 22485: 升空的焰火，从侧面看

http://cs101.openjudge.cn/practice/22485/



思路：



代码

```python
from collections import deque

def right_view(n, tree):
    queue = deque([(1, tree[1])])  # start with root node
    right_view = []

    while queue:
        level_size = len(queue)
        for i in range(level_size):
            node, children = queue.popleft()
            if children[0] != -1:
                queue.append((children[0], tree[children[0]]))
            if children[1] != -1:
                queue.append((children[1], tree[children[1]]))
        right_view.append(node)

    return right_view

n = int(input())
tree = {1: [-1, -1] for _ in range(n+1)}  # initialize tree with -1s
for i in range(1, n+1):
    left, right = map(int, input().split())
    tree[i] = [left, right]

result = right_view(n, tree)
print(' '.join(map(str, result)))

```



代码运行截图 ==（至少包含有"Accepted"）==

<img width="1024" alt="截屏2024-05-28 22 58 23" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/6edb0dad-5b7d-4eb4-9334-7e6d63fc9d95">




### 28203:【模板】单调栈

http://cs101.openjudge.cn/practice/28203/



思路：



代码

```python
n = int(input())
a = list(map(int, input().split()))
stack = []

for i in range(n):
    while stack and a[stack[-1]] < a[i]:
        #f[stack.pop()] = i + 1
        a[stack.pop()] = i + 1


    stack.append(i)

while stack:
    a[stack[-1]] = 0
    stack.pop()

print(*a)

```



代码运行截图 ==（至少包含有"Accepted"）==


<img width="958" alt="截屏2024-05-28 23 00 43" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/5e429c45-5f8e-485b-a459-74208837fdf0">



### 09202: 舰队、海域出击！

http://cs101.openjudge.cn/practice/09202/



思路：



代码

```python
from collections import defaultdict

def dfs(node, color):
    color[node] = 1
    for neighbour in graph[node]:
        if color[neighbour] == 1:
            return True
        if color[neighbour] == 0 and dfs(neighbour, color):
            return True
    color[node] = 2
    return False

T = int(input())
for _ in range(T):
    N, M = map(int, input().split())
    graph = defaultdict(list)
    for _ in range(M):
        x, y = map(int, input().split())
        graph[x].append(y)
    color = [0] * (N + 1)
    is_cyclic = False
    for node in range(1, N + 1):
        if color[node] == 0:
            if dfs(node, color):
                is_cyclic = True
                break
    print("Yes" if is_cyclic else "No")

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="970" alt="截屏2024-05-28 23 02 11" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/a519d425-660e-4657-a587-0176110f4d9d">




### 04135: 月度开销

http://cs101.openjudge.cn/practice/04135/



思路：



代码

```python
n,m = map(int, input().split())
expenditure = []
for _ in range(n):
    expenditure.append(int(input()))

def check(x):
    num, s = 1, 0
    for i in range(n):
        if s + expenditure[i] > x:
            s = expenditure[i]
            num += 1
        else:
            s += expenditure[i]
    
    return [False, True][num > m]

# https://github.com/python/cpython/blob/main/Lib/bisect.py
lo = max(expenditure)
# hi = sum(expenditure)
hi = sum(expenditure) + 1
ans = 1
while lo < hi:
    mid = (lo + hi) // 2
    if check(mid):      # 返回True，是因为num>m，是确定不合适
        lo = mid + 1    # 所以lo可以置为 mid + 1。
    else:
        ans = mid    # 如果num==m, mid可能是答案
        hi = mid
        
#print(lo)
print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==


<img width="1037" alt="截屏2024-05-28 23 03 35" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/6c8cf043-b914-4331-b654-c4ad520bbd9d">



### 07735: 道路

http://cs101.openjudge.cn/practice/07735/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 01182: 食物链

http://cs101.openjudge.cn/practice/01182/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

期末太忙，作业六道没做完，这周抓紧时间完成并巩固复习，下周机考加油



