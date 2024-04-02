# Assignment #1: 拉齐大家Python水平

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/


##### 代码

```python
def Tribonacci(n):
    if n == 0:
        return 0
    elif n in {1, 2}:
        return 1
    
    a, b, c = 0, 1, 1
    for _ in range(3, n + 1):
        a, b, c = b, c, a + b + c
    return c

n = int(input())
print(Tribonacci(n))

```




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




### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/

思路：利用Sieve of Eratosthenes将和以内的素数找出，然后一一判断

##### 代码


```python
def generate_primes(n):
    primes = []
    is_prime = [True] * (n + 1)
    is_prime[0] = is_prime[1] = False
    for i in range(2, int(n**0.5) + 1):
        if is_prime[i]:
            primes.append(i)
            for j in range(i * i, n + 1, i):
                is_prime[j] = False
    for i in range(int(n**0.5) + 1, n + 1):
        if is_prime[i]:
            primes.append(i)
    return primes

def find_prime_pair(sum):
    primes = generate_primes(sum)
    for prime in primes:
        if sum - prime in primes:
            return prime, sum - prime

sum = int(input())
A, B = find_prime_pair(sum)
print(A, B)

```




### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/



##### 代码

```python
import re


def time_complecity(s):
    coe_exp = re.findall(r"(\d*)n\^(\d+)", s)
    max_exponent = 0
    for coefficient, exponent in coe_exp:
        if coefficient != "0":
            max_exponent = max(max_exponent, int(exponent))
    return f"n^{max_exponent}"


s = input()
print(time_complecity(s))

```




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




## 2. 学习总结和收获

一个经典的素数判断函数如下

```python
def is_prime(n):
    if n <= 1:
        return False
    elif n <= 3:
        return True
    elif n % 2 == 0 or n % 3 == 0:
        return False
    i = 5
    while i * i <= n:
        if n % i == 0 or n % (i + 2) == 0:
            return False
        i += 6
    return True

```


