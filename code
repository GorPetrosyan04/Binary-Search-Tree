import java.io.*;
import java.util.*;

public class PetroH7 {
    // root is a pointer to root of the BST
    Node root = null;
    // use prt for System.out to save typing
    PrintStream prt = System.out;

    // class Node
    private class Node {
        int[] data = new int[2]; // Data array to hold one or two data elements
        Node[] child = new Node[3]; // Child array to hold references to child nodes
        int count; // Number of data elements in the node

        // Node constructor
        Node(int x) {
            data[0] = x;
            child[0] = child[1] = child[2] = null;
            count = 1; // Initially, a node has one data element
        }
    } // end class Node

    // SearchResult class
    private class SearchResult {
        Node leaf;
        boolean found;

        // SearchResult Constructor
        SearchResult(Node t, boolean k) {
            leaf = t;
            found = k;
        }
    } // end class SearchResult

    // Inorder traversal of BST
    private void inorder() {
        if (root == null)
            return; // BST is empty
        prt.printf("\n\tInorder Traversal:");
        inorder(root);
    }// end inorder()

    // Inorder traversal from Node t
    private void inorder(Node t) {
        if (t == null)
            return; // BST is empty
        if (t.child[0] != null)
            inorder(t.child[0]);
        prt.printf("%d, ", t.data[0]);
        if (t.child[1] != null)
            inorder(t.child[1]);
        if (t.data[1] != 0) {
            prt.printf("%d, ", t.data[1]);
            if (t.child[2] != null)
                inorder(t.child[2]);
        }
    } // end inorder(t)

    // Search for x in a 2-3 tree
    private SearchResult search(int x) {
        return search(x, root); // call search from root node
    } // end search

    // Search for x in a 2-3 tree with root t
    private SearchResult search(int x, Node t) { // return null if x is duplicate
        if (t == null) // tree is empty;
            return new SearchResult(null, false);
        // end if t == null
        Node parent = t; // save t
        while (t != null) { // tree is not empty;
            parent = t; // save t
            switch (t.count) {
                // t has 2 children
                case 2:
                    if (x == t.data[0] || x == t.data[1]) // x is duplicate
                        return new SearchResult(t, true);
                    if (x < t.data[0])
                        t = t.child[0];
                    else if (x > t.data[1])
                        t = t.child[2];
                    else
                        t = t.child[1];
                    break;
                default:
                    if (x == t.data[0]) // node t has 1 data and x is duplicate
                        return new SearchResult(t, true);
                    if (x < t.data[0])
                        t = t.child[0];
                    else
                        t = t.child[1];
            } // end switch (t.count){
        } // end while
        // x is not found, so x should be inserted in its parent node
        return new SearchResult(parent, false); // leaf node pointed by parent
    } // end search

    // Insert x in 2-3 tree with root t
   private void insert(int x) {
    prt.printf("\n\t Insert %d ", x);
    if (root == null) { // insert x into empty 2-3 Tree
        root = new Node(x);
        return;
    } // end if
    // 2-3 tree is not empty, first search for x
    SearchResult r = search(x);
    if (!r.found) { // x is NOT duplicate insert it in r.leaf node;
        insert(x, r.leaf);
    } else // x is duplicate can not insert
        prt.printf(" OOPS.. Duplicate...");
    // Check if root needs to be split
    if (root.count == 2) {
        // Split the root node
        Node newRoot = new Node(root.data[1]); // Create a new root with the second data element
        newRoot.child[0] = root; // Make the old root the left child of the new root
        newRoot.child[1] = root.child[2]; // Assign t.link2 (the right child of the old root) as the right child of the new root

        // Disconnect t.link2 from root
        root.child[2] = null;
        
        root = newRoot; // Update the root pointer
    }
} // end insert


