# Assignment #A: 图论：算法，树算及栈

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 20743: 整人的提词本

http://cs101.openjudge.cn/practice/20743/



思路：



代码

```python
def translate(s):
    stack = []
    queue = []
    for char in s:
        if char != ")":
            stack.append(char)
        else:
            while (a := stack.pop()) != "(":
                queue.append(a)
            while queue:
                stack.append(queue.pop(0))
    return "".join(stack)

s = input()
print(translate(s))

```



代码运行截图

<img width="959" alt="截屏2024-04-30 20 14 47" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/51201d01-5b4c-470e-af2a-352f0fdb17b7">




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



代码运行截图 ==（至少包含有"Accepted"）==

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



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="952" alt="截屏2024-04-30 20 46 43" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/7f904b90-6649-45ff-b784-19600fc6ef99">




### 04115: 鸣人和佐助

bfs, http://cs101.openjudge.cn/practice/04115/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 05442: 兔子与星空

Prim, http://cs101.openjudge.cn/practice/05442/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==





