# experiment-10
exp10
# =========================
# Node Class for BST
# =========================
class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

# =========================
# BST Class
# =========================
class BST:
    def __init__(self):
        self.root = None

    # -------- Insertion --------
    def insert(self, root, key):
        if root is None:
            return Node(key)
        if key < root.key:
            root.left = self.insert(root.left, key)
        elif key > root.key:
            root.right = self.insert(root.right, key)
        return root

    # -------- Search --------
    def search(self, root, key):
        if root is None:
            return False
        if root.key == key:
            return True
        elif key < root.key:
            return self.search(root.left, key)
        else:
            return self.search(root.right, key)

    # -------- Find Minimum --------
    def minValueNode(self, node):
        current = node
        while current.left is not None:
            current = current.left
        return current

    # -------- Deletion --------
    def delete(self, root, key):
        if root is None:
            return root
        if key < root.key:
            root.left = self.delete(root.left, key)
        elif key > root.key:
            root.right = self.delete(root.right, key)
        else:
            # Node with only one child or no child
            if root.left is None:
                temp = root.right
                root = None
                return temp
            elif root.right is None:
                temp = root.left
                root = None
                return temp
            # Node with two children: get inorder successor
            temp = self.minValueNode(root.right)
            root.key = temp.key
            root.right = self.delete(root.right, temp.key)
        return root

    # -------- Display (Inorder Traversal) --------
    def inorder(self, root):
        if root:
            self.inorder(root.left)
            print(root.key, end=" ")
            self.inorder(root.right)

# =========================
# Runtime Interaction
# =========================
bst = BST()
root = None

# Insert values
n = int(input("How many values do you want to insert? "))
for _ in range(n):
    val = int(input("Enter value to insert: "))
    root = bst.insert(root, val)

print("\nInorder Traversal after insertion:")
bst.inorder(root)
print("\n")

# Search values
m = int(input("How many values do you want to search? "))
for _ in range(m):
    key = int(input("Enter value to search: "))
    found = bst.search(root, key)
    print(f"Search {key}: {'Found' if found else 'Not Found'}")

print("\n")

# Delete values
k = int(input("How many values do you want to delete? "))
for _ in range(k):
    key = int(input("Enter value to delete: "))
    root = bst.delete(root, key)
    print(f"Inorder Traversal after deleting {key}:")
    bst.inorder(root)
    print("\n")
