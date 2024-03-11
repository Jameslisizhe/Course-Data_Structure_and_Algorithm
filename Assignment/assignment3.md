# Assignment #3: March月考

2024 spring, Complied by 李思哲 物理学院


**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/



思路：



##### 代码

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==





**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147



思路：



##### 代码

```python
# 

```



代码运行截图

<img width="963" alt="截屏2024-03-11 16 53 06" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/f7618a67-8352-4849-b12d-89607123bafe">




**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253



思路：



##### 代码

```python
def answer_Joseph_problem(n, p, m):
    kid_queue = []
    for i in range(1, n + 1):
        kid_queue.append(i)
    pos_of_1 = p - 1
    quit_list = []
    while len(kid_queue) != 0:
        if pos_of_1 + m - 1 < len(kid_queue):
            quit_list.append(kid_queue[pos_of_1 + m - 1])
            del kid_queue[pos_of_1 + m - 1]
            pos_of_1 += m - 1
        else:
            pos_of_1 -= len(kid_queue)
    return quit_list

while True:
    n, p, m = map(int, input().split())
    if n != 0 or p != 0 or m != 0:
        print(*answer_Joseph_problem(n, p, m), sep = ',')
    else:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554



思路：



##### 代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





**19963:买学区房**

http://cs101.openjudge.cn/practice/19963



思路：



##### 代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：



##### 代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==




