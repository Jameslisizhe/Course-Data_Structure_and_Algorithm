# Assignment #5: "树"算：概念、表示、解析、遍历

Updated 2124 GMT+8 March 17, 2024

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 27638: 求二叉树的高度和叶子数目

http://cs101.openjudge.cn/practice/27638/



思路：递归求高度，遍历求叶数



代码

```python
def depth_tree(node, tree_list):
    if node == -1:
        return 0
    else:
        return (
            max(
                depth_tree(tree_list[node][0], tree_list),
                depth_tree(tree_list[node][1], tree_list),
            )
            + 1
        )


def root(tree_list):
    n = len(tree_list)
    root_list = [1] * (n + 1)
    for i in range(n):
        root_list[tree_list[i][0]] = 0
        root_list[tree_list[i][1]] = 0
    return root_list.index(1)


def leaf_num(tree_list):
    sum = 0
    for link in tree_list:
        if link == [-1, -1]:
            sum += 1
    return sum

n = int(input())
tree_list = []
for i in range(n):
    tree_list.append(list(map(int, input().split())))
print(depth_tree(root(tree_list), tree_list) - 1, leaf_num(tree_list))
```



代码运行截图

<img width="953" alt="截屏2024-03-25 16 41 14" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/567597b3-16ee-4b84-94ac-2d0c25c30a28">




### 24729: 括号嵌套树

http://cs101.openjudge.cn/practice/24729/



思路：正向删括号，反向先将括号前的字母移到括号后再删括号



代码

```python
def forward(exp):
    forward = ""
    for i in exp:
        if i.isupper():
            forward += i
    return forward


def backward(exp):
    stack = []
    for i in range(len(exp)):
        if exp[i] == "(":
            stack.append(i)
        elif exp[i] == ")":
            j = stack.pop()
            exp = exp[: j - 1] + exp[j : i + 1] + exp[j - 1] + exp[i + 1 :]
    return forward(exp)


exp = input()
print(forward(exp))
print(backward(exp)) 

```



代码运行截图

<img width="954" alt="截屏2024-03-26 15 08 02" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/6458edd6-2af5-4381-ba8b-578a3d0cbad6">




### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/



思路：栈



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



代码运行截图

<img width="797" alt="截屏2024-03-26 17 33 59" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/ce63031d-e23c-4ffe-83f5-ab8153708eab">




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