    // Insert element x into a 2-node or 3-node
    private void insertIntoNode(int x, Node t) {
        if (t.count == 1) {
            // 2-node, insert directly
            if (x < t.data[0]) {
                t.data[1] = t.data[0];
                t.data[0] = x;
            } else {
                t.data[1] = x;
            }
            t.count = 2;
        } else {
            // 3-node, promote median to parent
            if (x < t.data[0]) {
                shiftRight(t.data, 0);
                t.data[0] = x;
            } else if (x > t.data[1]) {
                shiftRight(t.data, 1);
                t.data[1] = x;
            } else {
                t.data[1] = t.data[0];
                t.data[0] = x;
            }
            t.count = 2;
        }
    }

    // Insert x in 2-3 tree with root t
    private void insert(int x, Node t) {
        // If node is a leaf node, insert x here
        if (t.child[0] == null) {
            insertIntoNode(x, t);
            return;
        }
        // Find appropriate child to continue insertion
        int i = findChild(x, t);
        insert(x, t.child[i]);
        if (t.child[i].count == 2) {
            // Split the node if it's a 3-node
            // You can add your split logic here if needed
            // However, in this example, we're not implementing the split method
        }
    } // end insert(x, t)

    // Find appropriate child index for insertion
    private int findChild(int x, Node t) {
        if (t.count == 2) {
            if (x < t.data[0]) {
                return 0;
            } else if (x > t.data[1]) {
                return 2;
            } else {
                return 1;
            }
        } else { // 1 data element
            if (x < t.data[0]) {
                return 0;
            } else {
                return 1;
            }
        }
    }

    // Shift elements in an array to the right starting from index i
    private void shiftRight(int[] arr, int i) {
        for (int j = arr.length - 1; j > i; j--) {
            arr[j] = arr[j - 1];
        }
    }

        // process method for BST insert and search
    private void process(String args[]) {
        prt.print("\n\tProcess method gets input file name from" +
                " program argument, then reads:" +
                "\n\t\tInteger No. of elements to insert in BST " +
                "followed by elements to insert" +
                "\n\t\tInteger No. of elements to search followed by element to search");
        // declare variables
        int cnt = args.length; // get no. of arguments
        String fname;
        if (cnt < 1) {
            prt.printf("\n\tOOOPS Invalid No. of arguments!");
            return;
        } // end if
        // get input file name
        fname = args[0];
        prt.printf("\n\t\tInput filename: %s", fname);
        // local variables
        int j, n, k, x;
        try {
            // open input file
            Scanner inf = new Scanner(new File(fname));
            // read no. of elements to insert
            n = inf.nextInt();
            prt.printf("\n\n\tInsert %d elements in the 2-3 tree:", n);
            for (j = 1; j <= n; j++) {
                x = inf.nextInt(); // read x
                prt.printf("%d, ", x);
                insert(x); // insert x in the 2-3 tree
            } // end for
            // print inorder traversal
            inorder();
            // read no. of elements to search in 2-3 tree
            n = inf.nextInt();
            prt.printf("\n\tSearch for %d elements in the 2-3 tree.", n);
            for (j = 1; j <= n; j++) {
                x = inf.nextInt(); // read x to search
                SearchResult result = search(x); // Search for x
                prt.printf("\n\t\tSearch for %2d in 2-3 tree: ", x);
                if (result.found)
                    prt.printf("Found");
                else
                    prt.printf("NOT Found");
            }// end for
            // close input file
            inf.close();
        } catch (Exception e) {
            prt.printf("\n\tRead Error! %s", e);
        }
    } // end process(fname)

    // main method
    public static void main(String args[]) throws Exception {
        System.out.printf("\n\tJava 2-3 Tree Program:" +
                "\n\t\tTo Compile: javac PetroH7.java" +
                "\n\t\tTo Execute: java PetroH7 inputfilename");
        // create an instance of 2-3 Tree class
        PetroH7 t = new PetroH7();
        // call process method
        t.process(args);
        System.out.printf("\n\tAuthor: Gor Petrosyan Date: " +
                java.time.LocalDate.now());
    } // end main
} // end class PetroH7
