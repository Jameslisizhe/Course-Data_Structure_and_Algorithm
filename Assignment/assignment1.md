# Assignment #1: 拉齐大家Python水平


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


##### 代码

```python
def doesVasyaSayHello(s):
    hello = "hello"
    index = 0
    for char in s:
        if char == hello[index]:
            index += 1
            if index == 5:
                return "YES"
    return "NO"


s = input()
print(doesVasyaSayHello(s))

```



### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A


##### 代码

```python
def deleteVowels(s):
    newstr = ""
    for char in s:
        if char not in "AaOoYyEeUuIi":
            newstr += "." + char.lower()
    return newstr


s = input()
print(deleteVowels(s))

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



思路：利用collections中Counter进行统计



##### 代码

```python
from collections import Counter


def find_winner(votes):
    winner_count = Counter(votes).most_common()
    max_votes = winner_count[0][1]
    winners = [option for option, count in winner_count if count == max_votes]
    return sorted(winners)


votes = list(map(int, input().split()))
print(*find_winner(votes))

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


collections.Counter

```python
from collections import Counter

counter = Counter(list)
counter.most_common(n) # find the most common n value

```

re
```python

```

