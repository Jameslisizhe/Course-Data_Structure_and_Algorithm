# Assignment #9: 图论：遍历，及 树算

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 04081: 树的转换

http://cs101.openjudge.cn/dsapre/04081/



思路：



代码

```python
def tree_heights(s):
    old_height = 0
    max_old = 0
    new_height = 0
    max_new = 0
    stack = []
    for c in s:
        if c == 'd':
            old_height += 1
            max_old = max(max_old, old_height)

            new_height += 1
            stack.append(new_height)
            max_new = max(max_new, new_height)
        else:
            old_height -= 1

            new_height = stack[-1]
            stack.pop()
    return f"{max_old} => {max_new}"

s = input().strip()
print(tree_heights(s))

```



代码运行截图 ==（至少包含有"Accepted"）==





### 08581: 扩展二叉树

http://cs101.openjudge.cn/dsapre/08581/



思路：



代码

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==





### 22067: 快速堆猪

http://cs101.openjudge.cn/practice/22067/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 28046: 词梯

bfs, http://cs101.openjudge.cn/practice/28046/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 28050: 骑士周游

dfs, http://cs101.openjudge.cn/practice/28050/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==





