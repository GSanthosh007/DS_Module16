# Ex4(D) B+ Tree
## AIM:
To write a Java program to traverse the elements in a B+ Tree using in-order traversal.

## Algorithm
1. Start  
2. Create a B+ Tree node class with data array, child pointers, leaf flag, and number of keys.  
3. For each key in the node, do:  
   - If the node is not a leaf, recursively traverse the child at that index.  
   - Print the current data element.  
4. After all keys, if the node is not a leaf, traverse the last child pointer.  
5. End after completing traversal.

## Program:
```java
/*
Program to traverse the elements in a B+ Tree
Developed by: Santhosh G
RegisterNumber: 212223240152
*/

class BPlusNode {
    int[] data;
    BPlusNode[] child_ptr;
    boolean leaf;
    int n;

    BPlusNode(int size, boolean isLeaf) {
        data = new int[size];
        child_ptr = new BPlusNode[size + 1];
        leaf = isLeaf;
        n = 0;
    }
}

public class BPlusTreeTraversal {

    static void traverse(BPlusNode p) {
        for (int i = 0; i < p.n; i++) {
            if (!p.leaf) {
                traverse(p.child_ptr[i]);
            }
            System.out.print(p.data[i] + " ");
        }
        if (!p.leaf) {
            traverse(p.child_ptr[p.n]);
        }
    }

    public static void main(String[] args) {
        BPlusNode root = new BPlusNode(3, false);
        BPlusNode child1 = new BPlusNode(3, true);
        BPlusNode child2 = new BPlusNode(3, true);

        child1.data[0] = 10;
        child1.data[1] = 20;
        child1.n = 2;

        child2.data[0] = 30;
        child2.data[1] = 40;
        child2.n = 2;

        root.data[0] = 25;
        root.child_ptr[0] = child1;
        root.child_ptr[1] = child2;
        root.n = 1;

        System.out.print("B+ Tree traversal: ");
        traverse(root);
    }
}
```

# Output:
<img width="888" height="306" alt="be479487-a127-44b2-8f68-334ef8ef1b3c" src="https://github.com/user-attachments/assets/e2e2884b-66e1-4cdc-9acf-93c5b1ebcfa2" />


# Result:
Thus, the Java program to traverse the elements in a B+ Tree is implemented successfully.
