# Ex. No: 16E - Perform Left Rotation in AVL Tree and Insert '7'

## AIM:
To write a Python function `def leftRotate(self, z):` to perform the left rotation operation in an AVL Tree and insert the element '7' into it.

---

## ALGORITHM:

### Step 1: Start the program.

### Step 2: Define the `TreeNode` class to represent each node in the AVL Tree:
- Key value
- Left and right child pointers
- Height of the node

### Step 3: Define the `AVL_Tree` class to manage AVL operations.

### Step 4: In the `insert()` method:
- Insert the key using standard Binary Search Tree logic.
- Update the height of the current node.
- Calculate the balance factor to detect imbalance.
- Based on balance factor and key position, perform necessary rotations.

### Step 5: Define `leftRotate(z)` method:
- Let `y = z.right` and `T2 = y.left`
- Make `z` the left child of `y`
- Assign `T2` as the right child of `z`
- Update heights of `z` and `y`
- Return `y` as the new root of the subtree

### Step 6: Insert the key `'7'` using the `insert()` method. If it causes imbalance, perform appropriate rotation.

### Step 7: Display the tree using `preOrder()` traversal to show the structure after insertion and rotation.

### Step 8: End the program.

---

## PYTHON PROGRAM

```
#Reg.NO-212223060119
#Name-Kavindra T G
ENTER YOUR CODE
class TreeNode(object):
	def __init__(self, val):
		self.val = val
		self.left = None
		self.right = None
		self.height = 1

class AVL_Tree(object):
	def insert(self, root, key):
		if not root:
			return TreeNode(key)
		elif key < root.val:
			root.left = self.insert(root.left, key)
		else:
			root.right = self.insert(root.right, key)

	
		root.height = 1 + max(self.getHeight(root.left),
						self.getHeight(root.right))

		balance = self.getBalance(root)

		if balance > 1 and key < root.left.val:
			return self.rightRotate(root)

	
		if balance < -1 and key > root.right.val:
			return self.leftRotate(root)

		
		if balance > 1 and key > root.left.val:
			root.left = self.leftRotate(root.left)
			return self.rightRotate(root)
   
		if balance < -1 and key < root.right.val:
			root.right = self.rightRotate(root.right)
			return self.leftRotate(root)

		return root

	def leftRotate(z):

		y = z.left
		T2 = y.right

	
		y.right = z
		z.left = T2

		z.height = 1 + max(self.getHeight(z.left),
						self.getHeight(z.right))
		y.height = 1 + max(self.getHeight(y.left),
						self.getHeight(y.right))

		return y

	
	def getHeight(self, root):
		if not root:
			return 0

		return root.height

	def getBalance(self, root):
		if not root:
			return 0

		return self.getHeight(root.left) - self.getHeight(root.right)

	def preOrder(self, root):

		if not root:
			return

		print("{0} ".format(root.val), end="")
		self.preOrder(root.left)
		self.preOrder(root.right)


myTree = AVL_Tree()
root = None
n=int(input())
root = myTree.insert(root, 13)
root = myTree.insert(root, 10)
root = myTree.insert(root, 15)
root = myTree.insert(root, 5)
root = myTree.insert(root, 11)
root = myTree.insert(root, 16)
root = myTree.insert(root, n)
    


print("Preorder traversal of the constructed AVL tree is")
myTree.preOrder(root)
print()


```

## OUTPUT
![image](https://github.com/user-attachments/assets/511a8909-6392-4835-994d-b50ed1e352b9)

## RESULT
Thus, the python function `def leftRotate(self, z):` to perform the left rotation operation in an AVL Tree and insert the element '7' into it has been executed and verified successfully.
