# Ex. No: 16C - Inserting Nodes in a B-Tree in Python

## AIM:
To write a Python function `def insert(self, k):` to insert the nodes in a **B-Tree**.

---

## ALGORITHM:

**Step 1**: Start the program.

**Step 2**: Define the `BTreeNode` class to represent a node:
- Contains a list of keys.
- Contains a list of children.
- Indicates whether it is a leaf.

**Step 3**: Define the `BTree` class with:
- Methods for inserting keys.
- Handling node splitting.
- Tree traversal and printing.

**Step 4**: Implement `insert()`:
- Insert a key into the tree.
- Handle full root case and invoke node splitting if needed.

**Step 5**: Implement `insert_non_full()` to insert a key into a node that is not full.

**Step 6**: Implement `split_child()` to split a full child during insertion.

**Step 7**: Define `print_tree()` to recursively print the structure of the B-Tree.

---

## PYTHON PROGRAM

```
#Reg.NO-212223060119
#Name-Kavindra T G
ENTER YOUR CODE

class BTreeNode:
    def __init__(self, t, is_leaf):
        self.t = t
        self.keys = []
        self.children = []
        self.is_leaf = is_leaf

class BTree:
    def __init__(self, t):
        self.root = BTreeNode(t, True)
        self.t = t

    def insert(self, k):
        root = self.root
        if len(root.keys) == (2 * self.t) - 1:
            new_node = BTreeNode(self.t, False)
            new_node.children.insert(0, root)
            self.split_child(new_node, 0)
            self.insert_non_full(new_node, k)
            self.root = new_node
        else:
            self.insert_non_full(root, k)

    def insert_non_full(self, node, k):
        i = len(node.keys) - 1
        if node.is_leaf:
            node.keys.append(None)
            while i >= 0 and k < node.keys[i]:
                node.keys[i + 1] = node.keys[i]
                i -= 1
            node.keys[i + 1] = k
        else:
            while i >= 0 and k < node.keys[i]:
                i -= 1
            i += 1
            if len(node.children[i].keys) == (2 * self.t) - 1:
                self.split_child(node, i)
                if k > node.keys[i]:
                    i += 1
            self.insert_non_full(node.children[i], k)

    def split_child(self, parent, i):
        t = self.t
        y = parent.children[i]
        z = BTreeNode(t, y.is_leaf)
        parent.children.insert(i + 1, z)
        parent.keys.insert(i, y.keys[t - 1])
        z.keys = y.keys[t:(2 * t) - 1]
        y.keys = y.keys[0:t - 1]
        if not y.is_leaf:
            z.children = y.children[t:(2 * t)]
            y.children = y.children[0:t]

    def print_tree(self, node=None, level=0):
        if node is None:
            node = self.root
        print("Level", level, "Keys:", node.keys)
        if not node.is_leaf:
            for child in node.children:
                self.print_tree(child, level + 1)
b_tree = BTree(t=3)
for key in [10, 20, 5, 6, 12, 30, 7, 17]:
    b_tree.insert(key)
b_tree.print_tree()

```

## OUTPUT
![image](https://github.com/user-attachments/assets/6112635d-c263-4d7d-9bc6-30223c5f7ff9)


## RESULT
Thus, the python function `def insert(self, k):` to insert the nodes in a **B-Tree** has been executed and verified successfully.
