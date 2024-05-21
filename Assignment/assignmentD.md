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
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==







### 27947: 动态中位数

http://cs101.openjudge.cn/practice/27947/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 28190: 奶牛排队

http://cs101.openjudge.cn/practice/28190/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==





