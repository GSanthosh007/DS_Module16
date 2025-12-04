# Ex 4A AVL Tree - Insertion
## DATE:24/03/2025
## AIM:
To write a Java program to insert elements into an AVL Tree using rotations for balancing.

## Algorithm
1. Start  
2. Create a Node class with data, height, left, and right references.  
3. If the current node is null, create and return a new node.  
4. Recursively insert the value into the left or right subtree based on comparison.  
5. Update the height of the current node.  
6. Compute the Balance Factor (BF).  
7. If BF is +2 or -2, apply the required rotation: LL, LR, RR, or RL.  
8. Return the updated root after insertion and balancing.  
9. End.

## Program:
```
/*
Program to insert the elements in an AVL Tree
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

public class AVLTree {

    int height(Node N) {
        if (N == null)
            return 0;
        return N.height;
    }

    int getBalance(Node N) {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
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

    Node insert(Node node, int key) {
        if (node == null)
            return new Node(key);

        if (key < node.data)
            node.left = insert(node.left, key);
        else if (key > node.data)
            node.right = insert(node.right, key);
        else
            return node;

        node.height = 1 + Math.max(height(node.left), height(node.right));

        int bf = getBalance(node);

        if (bf > 1 && key < node.left.data)
            return rightRotate(node);

        if (bf < -1 && key > node.right.data)
            return leftRotate(node);

        if (bf > 1 && key > node.left.data) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        if (bf < -1 && key < node.right.data) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        return node;
    }

    public static void main(String[] args) {
        AVLTree tree = new AVLTree();
        Node root = null;

        root = tree.insert(root, 30);
        root = tree.insert(root, 20);
        root = tree.insert(root, 40);
        root = tree.insert(root, 10);

        System.out.println("AVL Tree insertion completed.");
    }
}
```
# Output:
<img width="789" height="167" alt="35f7dc7d-c765-42ab-82b3-af87c9323c8a" src="https://github.com/user-attachments/assets/2c8468c8-03a1-474e-8e67-45384290d819" />


# Result:
Thus, the Java program to insert elements in an AVL Tree is implemented successfully.
