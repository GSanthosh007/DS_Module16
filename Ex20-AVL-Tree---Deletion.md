# Ex4(E) AVL Tree - Deletion
## AIM:
To write a Java program to delete an element from an AVL Tree with automatic rebalancing.

## Algorithm
1. Start  
2. Search for the node containing the value to delete starting from the root.  
3. Delete the node using standard BST deletion rules:  
   - Node with no child: remove directly.  
   - Node with one child: replace with child.  
   - Node with two children: replace with inorder successor.  
4. Update the height of the affected nodes.  
5. Calculate the Balance Factor (BF) for each node.  
6. Perform rotations (LL, LR, RR, RL) if a node is unbalanced.  
7. Continue until the tree is balanced again.  
8. End.

## Program:
```java
/*
Program to delete an element from an AVL Tree
Developed by: Santhosh G
RegisterNumber: 212223240152
*/

class Node {
    int data, height;
    Node left, right;

    Node(int d) {
        data = d;
        height = 1;
    }
}

public class AVLDeletion {

    int height(Node n) {
        return (n == null) ? 0 : n.height;
    }

    int getBalance(Node n) {
        return (n == null) ? 0 : height(n.left) - height(n.right);
    }

    Node rightRotate(Node y) {
        Node x = y.left;
        Node T2 = x.right;

        x.right = y;
        y.left = T2;

        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        return x;
    }

    Node leftRotate(Node x) {
        Node y = x.right;
        Node T2 = y.left;

        y.left = x;
        x.right = T2;

        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        return y;
    }

    Node minValueNode(Node node) {
        Node current = node;
        while (current.left != null)
            current = current.left;
        return current;
    }

    Node delete(Node root, int key) {
        if (root == null)
            return null;

        if (key < root.data)
            root.left = delete(root.left, key);
        else if (key > root.data)
            root.right = delete(root.right, key);
        else {
            if ((root.left == null) || (root.right == null)) {
                Node temp = (root.left != null) ? root.left : root.right;
                if (temp == null) {
                    root = null;
                } else {
                    root = temp;
                }
            } else {
                Node temp = minValueNode(root.right);
                root.data = temp.data;
                root.right = delete(root.right, temp.data);
            }
        }

        if (root == null)
            return root;

        root.height = 1 + Math.max(height(root.left), height(root.right));

        int balance = getBalance(root);

        if (balance > 1 && getBalance(root.left) >= 0)
            return rightRotate(root);

        if (balance > 1 && getBalance(root.left) < 0) {
            root.left = leftRotate(root.left);
            return rightRotate(root);
        }

        if (balance < -1 && getBalance(root.right) <= 0)
            return leftRotate(root);

        if (balance < -1 && getBalance(root.right) > 0) {
            root.right = rightRotate(root.right);
            return leftRotate(root);
        }

        return root;
    }

    public static void main(String[] args) {
        AVLDeletion tree = new AVLDeletion();
        Node root = new Node(30);
        root.left = new Node(20);
        root.right = new Node(40);
        root.left.left = new Node(10);

        root = tree.delete(root, 20);

        System.out.println("AVL Tree deletion completed.");
    }
}
```

# Output:
<img width="1338" height="249" alt="9483ef24-e2a3-4f53-8584-87920281ce22" src="https://github.com/user-attachments/assets/51ae635d-3cff-4f42-a1b9-7d7e0a92c19d" />


# Result:
Thus, the Java program to delete an element from an AVL Tree is implemented successfully.


