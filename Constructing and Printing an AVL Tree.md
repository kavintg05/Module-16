# Ex. No: 16A - Constructing and Printing an AVL Tree in Python

## AIM:
To write a Python program to construct an **AVL tree** and print the nodes of it using the appropriate packages and built-in function.

---

## ALGORITHM:

**Step 1**: Start the program.

**Step 2**: Define a function `getDictTree(tree)` to return the **dict_tree** of an AVL tree.

**Step 3**: Define a function `Construct_AVL(L)` to:
- Create an **AVL tree** from the list `L`.
- Get and print the **dict_tree** using `getDictTree(tree)`.

**Step 4**: Define a list `L` with integer values.

**Step 5**: Call `Construct_AVL(L)` to build the tree and print the result.

**Step 6**: End the program.

---

## PYTHON PROGRAM
```
#Reg.NO-212223060119
#Name-Kavindra T G
ENTER YOUR CODE HERE

class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None
        self.height = 1

def getHeight(node):
    if not node:
        return 0
    return node.height

def getBalance(node):
    if not node:
        return 0
    return getHeight(node.left) - getHeight(node.right)

def rightRotate(z):
    y = z.left
    T3 = y.right
    y.right = z
    z.left = T3
    z.height = 1 + max(getHeight(z.left), getHeight(z.right))
    y.height = 1 + max(getHeight(y.left), getHeight(y.right))
    return y

def leftRotate(z):
    y = z.right
    T2 = y.left
    y.left = z
    z.right = T2
    z.height = 1 + max(getHeight(z.left), getHeight(z.right))
    y.height = 1 + max(getHeight(y.left), getHeight(y.right))
    return y

def insert(node, key):
    if not node:
        return Node(key)
    elif key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    node.height = 1 + max(getHeight(node.left), getHeight(node.right))
    balance = getBalance(node)

    if balance > 1 and key < node.left.key:
        return rightRotate(node)
    if balance < -1 and key > node.right.key:
        return leftRotate(node)
    if balance > 1 and key > node.left.key:
        node.left = leftRotate(node.left)
        return rightRotate(node)
    if balance < -1 and key < node.right.key:
        node.right = rightRotate(node.right)
        return leftRotate(node)

    return node

def getDictTree(node):
    if not node:
        return None
    return {
        "key": node.key,
        "left": getDictTree(node.left),
        "right": getDictTree(node.right)
    }

def Construct_AVL(L):
    root = None
    for key in L:
        root = insert(root, key)
    tree_dict = getDictTree(root)
    print("AVL Tree (dict format):")
    print(tree_dict)

L = [20, 4, 15, 70, 50, 100, 80]
Construct_AVL(L)

```

## OUTPUT
![image](https://github.com/user-attachments/assets/afa5d17a-e14c-4b41-9d51-32088a57be09)


## RESULT
Thus, the python program to construct an **AVL tree** and print the nodes of it using the appropriate packages and built-in function has been executed and verified successfully.
