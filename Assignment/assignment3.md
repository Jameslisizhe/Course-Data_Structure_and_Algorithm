# Assignment #3: March月考

2024 spring, Complied by 李思哲 物理学院


**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 02945: 拦截导弹

http://cs101.openjudge.cn/practice/02945/



思路：



##### 代码

```python
def missile_interception(k):
    missile_hight = list(map(int, input().split()))
    longest_sub = [1] * k
    for i in range(k):
        for j in range(i):
            if missile_hight[j] >= missile_hight[i]:
                longest_sub[i] = max(longest_sub[i], longest_sub[j] + 1)
    return max(longest_sub)


k = int(input())
print(missile_interception(k))

```



代码运行截图

<img width="965" alt="截屏2024-03-11 19 27 12" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/6c1244a4-109c-4c34-9df8-a2c535a9494c">




### 04147:汉诺塔问题(Tower of Hanoi)

http://cs101.openjudge.cn/practice/04147



思路：



##### 代码

```python
def tower_of_Hanoi(n, a, b, c):
    if n > 3:
        tower_of_Hanoi(n - 1, a, c, b)
        print('%d:%s->%s' % (n, a, c))
        tower_of_Hanoi(n - 1, b, a, c)
    elif n == 3:
        print('%d:%s->%s' % (1, a, c))
        print('%d:%s->%s' % (2, a, b))
        print('%d:%s->%s' % (1, c, b))
        print('%d:%s->%s' % (3, a, c))
        print('%d:%s->%s' % (1, b, a))
        print('%d:%s->%s' % (2, b, c))
        print('%d:%s->%s' % (1, a, c))


n, a, b, c = input().split()
tower_of_Hanoi(int(n), a, b, c)
```



代码运行截图

<img width="950" alt="截屏2024-03-11 17 11 07" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/acd94097-f3ce-4213-83ec-256af417aea9">




### 03253: 约瑟夫问题No.2

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



代码运行截图

<img width="963" alt="截屏2024-03-11 16 53 06" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/f7618a67-8352-4849-b12d-89607123bafe">





### 21554:排队做实验 (greedy)v0.2

http://cs101.openjudge.cn/practice/21554



思路：



##### 代码

```python
def lab_arrangement(time_list: list, n: int):
    for i in range(n):
        time_list[i] = [time_list[i], i + 1]
    time_list.sort()
    total_time = 0
    print_list = []
    for i in range(n):
        print_list.append(time_list[i][1])
        total_time += time_list[i][0] * (n - 1 - i)
    print(*print_list)
    print("%.2f" % (total_time / n))


n = int(input())
time_list = list(map(int, input().split()))
lab_arrangement(time_list, n)

```



代码运行截图

<img width="953" alt="截屏2024-03-11 17 13 51" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/2e0a1fb6-989e-4ccc-ade3-84a8de5d905a">




### 19963:买学区房

http://cs101.openjudge.cn/practice/19963



思路：



##### 代码

```python
def find_favored_house_amount(n: int, house: list):
    amount = 0
    house.sort()
    if n % 2 == 1:
        mid_price = house[int((n - 1) / 2)][0]
    else:
        mid_price = (house[int(n / 2) - 1][0] + house[int(n / 2)][0]) / 2
    for i in range(n):
        if house[i][0] < mid_price:
            house[i].append(True)
            house[i].insert(0, house[i][1] / house[i][0])
        else:
            house[i].append(False)
            house[i].insert(0, house[i][1] / house[i][0])
    house.sort()
    if n % 2 == 1:
        mid_value = house[int((n - 1) / 2)][0]
    else:
        mid_value = (house[int(n / 2) - 1][0] + house[int(n / 2)][0]) / 2
    for i in range(n):
        if house[i][0] > mid_value and house[i][3]:
            amount += 1
    return amount


n = int(input())
distance_xy = list(input().split())
house = []
for i in range(n):
    x, y = map(int, distance_xy[i][1: -1].split(','))
    house.append([x + y])
price = list(map(int, input().split()))
for i in range(n):
    house[i].insert(0, price[i])
print(find_favored_house_amount(n, house))

```



代码运行截图

<img width="961" alt="截屏2024-03-11 20 42 30" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/6ed0b0db-4de5-4d27-9a61-cb4c92b2a023">




### 27300: 模型整理

http://cs101.openjudge.cn/practice/27300



思路：



##### 代码

```python
# 

```



代码运行截图





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==




