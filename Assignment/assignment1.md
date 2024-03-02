# Assignment #1: 拉齐大家Python水平

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/

思路：逐一递推

##### 代码

```python
def num(n):
    list = []
    list.append(0)
    list.append(1)
    list.append(1)
    for i in range(n):
        list.append(list[i+2] + list[i+1] + list[i])
    print(list[n])

n = int(input())
num(n)
```




代码运行截图

<img width="955" alt="20742" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/25a73be6-d542-4b91-9c83-d63ee28261b5">




### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A


思路：逐一判断


##### 代码

```python
def doesVasyaSayHello(s):
    a = 0
    for i in range(len(s)):
        list = ['h','e','l','l','o']
        if s[i] == list[a]:
            a += 1
        if a == 5:
            break
    if a == 5:
        print('YES')
    else:
        print('NO')

s = input()
doesVasyaSayHello(s)
```



代码运行截图

<img width="1183" alt="58A" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/380e2cbf-ff14-43da-a697-34694cd9937e">




### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A


思路：逐一对每个字符进行3个操作


##### 代码

```python
def deleteVowels(s):
    list = ['A','O','Y','E','U','I','a','o','y','e','u','i']
    s1 = ''
    for i in range(len(s)):
        a = 0
        for j in range(12):
            if s[i] == list[j]:
                a = 1
                break
        if a == 0:
            s1 += '.'
            s1 += s[i].lower()
    print(s1)

s = input()
deleteVowels(s)
```



代码运行截图

<img width="1183" alt="118A" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/f33c84f1-c58c-4e9d-84f0-9a05058b4516">




### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/


思路：先定义判断素数的函数，然后遍历判断对应两个数是否均为素数



##### 代码

```python
def is_Prime(n):
    if n <= 1:
        return 0
    elif n <= 3:
        return 1
    elif n % 2 == 0 or n % 3 == 0:
        return 0
    i = 5
    while i*i <= n:
        if n % i == 0 or n % (i+2) == 0:
            return 0
        i += 6
    return 1

def sepPrime(m):
    for i in range(int(m/2)+1):
        if is_Prime(i)*is_Prime(m-i) == 1:
            print(i,m-i)
            break

m = int(input())
sepPrime(m)
```



代码运行截图

<img width="957" alt="22359" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/edda7b48-5271-4069-8f51-7c547d52cde6">




### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/



思路：遍历找到最大指数幂



##### 代码

```python
def timeComplexity(s):
    list = s.split('+')
    a = 0
    for i in range(len(list)):
        splitList = list[i].split('n^')
        if int(splitList[1]) > a and splitList[0] != '0':
            a = int(splitList[1])
    a = 'n^' + str(a)
    print(a)

s = input()
timeComplexity(s)
```



代码运行截图

<img width="954" alt="23563" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/eaa1b23c-a2e3-4f4e-8e24-d7d3c5b65a44">




### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/



思路：先排序，然后统计票数，找到最大票数的选项，对其进行排序后输出



##### 代码

```python
def topSelection(s):
    s.sort()
    list = []
    expList = []
    list.append([s[0],1])
    for i in range(len(s)-1):
        if s[i+1] != s[i]:
            list.insert(0,[s[i+1],1])
        else:
            list[0][1] += 1
    a = 1
    for i in range(len(list)):
        if list[i][1] >= a:
            a = list[i][1]
    for i in range(len(list)):
        if list[i][1] == a:
            expList.append(int(list[i][0]))
    expList.sort()
    for i in range(len(expList)-1):
        print(expList[i],end=' ')
    print(expList[len(expList)-1])

s = input().split(' ')
topSelection(s)
```



代码运行截图

<img width="962" alt="24684" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/65aa8183-8d30-4952-ace9-a287b79fdb84">




## 2. 学习总结和收获

计算概论选择C语言，自学python，作业中复习了字符串、列表、字典等数据类型的功能。

练习了OJ“2024spring每日选做“



