# Assignment #7: April 月考

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)


## 1. 题目

### 27706: 逐词倒放

http://cs101.openjudge.cn/practice/27706/



代码

```python
print(*input().split()[::-1])

```




### 27951: 机器翻译

http://cs101.openjudge.cn/practice/27951/



代码

```python
from collections import deque

def time(M, word_list):
    queue = deque()
    time = 0
    for word in word_list:
        if word not in queue:
            if len(queue) == M:
                queue.popleft()
            queue.append(word)
            time += 1
    return time

M, N = map(int, input().split())
word_list = input().split()
print(time(M, word_list))

```




### 27932: Less or Equal

http://cs101.openjudge.cn/practice/27932/



思路：需考虑k=0和n的边界情况



代码

```python
n, k = map(int, input().split())
edited_list = [1] + sorted(list(map(int, input().split())))
print(edited_list[k] if k == n or edited_list[k + 1] - edited_list[k] else -1)

```




### 27948: FBI树

http://cs101.openjudge.cn/practice/27948/



代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def tree_type(s):
    if all(c == '0' for c in s):
        return 'B'
    elif all(c == '1' for c in s):
        return "I"
    else:
        return "F"


def build_tree(S):
    if len(S) == 1:
        return TreeNode(tree_type(S))
    root = TreeNode(tree_type(S))
    root.left = build_tree(S[:len(S)//2])
    root.right = build_tree(S[len(S)//2:])
    return root

def postorder(node):
    if not node:
        return ""
    return postorder(node.left) + postorder(node.right) + node.value

N = int(input())
S = input()
print(postorder(build_tree(S)))

```



### 27925: 小组队列

http://cs101.openjudge.cn/practice/27925/



代码

```python
def operation(queue, group_end, op):
    if op[0] == "ENQUEUE":
        g_end = group_end[people.get(op[1])]
        if g_end == None:
            queue.append(op[1])
            group_end[people.get(op[1])] = len(queue) - 1
        else:
            queue.insert(g_end + 1, op[1])
            for i in range(len(group_end)):
                if group_end[i] != None and group_end[i] >= g_end:
                    group_end[i] += 1
    elif op[0] == "DEQUEUE":
        print(queue.pop(0))
        for i in range(len(group_end)):
            if group_end[i] != None and group_end[i] != 0:
                group_end[i] -= 1
            elif group_end[i] == 0:
                group_end[i] = None


n = int(input())
people = {}
for i in range(n):
    group = input().split()
    for person in group:
        people[person] = i
queue = []
group_end = [None] * n
while (op := input().split()) != ["STOP"]:
    operation(queue, group_end, op)

```



### 27928: 遍历树

http://cs101.openjudge.cn/practice/27928/



代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []


def traverse_print(root, nodes):
    if root.children == []:
        print(root.value)
        return
    pac = {root.value: root}
    for child in root.children:
        pac[child] = nodes[child]
    for value in sorted(pac.keys()):
        if value in root.children:
            traverse_print(pac[value], nodes)
        else:
            print(root.value)


n = int(input())
nodes = {}
children_list = []
for i in range(n):
    info = list(map(int, input().split()))
    nodes[info[0]] = TreeNode(info[0])
    for child_value in info[1:]:
        nodes[info[0]].children.append(child_value)
        children_list.append(child_value)
root = nodes[[value for value in nodes.keys() if value not in children_list][0]]
traverse_print(root, nodes)

```




## 2. 学习总结和收获

月考题目思维难度不大，但是细节需要十分注意。近期将所有课程已全部补上，对树有了更深的理解，也总结了许多常用的树相关函数。

班上大佬太多，作为C语言选手，仍需努力熟练Python的语法和包的使用，争取让代码更加简洁、高效。





