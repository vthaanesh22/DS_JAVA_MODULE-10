# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE: 18-03-2026
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
## Algorithm
1. Read n and insert each of the n book IDs into a Binary Search Tree using the insert function.
2. In insert, if the tree is empty create a new node; otherwise recursively insert the key into the left or right subtree based on comparison.
3. Read q, the number of search queries.
4. For each query, use the search function: if the current node is null return false, if its value matches return true, else search left or right based on comparison.
5. Print “Found” if the key exists in the BST; otherwise print “Not Found.”

## Program:
```JAVA
/*
Program to constructs a Binary Search Tree (BST) using given Book IDs 
Developed by: Thaanesh V
RegisterNumber: 212223230228
*/
import java.util.*;

public class BookIDSearch {
    

    public static Node insert(Node root, int key) {
        //Type your Code
        if (root == null) 
        return new Node(key);
        if (key < root.data) 
        root.left = insert(root.left, key);
        else 
        root.right = insert(root.right, key);
        return root;
    }

    public static boolean search(Node root, int key) {
        //Type your Code
        if (root == null) 
        return false;
        if (root.data == key) 
        return true;
        return (key < root.data) ? search(root.left, key) : search(root.right, key);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Node root = null;
        for (int i = 0; i < n; i++) {
            root = insert(root, sc.nextInt());
        }
        int q = sc.nextInt();
        while (q-- > 0) {
            int key = sc.nextInt();
            System.out.println(search(root, key) ? "Found" : "Not Found");
        }
    }
}
class Node {
        int data;
        Node left, right;
        Node(int data) {
            this.data = data;
        }
    }

```

## Output:
<img width="1265" height="357" alt="image" src="https://github.com/user-attachments/assets/5b1e0d29-22bc-47ed-b91c-bb9831419015" />



## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.
