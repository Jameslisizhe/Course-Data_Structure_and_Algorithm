# Assignment #4: 排序、栈、队列和树


## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



代码

```python
from collections import deque

def deque_operation(queue, op, value):
    if op == 1:
        queue.append(value)
    elif op == 2:
        if value == 0:
            queue.popleft()
        elif value == 1:
            queue.pop()


t = int(input())
for _ in range(t):
    queue = deque()
    n = int(input())
    for _ in range(n):
        op, value = map(int, input().split())
        deque_operation(queue, op, value)
    if queue:
        print(*queue)
    else:
        print("NULL")

```



### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/


代码

```python
def Poland_exp(exp):
    stack = []
    for token in exp.split():
        stack.append(token)
        while len(stack) > 1 and stack[-2] not in {'+', "-", "*", '/'} and stack[-1] not in {'+', "-", "*", '/'}:
                right_operand = float(stack.pop())
                left_operand = float(stack.pop())
                operator = stack.pop()
                if operator == '+':
                    stack.append(left_operand + right_operand)
                elif operator == '-':
                    stack.append(left_operand - right_operand)
                elif operator == '*':
                    stack.append(left_operand * right_operand)
                elif operator == '/':
                    stack.append(left_operand / right_operand)
    return stack[0]

s = input()
print("%f" % Poland_exp(s))

```




### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/



思路：先对括号内处理并缩合，最后对一个没有括号的列表处理



代码

```python
def exp_split(exp):
    exp_list = []
    i = 0
    while i < len(exp):
        if (
            exp[i] == "+"
            or exp[i] == "-"
            or exp[i] == "*"
            or exp[i] == "/"
            or exp[i] == "("
            or exp[i] == ")"
        ):
            if exp[:i] != '':
                exp_list.append(exp[:i])
            exp_list.append(exp[i])
            exp = exp[i + 1 :]
            i = 0
        else:
            i += 1
    if exp != '':
        exp_list.append(exp)
    return exp_list


def normal_trans(exp_list):
    i = 0
    while i < len(exp_list):
        if exp_list[i] == "*":
            exp_list[i] = exp_list[i - 1] + " " + exp_list[i + 1] + " " + "*"
            del exp_list[i - 1], exp_list[i]
        elif exp_list[i] == "/":
            exp_list[i] = exp_list[i - 1] + " " + exp_list[i + 1] + " " + "/"
            del exp_list[i - 1], exp_list[i]
        else:
            i += 1
    i = 0
    while i < len(exp_list):
        if exp_list[i] == "+":
            exp_list[i] = exp_list[i - 1] + " " + exp_list[i + 1] + " " + "+"
            del exp_list[i - 1], exp_list[i]
        elif exp_list[i] == "-":
            exp_list[i] = exp_list[i - 1] + " " + exp_list[i + 1] + " " + "-"
            del exp_list[i - 1], exp_list[i]
        else:
            i += 1
    return exp_list


def trans(exp):
    exp_list = exp_split(exp)
    stack = []
    i = 0
    while i < len(exp_list):
        if exp_list[i] == "(":
            stack.append(i)
            i += 1
        elif exp_list[i] == ")":
            exp_list = (
                exp_list[: stack[-1]]
                + normal_trans(exp_list[stack[-1] + 1 : i])
                + exp_list[i + 1 :]
            )
            i = stack[-1] + 1
            stack.pop()
        else:
            i += 1
    return normal_trans(exp_list)[0]


n = int(input())
for _ in range(n):
    exp = input()
    print(trans(exp))

```




### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/



思路：下一个出栈必须是上一个出栈的元素前一个或者后边的元素



代码

```python
def is_valid_pop_seq(x, s):
    if len(s) != len(x):
        return False
    else:
        pos = 1
        for i in range(len(s)):
            if s[i] in x:
                if x.find(s[i]) < pos - 1:
                    return False
                else:
                    pos = x.find(s[i])
                    x = x[:pos] + x[pos + 1 :]
            else:
                return False
        return True


x = input()
while True:
    try:
        s = input()
        if is_valid_pop_seq(x, s):
            print("YES")
        else:
            print("NO")
    except EOFError:
        break

```




### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



代码

```python
class TreeNode:
    def __init__(self):
        self.left = None
        self.right = None


def tree_depth(node):
    if node is None:
        return 0
    return max(tree_depth(node.left), tree_depth(node.right)) + 1


n = int(input())
nodes = [TreeNode() for _ in range(n)]
for i in range(n):
    left_index, right_index = map(int, input().split())
    if left_index != -1:
        nodes[i].left = nodes[left_index - 1]
    if right_index != -1:
        nodes[i].right = nodes[right_index - 1]
print(tree_depth(nodes[0]))

```



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




## 2. 学习总结和收获

基于链表的双端队列可以如下定义
```python
class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None
        self.prev = None

class Deque:
    def __init__(self):
        self.front = None
        self.rear = None

    def is_empty(self):
        return self.front is None

    def add_front(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.front = new_node
            self.rear = new_node
        else:
            new_node.next = self.front
            self.front.prev = new_node
            self.front = new_node

    def add_rear(self, data):
        new_node = Node(data)
        if self.is_empty():
            self.front = new_node
            self.rear = new_node
        else:
            new_node.prev = self.rear
            self.rear.next = new_node
            self.rear = new_node

    def remove_front(self):
        if self.is_empty():
            raise IndexError("Deque is empty")
        removed_data = self.front.data
        if self.front == self.rear:
            self.front = None
            self.rear = None
        else:
            self.front = self.front.next
            self.front.prev = None
        return removed_data

    def remove_rear(self):
        if self.is_empty():
            raise IndexError("Deque is empty")
        removed_data = self.rear.data
        if self.front == self.rear:
            self.front = None
            self.rear = None
        else:
            self.rear = self.rear.prev
            self.rear.next = None
        return removed_data

    def peek_front(self):
        if self.is_empty():
            raise IndexError("Deque is empty")
        return self.front.data

    def peek_rear(self):
        if self.is_empty():
            raise IndexError("Deque is empty")
        return self.rear.data

    def size(self):
        current = self.front
        count = 0
        while current:
            count += 1
            current = current.next
        return count

```




