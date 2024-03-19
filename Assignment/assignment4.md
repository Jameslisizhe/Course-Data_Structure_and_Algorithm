# Assignment #4: 排序、栈、队列和树

Updated 0005 GMT+8 March 11, 2024

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



思路：分类处理即可



代码

```python
def two_tail_array(n):
    array = []
    for i in range(n):
        op, value = map(int, input().split())
        if op == 1:
            array.append(value)
        elif op == 2:
            if value == 0:
                array.pop(0)
            elif value == 1:
                array.pop()
    if len(array) != 0:
        print(*array, sep = ' ')
    else:
        print('NULL')


t = int(input())
for _ in range(t):
    n = int(input())
    two_tail_array(n)

```



代码运行截图

<img width="951" alt="截屏2024-03-18 10 17 41" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/85ff5788-c8c9-45ad-a6fd-6c5b1fd28806">




### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/



思路：



代码

```python
def PolandExp(s):
    value = s.split()
    for i in range(len(value)):
        if value[i] != "+" and value[i] != "-" and value[i] != "*" and value[i] != "/":
            value[i] = float(value[i])
    while len(value) != 1:
        tag = []
        for i in range(1, len(value) - 1):
            if (
                isinstance(value[i], float)
                and isinstance(value[i + 1], float)
                and isinstance(value[i - 1], str)
            ):
                tag.append(i)
                if value[i - 1] == "+":
                    value[i - 1] = value[i] + value[i + 1]
                elif value[i - 1] == "-":
                    value[i - 1] = value[i] - value[i + 1]
                elif value[i - 1] == "*":
                    value[i - 1] = value[i] * value[i + 1]
                elif value[i - 1] == "/":
                    value[i - 1] = value[i] / value[i + 1]
        tag.reverse()
        for i in tag:
            del value[i + 1]
            del value[i]
    print("%f" % value[0])


s = input()
PolandExp(s)


```



代码运行截图

<img width="962" alt="截屏2024-03-11 21 31 26" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/ceedccd8-d3c9-439a-aa5b-f850b8f75f7b">




### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/



思路：



代码

```python
# 

```



代码运行截图





### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/



思路：



代码

```python
def isValid(x):
    s = input()
    if len(s) != len(x):
        print("NO")
    else:
        pos = 1
        for i in range(len(s)):
            if s[i] in x:
                if x.find(s[i]) < pos - 1:
                    print("NO")
                    return
                else:
                    pos = x.find(s[i])
                    x = x[:pos] + x[pos + 1 :]
            else:
                print("NO")
                return
        print("YES")


x = input()
while True:
    try:
        isValid(x)
    except EOFError:
        break


```



代码运行截图

<img width="955" alt="截屏2024-03-11 21 32 55" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/d556a30e-efae-44b7-86f7-50f51defba44">




### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



思路：



代码

```python
def tree_depth(n):
    tree_list = []
    for i in range(n):
        tree_list.append(list(map(int, input().split())))
    depth = [1] * n
    for i in range(n):
        if tree_list[i][0] != -1:
            depth[tree_list[i][0] - 1] = depth[i] + 1
        if tree_list[i][1] != -1:
            depth[tree_list[i][1] - 1] = depth[i] + 1
    return max(depth)


n = int(input())
print(tree_depth(n))
```



代码运行截图

<img width="947" alt="截屏2024-03-18 11 47 05" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/30bc31b6-7f8e-4ff8-848a-edb3291f360a">




### 02299: Ultra-QuickSort

http://cs101.openjudge.cn/practice/02299/



思路：归并排序



代码

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr, 0
    else:
        mid = len(arr) // 2
        left_half, left_count = merge_sort(arr[:mid])
        right_half, right_count = merge_sort(arr[mid:])
        merged_arr, merge_count = merge(left_half, right_half)
        return merged_arr, (left_count + right_count + merge_count)

def merge(left, right):
    result = []
    count = 0
    i = j = 0
    left_len = len(left)
    while i < left_len and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
            count += left_len - i
    result.extend(left[i:])
    result.extend(right[j:])
    return result, count

def count_inversions(arr):
    _, count = merge_sort(arr)
    return count

while True:
    n = int(input())
    arr = []
    if n!= 0:
        for _ in range(n):
            arr.append(int(input()))
        print(count_inversions(arr))
    else:
        break

```



代码运行截图

<img width="950" alt="截屏2024-03-19 13 06 44" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/39eb069c-4885-41da-ae18-698c55171a22">




## 2. 学习总结和收获

题目难度开始上升，需要多加练习




