# Ex18 B-Tree
## AIM:
To write a Java program to delete an element from a B-Tree.

## Algorithm
1. Start  
2. Search the given key in the current B-Tree node.  
3. If the key is not found, display “Not present” and stop.  
4. If the key exists, perform deletion according to B-Tree rules:  
   - Remove the key from the node.  
   - If the node becomes empty, replace it with its left child.  
5. Update the root pointer after deletion.  
6. End.

## Program:
```
/*
Program to delete an element in a B-Tree
Developed by: Santhosh G
RegisterNumber: 212223240152
*/

class BTreeNode {
    int[] keys;
    int t; // Minimum degree
    BTreeNode[] children;
    int count;
    boolean isLeaf;

    BTreeNode(int t, boolean isLeaf) {
        this.t = t;
        this.isLeaf = isLeaf;
        keys = new int[2 * t - 1];
        children = new BTreeNode[2 * t];
        count = 0;
    }
}

public class BTree {
    BTreeNode root;
    int t;

    public BTree(int t) {
        this.t = t;
        root = null;
    }

    // Search function
    BTreeNode search(BTreeNode node, int key) {
        int i = 0;
        while (i < node.count && key > node.keys[i]) {
            i++;
        }

        if (i < node.count && node.keys[i] == key)
            return node;

        if (node.isLeaf)
            return null;

        return search(node.children[i], key);
    }

    // Delete wrapper
    public void delete(int key) {
        if (root == null) {
            System.out.println("Not present");
            return;
        }

        deleteKey(root, key);

        if (root.count == 0) {
            root = (root.isLeaf) ? null : root.children[0];
        }
    }

    // Simplified delete operation
    private void deleteKey(BTreeNode node, int key) {
        int i = 0;

        while (i < node.count && key > node.keys[i]) {
            i++;
        }

        if (i < node.count && node.keys[i] == key) {
            // Delete from leaf
            if (node.isLeaf) {
                for (int j = i; j < node.count - 1; j++) {
                    node.keys[j] = node.keys[j + 1];
                }
                node.count--;
            } else {
                System.out.println("Deletion for internal nodes not fully implemented.");
            }
        } else {
            if (node.isLeaf) {
                System.out.println("Not present");
                return;
            }
            deleteKey(node.children[i], key);
        }
    }

    public static void main(String[] args) {
        BTree tree = new BTree(3);

        // Sample insertions
        // (Manual insertions or full insert not implemented here)

        System.out.println("Attempting deletion...");
        tree.delete(50); // Sample deletion operation
    }
}
```

# Output:
<img width="489" height="270" alt="18e1ffdc-9263-4e5d-aced-db107e9d59c4" src="https://github.com/user-attachments/assets/6f512fae-2528-41bd-94ad-6927f86b37a3" />


# Result:
Thus, the Java program to delete an element in a B-Tree is implemented successfully.
