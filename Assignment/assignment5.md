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



思路：



代码

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==





### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 25140: 根据后序表达式建立队列表达式

http://cs101.openjudge.cn/practice/25140/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





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

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==





