# Assignment #B: 图论和树算

2024 spring, Complied by 李思哲 物理学院




**编程环境**

操作系统：macOS Monota 14.1.1

Python编程环境：Visual Studio Code 1.86.2 (Universal)


## 1. 题目

### 28170: 算鹰

dfs, http://cs101.openjudge.cn/practice/28170/



思路：



代码

```python
def dfs(x,y):
    graph[x][y] = "-"
    for dx,dy in [(1,0),(-1,0),(0,1),(0,-1)]:
        if 0<=x+dx<10 and 0<=y+dy<10 and graph[x+dx][y+dy] == ".":
            dfs(x+dx,y+dy)
graph = []
result = 0
for i in range(10):
    graph.append(list(input()))
for i in range(10):
    for j in range(10):
        if graph[i][j] == ".":
            result += 1
            dfs(i,j)
print(result)

```



代码运行截图 ==（至少包含有"Accepted"）==

<img width="955" alt="截屏2024-05-07 23 25 36" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/22d38cd5-5612-4fa3-88a6-3ec8d3068b81">




### 02754: 八皇后

dfs, http://cs101.openjudge.cn/practice/02754/



思路：



代码

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==





### 03151: Pots

bfs, http://cs101.openjudge.cn/practice/03151/



思路：



代码

```python
def bfs(A, B, C):
    start = (0, 0)
    visited = set()
    visited.add(start)
    queue = [(start, [])]

    while queue:
        (a, b), actions = queue.pop(0)

        if a == C or b == C:
            return actions

        next_states = [(A, b), (a, B), (0, b), (a, 0), (min(a + b, A),\
                max(0, a + b - A)), (max(0, a + b - B), min(a + b, B))]

        for i in next_states:
            if i not in visited:
                visited.add(i)
                new_actions = actions + [get_action(a, b, i)]
                queue.append((i, new_actions))

    return ["impossible"]


def get_action(a, b, next_state):
    if next_state == (A, b):
        return "FILL(1)"
    elif next_state == (a, B):
        return "FILL(2)"
    elif next_state == (0, b):
        return "DROP(1)"
    elif next_state == (a, 0):
        return "DROP(2)"
    elif next_state == (min(a + b, A), max(0, a + b - A)):
        return "POUR(2,1)"
    else:
        return "POUR(1,2)"


A, B, C = map(int, input().split())
solution = bfs(A, B, C)

if solution == ["impossible"]:
    print(solution[0])
else:
    print(len(solution))
    for i in solution:
        print(i)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==


<img width="1009" alt="123" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/349d6179-6501-40a4-aa31-32f59e06c6f4">




### 05907: 二叉树的操作

http://cs101.openjudge.cn/practice/05907/



思路：



代码

```python
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None

class BinaryTree:
    def __init__(self, n):
        self.root = TreeNode(0)
        self.node_dict = {0: self.root}
        self.build_tree(n)

    def build_tree(self, n):
        for _ in range(n):
            idx, left, right = map(int, input().split())
            if idx not in self.node_dict:
                self.node_dict[idx] = TreeNode(idx)
            node = self.node_dict[idx]
            if left != -1:
                if left not in self.node_dict:
                    self.node_dict[left] = TreeNode(left)
                left_node = self.node_dict[left]
                node.left = left_node
                left_node.parent = node
            if right != -1:
                if right not in self.node_dict:
                    self.node_dict[right] = TreeNode(right)
                right_node = self.node_dict[right]
                node.right = right_node
                right_node.parent = node

    def swap_nodes(self, x, y):
        node_x = self.node_dict[x]
        node_y = self.node_dict[y]
        px, py = node_x.parent, node_y.parent

        if px == py:
            px.left, px.right = px.right, px.left
            return

        # Swap in the parent's children references
        if px.left == node_x:
            px.left = node_y
        else:
            px.right = node_y

        if py.left == node_y:
            py.left = node_x
        else:
            py.right = node_x

        # Swap their parent references
        node_x.parent, node_y.parent = py, px

    def find_leftmost_child(self, x):
        node = self.node_dict[x]
        while node.left:
            node = node.left
        return node.val

def main():
    t = int(input())
    for _ in range(t):
        n, m = map(int, input().split())
        tree = BinaryTree(n)
        for _ in range(m):
            op, *args = map(int, input().split())
            if op == 1:
                x, y = args
                tree.swap_nodes(x, y)
            elif op == 2:
                x, = args
                print(tree.find_leftmost_child(x))

if __name__ == "__main__":
    main()

```




代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="965" alt="截屏2024-05-07 23 28 16" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/ac670f96-a75c-4892-ae43-f58e2ab1bc2b">






### 18250: 冰阔落 I

Disjoint set, http://cs101.openjudge.cn/practice/18250/



思路：



代码

```python
def find(x):
    if parent[x] != x:
        parent[x] = find(parent[x])
    return parent[x]

def union(x, y):
    root_x = find(x)
    root_y = find(y)
    if root_x != root_y:
        parent[root_y] = root_x

while True:
    try:
        n, m = map(int, input().split())
        parent = list(range(n + 1))

        for _ in range(m):
            a, b = map(int, input().split())
            if find(a) == find(b):
                print('Yes')
            else:
                print('No')
                union(a, b)

        unique_parents = set(find(x) for x in range(1, n + 1))  # 获取不同集合的根节点
        ans = sorted(unique_parents)  # 输出有冰阔落的杯子编号
        print(len(ans))
        print(*ans)

    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

<img width="949" alt="截屏2024-05-07 23 29 29" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/0b2c4ff5-db72-4870-adea-6b3e13716e34">




### 05443: 兔子与樱花

http://cs101.openjudge.cn/practice/05443/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

近日任务较多，仅完成四题，周末补上月考以及之前未完成的题目



