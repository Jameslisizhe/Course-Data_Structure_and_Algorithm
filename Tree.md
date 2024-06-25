# Tree

## 定义与概念
二叉树深度定义：从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的节点个数为树的深度

## 算法

### 解析树

我们也可以将 ( ( 7 + 3) * ( 5 - 2 ) ) 这样的数学表达式表示成解析树
<img width="709" alt="202401311918463" src="https://github.com/Jameslisizhe/Course-Data_Structure_and_Algorithm/assets/161715584/23ecc27d-32d8-434c-a0c5-26f3af573559">

### 树的遍历

二叉树的前中后序序列

```python
def preorder(node):
    if not node:
        return ""
    return node.value + preorder(node.left) + preorder(node.right)


def inorder(node):
    if not node:
        return ""
    return inorder(node.left) + node.value + inorder(node.right)


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


###
