# Assignment #5: "树"算：概念、表示、解析、遍历

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 27638: 求二叉树的高度和叶子数目

http://cs101.openjudge.cn/practice/27638/



代码

```python
class TreeNode:
    def __init__(self):
        self.parent = None
        self.left = None
        self.right = None


def tree_height(node):
    if node is None:
        return -1
    return max(tree_height(node.left), tree_height(node.right)) + 1


def root(node):
    if node.parent is None:
        return node
    return root(node.parent)


def count_leaves(node):
    if node is None:
        return 0
    elif node.left is None and node.right is None:
        return 1
    return count_leaves(node.left)+count_leaves(node.right)


n = int(input())
nodes = [TreeNode() for _ in range(n)]
for i in range(n):
    left_index, right_index = map(int, input().split())
    if left_index != -1:
        nodes[i].left = nodes[left_index]
        nodes[left_index].parent = nodes[i]
    if right_index != -1:
        nodes[i].right = nodes[right_index]
        nodes[right_index].parent = nodes[i]
print(tree_height(root(nodes[0])),count_leaves(root(nodes[0])))

```




### 24729: 括号嵌套树

http://cs101.openjudge.cn/practice/24729/



代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []


def preorder(node):
    if node.children == []:
        return node.value
    return node.value + "".join(map(preorder, node.children))


def postorder(node):
    if node.children == []:
        return node.value
    return "".join(map(postorder, node.children)) + node.value


exp = input()
stack = []
for char in exp:
    if char.isalpha():
        node = TreeNode(char)
        if stack:
            stack[-1].children.append(node)
    elif char == "(":
        stack.append(node)
    elif char == ")":
        node = stack.pop()
root = node
print(preorder(root))
print(postorder(root))

```



### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/


代码

```python
def arrangement(file):
    stack = []
    print("ROOT")
    depth = 0
    for i in range(len(file)):
        if file[i][0] == "f":
            stack.append([file[i], depth])
        elif file[i][0] == "d":
            depth += 1 
            print("|     " * depth, file[i], sep="")
        elif file[i][0] == "]":
            temp = []
            while stack != [] and stack[-1][1] == depth:
                temp.append(stack.pop()[0])
            temp.sort()
            for temp_file in temp:
                print("|     " * depth, temp_file, sep="")
            depth -= 1
    stack.sort()
    for temp_file in stack:
        print(temp_file[0], sep = '')

set_num = 0
while True:
    set_num += 1
    file = []
    while True:
        a = input()
        if a != '*' and a != '#':
            file.append(a)
        else:
            break
    if a == '#':
        break
    if set_num != 1:
        print("\nDATA SET %d:" % set_num)
    else:
        print("DATA SET %d:" % set_num)
    arrangement(file)

```




### 25140: 根据后序表达式建立队列表达式

http://cs101.openjudge.cn/practice/25140/



思路：建立起表达式树，按层次遍历表达式树的结果前后颠倒就得到队列表达式


代码

```python
def root(tree_list):
    n = len(tree_list)
    root_list = [1] * (n + 1)
    for i in range(n):
        root_list[tree_list[i][0]] = 0
        root_list[tree_list[i][1]] = 0
    return root_list.index(1)


def queexp(exp):
    tree_list = [[]] * len(exp)
    stack = []
    for i in range(len(exp)):
        if exp[i].islower():
            stack.append(i)
            tree_list[i] = [-1, -1]
        elif exp[i].isupper():
            rightopv = stack.pop()
            leftopv = stack.pop()
            tree_list[i] = [leftopv, rightopv]
            stack.append(i)
    next_layer = [root(tree_list)]
    forward_exp = ''
    while True:
        ed_layer = []
        for i in next_layer:
            forward_exp += exp[i]
            if tree_list[i][0] != -1:
                ed_layer.append(tree_list[i][0])
            if tree_list[i][1] != -1:
                ed_layer.append(tree_list[i][1])
        next_layer = ed_layer
        if next_layer == []:
            break
    return forward_exp[::-1]
    


n = int(input())
for i in range(n):
    exp = input()
    print(queexp(exp))

```



代码运行截图

<img width="751" alt="截屏2024-03-26 16 25 33" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/45d0d110-b699-4537-b7b4-af6dda235a81">




### 24750: 根据二叉树中后序序列建树

http://cs101.openjudge.cn/practice/24750/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 22158: 根据二叉树前中序序列建树

http://cs101.openjudge.cn/practice/22158/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

最近课程有所遗落，本周作业有两题未完成，近期补上





