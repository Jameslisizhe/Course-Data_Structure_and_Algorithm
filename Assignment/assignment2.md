# Assignment #2: 编程练习

2024 spring, Complied by 李思哲 物理学院



**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)



## 1. 题目

### 27653: Fraction类

http://cs101.openjudge.cn/practice/27653/

##### 代码

```python
import math


class Fraction:

    def __init__(self, num, den):
        self.num = num
        self.den = den

    def __str__(self):
        return str(self.num) + "/" + str(self.den)

    def __add__(self, another_frac):
        newnum = self.num * another_frac.den + self.den * another_frac.num
        newden = self.den * another_frac.den
        gcd = math.gcd(newnum, newden)
        return Fraction(newnum // gcd, newden // gcd)


a, b, c, d = map(int, input().split())
print(Fraction(a, b) + Fraction(c, d))

```



代码运行截图

<img width="946" alt="27653" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/deb23f25-dcf1-4a86-b647-0e89909a95e1">




### 04110: 圣诞老人的礼物-Santa Clau’s Gifts

greedy/dp, http://cs101.openjudge.cn/practice/04110



思路：贪心，先对单位质量价值排序，由大到小添加



##### 代码

```python
def greatestValue(n, w):
    valueList = []
    for i in range(n):
        value, weight = map(int, input().split())
        valueList.append([value/weight, weight, value])
    valueList.sort(reverse = True)
    weightSum = 0
    valueSum = 0
    for i in range(n):
        if weightSum + valueList[i][1] <= w:
            weightSum += valueList[i][1]
            valueSum += valueList[i][2]
        else:
            valueSum += valueList[i][0] * (w - weightSum)
            break
    print('%.1f' % valueSum)

n, w = map(int, input().split())
greatestValue(n, w)
```



代码运行截图

<img width="943" alt="04110" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/af8c53a8-5b8e-4772-bc5b-d058b5e9edb9">




### 18182: 打怪兽

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/



思路：先对技能排序，在同一时刻，先试用伤害大的技能，直到达到使用上限



##### 代码

```python
def monsterStatus(n, m, b):
    skillList = []
    for i in range(n):
        skillList.append(list(map(int, input().split())))
    skillList.sort()
    lostPoint = 0
    for i in range(n - 1):
        if skillList[i][0] != skillList[i + 1][0]:
            usedSkillAmount = 0
            while usedSkillAmount < m and skillList[i-usedSkillAmount][0] == skillList[i][0]:
                lostPoint += skillList[i-usedSkillAmount][1]
                if i-usedSkillAmount == 0:
                    break
                usedSkillAmount += 1
        if lostPoint >= b:
            print(skillList[i][0])
            return
    usedSkillAmount = 0
    while usedSkillAmount < m and skillList[n - 1 - usedSkillAmount][0] == skillList[n - 1][0]:
        lostPoint += skillList[n - 1 - usedSkillAmount][1]
        if n - 1 - usedSkillAmount == 0:
            break
        usedSkillAmount += 1
    if lostPoint >= b:
        print(skillList[n - 1][0])
    else:
        print('alive')
    return

nCase = int(input())
for i in range(nCase):
    n, m, b = map(int, input().split())
    monsterStatus(n, m, b)
```



代码运行截图

<img width="951" alt="18182" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/0f920ea8-b0cb-4ceb-9d21-9ee130ccf4e1">




### 230B. T-primes

binary search/implementation/math/number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：先将所有1000000内的素数找出，判断输入的数可以开方并在开方后是素数即可



##### 代码

```python
import math

sieve = [True] * 1000001
sieve[0] = sieve[1] = False
for i in range(2, 1001):
    if sieve[i]:
        for j in range(i * i, 1000001, i):
            sieve[j] = False

def isTPrime(sieve, n):
    root = round(math.sqrt(n))
    if sieve[root] and root ** 2 == n:
        return True
    return False

n = int(input())
numList = list(map(int, input().split()))
for i in range(n):
    if isTPrime(sieve, numList[i]):
        print('YES')
    else:
        print('NO')
```



代码运行截图

<img width="1184" alt="230B" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/d4376259-3456-4661-b9ed-b5399e9c46fa">




### 1364A. XXXXX

brute force/data structures/number theory/two pointers, 1200, https://codeforces.com/problemset/problem/1364/A



思路：先做数学证明：子列必须贴着原列的两边，然后遍历



##### 代码

```python
def longestSubArray(n, x):
    arrayList = list(map(int, input().split()))
    sum = 0
    for i in arrayList:
        sum += i
    suffixSum = sum
    prefixSum = sum
    if sum % x != 0:
        print(n)
        return
    for i in range(n):
        suffixSum -= arrayList[i]
        prefixSum -= arrayList[n - i - 1]
        if suffixSum % x != 0 or prefixSum % x != 0:
            print(n - i - 1)
            return
    print(-1)

t = int(input())
for i in range(t):
    n, x = map(int, input().split())
    longestSubArray(n, x)
```



代码运行截图

<img width="1182" alt="1364A" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/9e4ea76c-13ee-4f93-a009-a92a9474f164">




### 18176: 2050年成绩计算

http://cs101.openjudge.cn/practice/18176/



思路：先建立素数表，利用230B的方法判断成绩是否为T-Prime，最后平均所有有效成绩



##### 代码

```python
import math

def aveScore(m,n):
    #create square pirme list
    sieve = [True] * 10001
    sieve[0] = sieve[1] = False
    for i in range(2, 101):
        if sieve[i]:
            for j in range(i * i, 10001, i):
                sieve[j] = False
    #calculate average score
    for i in range(m):
        scoreList = input().split()
        scoreSum = 0
        for j in scoreList:
            root = round(math.sqrt(int(j)))
            if sieve[root] and root ** 2 == int(j):
                scoreSum += float(j)
        if scoreSum == 0:
            print(0)
        else:
            print('%.2f' % (scoreSum / len(scoreList)))

m,n = input().split()
aveScore(int(m),int(n))
```



代码运行截图

<img width="957" alt="18176" src="https://github.com/Jameslisizhe/CS-Lesson/assets/161715584/89cbc15d-6c08-44a7-be39-c792b4dc7340">




## 2. 学习总结和收获

在做素数判断时，可以利用Sieve of Eratosthenes来减少时间复杂度

练习了OJ“2024spring每日选做”





