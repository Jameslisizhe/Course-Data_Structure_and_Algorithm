# Assignment #5: "树"算：概念、表示、解析、遍历


## 1. 题目

### 27638: 求二叉树的高度和叶子数目

http://cs101.openjudge.cn/practice/27638/



代码

```python
class TreeNode:
    def __init__(self):
        self.parent = None
        self.left = None
        self.right = None


def tree_height(node):
    if node is None:
        return -1
    return max(tree_height(node.left), tree_height(node.right)) + 1


def root(node):
    if node.parent is None:
        return node
    return root(node.parent)


def count_leaves(node):
    if node is None:
        return 0
    elif node.left is None and node.right is None:
        return 1
    return count_leaves(node.left)+count_leaves(node.right)


n = int(input())
nodes = [TreeNode() for _ in range(n)]
for i in range(n):
    left_index, right_index = map(int, input().split())
    if left_index != -1:
        nodes[i].left = nodes[left_index]
        nodes[left_index].parent = nodes[i]
    if right_index != -1:
        nodes[i].right = nodes[right_index]
        nodes[right_index].parent = nodes[i]
print(tree_height(root(nodes[0])),count_leaves(root(nodes[0])))

```




### 24729: 括号嵌套树

http://cs101.openjudge.cn/practice/24729/



代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.children = []


def preorder(node):
    if node.children == []:
        return node.value
    return node.value + "".join(map(preorder, node.children))


def postorder(node):
    if node.children == []:
        return node.value
    return "".join(map(postorder, node.children)) + node.value


exp = input()
node = root = TreeNode(exp[0])
stack = [root]
for char in exp[1:]:
    if char.isalpha():
        node = TreeNode(char)
        stack[-1].children.append(node)
    elif char == "(":
        stack.append(node)
    elif char == ")":
        stack.pop()
print(preorder(root))
print(postorder(root))

```



### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/


代码

```python
from sys import exit


class Dir:
    def __init__(self, name):
        self.name = name
        self.dir = []
        self.file = []


def construct():
    stack = [Dir("ROOT")]
    while (file_dir := input()) not in {"*", "#"}:
        if file_dir[0] == "d":
            dir = Dir(file_dir)
            stack[-1].dir.append(dir)
            stack.append(dir)
        elif file_dir[0] == "f":
            stack[-1].file.append(file_dir)
        elif file_dir == "]":
            stack.pop()
    if file_dir == "*":
        return stack[0]
    else:
        exit(0)


def graph_print(root, depth):
    print("|     " * depth + root.name)
    for dir in root.dir:
        graph_print(dir, depth + 1)
    for file in sorted(root.file):
        print("|     " * depth + file)

set_num = 0
while True:
    set_num += 1
    root = construct()
    print("DATA SET %d:" % set_num)
    graph_print(root, 0)
    print()

```




### 25140: 根据后序表达式建立队列表达式

http://cs101.openjudge.cn/practice/25140/



思路：建立起表达式树，按层次遍历表达式树的结果前后颠倒就得到队列表达式


代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def parse_tree(postfix):
    stack = []
    for char in postfix:
        node = TreeNode(char)
        if char.isupper():
            node.right = stack.pop()
            node.left = stack.pop()
        stack.append(node)
    return stack[0]


def level_order_traversal(root):
    queue = [root]
    traversal = []
    while queue:
        node = queue.pop(0)
        traversal.append(node.value)
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    return traversal


n = int(input())
for i in range(n):
    print("".join(reversed(level_order_traversal(parse_tree(input())))))

```




### 24750: 根据二叉树中后序序列建树

http://cs101.openjudge.cn/practice/24750/


代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def build_tree(inorder, postorder):
    if not inorder:
        return None
    root = TreeNode(postorder[-1])
    index = inorder.index(postorder[-1])
    root.left = build_tree(inorder[:index], postorder[:index])
    root.right = build_tree(inorder[index + 1 :], postorder[index:-1])
    return root


def preorder(node):
    if not node:
        return ""
    return node.value + preorder(node.left) + preorder(node.right)


inorder = input()
postorder = input()
print(preorder(build_tree(inorder, postorder)))

```





### 22158: 根据二叉树前中序序列建树

http://cs101.openjudge.cn/practice/22158/


代码

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


def build_tree(preorder, inorder, root):
    if preorder == inorder and len(preorder) == 1:
        return
    root_index = inorder.index(preorder[0])
    left_preorder = preorder[1 : root_index + 1]
    left_inorder = inorder[:root_index]
    right_preorder = preorder[root_index + 1 :]
    right_inorder = inorder[root_index + 1 :]
    if left_preorder:
        root.left = TreeNode(left_preorder[0])
        build_tree(left_preorder, left_inorder, root.left)
    if right_inorder:
        root.right = TreeNode(right_preorder[0])
        build_tree(right_preorder, right_inorder, root.right)


def postorder(node):
    if not node:
        return ""
    return postorder(node.left) + postorder(node.right) + node.value


while True:
    try:
        preorder = input()
        inorder = input()
        root = TreeNode(preorder[0])
        build_tree(preorder, inorder, root)
        print(postorder(root))
    except EOFError:
        break

```





## 2. 学习总结和收获

二叉树的前中后序序列

```python
def preorder(node):
    if not node:
        return ""
    return node.value + preorder(node.left) + preorder(node.right)


def inorder(node):
    if not node:
        return ""
    return preorder(node.left) + node.value + preorder(node.right)


def postorder(node):
    if not node:
        return ""
    return postorder(node.left) + postorder(node.right) + node.value

```

多叉树的前后序序列

```python
def preorder(node):
    if node.children == []:
        return node.value
    return node.value + "".join(map(preorder, node.children))


def postorder(node):
    if node.children == []:
        return node.value
    return "".join(map(postorder, node.children)) + node.value

```


