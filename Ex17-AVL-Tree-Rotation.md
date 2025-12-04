# Ex4(B) AVL Tree – Rotation
## AIM:
To write a Java program to perform a right rotation operation in an AVL Tree.

## Algorithm
1. Start  
2. Create a Node class with data, height, left, and right references.  
3. Assign y as the left child of x.  
4. Move y’s right subtree to become x’s left subtree.  
5. Set y’s right child as x.  
6. Update the heights of both x and y.  
7. Return y as the new root after rotation.  
8. End.

## Program:
```java
/*
Program to perform right rotation in AVL Tree
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

public class AVLRotation {

    int height(Node n) {
        if (n == null)
            return 0;
        return n.height;
    }

    // Right Rotation
    Node rotateRight(Node x) {
        Node y = x.left;
        Node temp = y.right;

        y.right = x;
        x.left = temp;

        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        return y;
    }

    public static void main(String[] args) {
        AVLRotation obj = new AVLRotation();

        Node x = new Node(30);
        x.left = new Node(20);
        x.left.left = new Node(10);

        Node newRoot = obj.rotateRight(x);

        System.out.println("Right Rotation performed successfully.");
        System.out.println("New root after rotation: " + newRoot.data);
    }
}

```
# Output:
<img width="943" height="201" alt="f7c9bf3d-195f-41ab-95fc-004ba497b4d3" src="https://github.com/user-attachments/assets/7f974d1f-9f36-47d4-bfce-a6a6b9ad7a53" />


# Result:
Thus, the Java program to perform right rotation in an AVL Tree is implemented successfully.
