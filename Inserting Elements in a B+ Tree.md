# Ex. No: 16D - Inserting Elements in a B+ Tree in Python

## AIM:
To write a Python function `def insert(self, key, value):` to insert elements into a **B+ Tree**.

---

## ALGORITHM:

**Step 1**: Start the program.

**Step 2**: Define a `BPlusTreeNode` class to represent each node in the B+ Tree:
- Store keys and corresponding values.
- Maintain child pointers.
- Track if the node is a leaf.

**Step 3**: Define a `BPlusTree` class to manage the overall structure:
- Implement methods to insert new keys and values.
- Handle node splitting when the node exceeds the allowed degree.

**Step 4**: Implement `insert(self, key, value)`:
- Locate the correct leaf node for insertion.
- Insert key-value pair.
- If the node overflows, split the node and propagate the split up if necessary.

**Step 5**: Implement methods to handle:
- Finding the appropriate node for insertion.
- Splitting full nodes.
- Linking leaf nodes for fast range queries.

**Step 6**: Print the B+ Tree level-wise after insertion.

---

## PYTHON PROGRAM

```
#Reg.NO-212223060119
#Name-Kavindra T G
ENTER YOUR CODE
class BPlusTreeNode:
    def __init__(self, is_leaf=False):
        self.is_leaf = is_leaf
        self.keys = []
        self.children = []
        self.parent = None
        self.next = None  
        self.values = [] if is_leaf else None

class BPlusTree:
    def __init__(self, degree):
        self.root = BPlusTreeNode(is_leaf=True)
        self.degree = degree

    def find_leaf(self, key):
        node = self.root
        while not node.is_leaf:
            i = 0
            while i < len(node.keys) and key >= node.keys[i]:
                i += 1
            node = node.children[i]
        return node

    def insert(self, key, value):
        leaf = self.find_leaf(key)
        i = 0
        while i < len(leaf.keys) and key > leaf.keys[i]:
            i += 1
        leaf.keys.insert(i, key)
        leaf.values.insert(i, value)
        if len(leaf.keys) >= self.degree:
            self.split_leaf(leaf)

    def split_leaf(self, leaf):
        new_leaf = BPlusTreeNode(is_leaf=True)
        mid = len(leaf.keys) // 2
        new_leaf.keys = leaf.keys[mid:]
        new_leaf.values = leaf.values[mid:]
        leaf.keys = leaf.keys[:mid]
        leaf.values = leaf.values[:mid]

        new_leaf.next = leaf.next
        leaf.next = new_leaf
        new_leaf.parent = leaf.parent

        if leaf.parent is None:
            new_root = BPlusTreeNode(is_leaf=False)
            new_root.keys = [new_leaf.keys[0]]
            new_root.children = [leaf, new_leaf]
            leaf.parent = new_root
            new_leaf.parent = new_root
            self.root = new_root
        else:
            self.insert_into_parent(leaf, new_leaf.keys[0], new_leaf)

    def insert_into_parent(self, left, key, right):
        parent = left.parent
        insert_pos = parent.children.index(left)
        parent.keys.insert(insert_pos, key)
        parent.children.insert(insert_pos + 1, right)
        right.parent = parent

        if len(parent.keys) >= self.degree:
            self.split_internal(parent)

    def split_internal(self, node):
        new_internal = BPlusTreeNode(is_leaf=False)
        mid = len(node.keys) // 2
        promote_key = node.keys[mid]

        new_internal.keys = node.keys[mid + 1:]
        new_internal.children = node.children[mid + 1:]
        for child in new_internal.children:
            child.parent = new_internal

        node.keys = node.keys[:mid]
        node.children = node.children[:mid + 1]

        if node.parent is None:
            new_root = BPlusTreeNode(is_leaf=False)
            new_root.keys = [promote_key]
            new_root.children = [node, new_internal]
            node.parent = new_root
            new_internal.parent = new_root
            self.root = new_root
        else:
            self.insert_into_parent(node, promote_key, new_internal)

    def print_leaves(self):
        node = self.root
        while not node.is_leaf:
            node = node.children[0]
        print("Leaf level:")
        while node:
            for key, val in zip(node.keys, node.values):
                print(f"{key}:{val}", end=" | ")
            node = node.next
        print("\n")


bpt = BPlusTree(degree=4)

bpt.insert(10, "A")
bpt.insert(20, "B")
bpt.insert(5, "C")
bpt.insert(6, "D")
bpt.insert(12, "E")
bpt.insert(30, "F")
bpt.insert(7, "G")
bpt.insert(17, "H")

bpt.print_leaves()

```

## OUTPUT

![image](https://github.com/user-attachments/assets/846a7f8f-47cd-4a4b-8853-4506276e0837)


## RESULT
Thus,the python function `def insert(self, key, value):` to insert elements into a **B+ Tree** has been executed and verified successfully.
