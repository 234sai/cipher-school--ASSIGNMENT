# cipher-school--ASSIGNMENT
project assignment -BST
Alright, let me give you a detailed description of this project. It's all about implementing a basic Binary Search Tree (BST) in C++. Now, a BST is a pretty important data structure in computer science, used for efficient data storage, retrieval, and management. This project covers the essential operations like insertion, search, and deletion of nodes within the tree.

First up, the tech stack: We've got C++ as the programming language, used for the core data structure and algorithms. As for the development environment, you can use Visual Studio Code or any other C++ supported IDE like CLion or Eclipse, along with the GCC (GNU Compiler Collection) to compile the C++ code.

Moving on to the project details. The project is called "Binary Search Tree Implementation," and it's pretty straightforward. We have a Node Class which represents each node in the BST, with attributes like an integer data, a pointer to the left child, and a pointer to the right child. The constructor initializes a node with a given value and sets the child pointers to nullptr.

Then, we have the BinarySearchTree Class, which contains a pointer to the root node of the BST. The constructor simply initializes the root to nullptr. As for the operations, we've got:

Search: Checks if a given value exists in the BST. Uses a recursive helper function to traverse the tree.

Insert: Adds a new value to the BST. Again, uses a recursive helper function to find the correct position for the new node.

Delete: Removes a node with a specified value from the BST. Handles different cases like deleting a leaf node, a node with one child, and a node with two children. Uses a recursive helper function to manage the deletion process and ensure the BST properties are maintained.

In-order Traversal: (Optional for testing) Prints the BST nodes in ascending order, helping to verify the correctness of insertion and deletion operations.

Helper Functions: These include searchHelper, insertHelper, deleteHelper, and minValue, which are used in the respective operations.

To use this project, the main function demonstrates the insertion of multiple values, searching for specific values, and deleting nodes from the BST. And if you include the inorderTraversal method, you can use it to print the BST in ascending order, which is great for verifying the operations.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
#include <iostream>

class Node {
public:
    int data;
    Node* left;
    Node* right;

    Node(int value) {
        data = value;
        left = nullptr;
        right = nullptr;
    }
};

class BinarySearchTree {
public:
    BinarySearchTree() {
        root = nullptr;
    }

    bool search(int value) {
        return searchHelper(root, value);
    }

    void insert(int value) {
        root = insertHelper(root, value);
    }

    void deleteNode(int value) {
        root = deleteHelper(root, value);
    }

    void inorderTraversal() {
        inorderHelper(root);
    }

private:
    Node* root;

    bool searchHelper(Node* node, int value) {
        if (node == nullptr) {
            return false;
        }
        if (value == node->data) {
            return true;
        }
        if (value < node->data) {
            return searchHelper(node->left, value);
        } else {
            return searchHelper(node->right, value);
        }
    }

    Node* insertHelper(Node* node, int value) {
        if (node == nullptr) {
            return new Node(value);
        }
        if (value < node->data) {
            node->left = insertHelper(node->left, value);
        } else if (value > node->data) {
            node->right = insertHelper(node->right, value);
        }
        return node;
    }

    Node* deleteHelper(Node* node, int value) {
        if (node == nullptr) {
            return node;
        }
        if (value < node->data) {
            node->left = deleteHelper(node->left, value);
        } else if (value > node->data) {
            node->right = deleteHelper(node->right, value);
        } else {
            if (node->left == nullptr) {
                Node* temp = node->right;
                delete node;
                return temp;
            } else if (node->right == nullptr) {
                Node* temp = node->left;
                delete node;
                return temp;
            }
            node->data = minValue(node->right);
            node->right = deleteHelper(node->right, node->data);
        }
        return node;
    }

    int minValue(Node* node) {
        int minv = node->data;
        while (node->left != nullptr) {
            minv = node->left->data;
            node = node->left;
        }
        return minv;
    }

    void inorderHelper(Node* node) {
        if (node == nullptr) {
            return;
        }
        inorderHelper(node->left);
        std::cout << node->data << " ";
        inorderHelper(node->right);
    }
};

int main() {
    BinarySearchTree bst;
    bst.insert(50);
    bst.insert(30);
    bst.insert(20);
    bst.insert(40);
    bst.insert(70);
    bst.insert(60);
    bst.insert(80);

    std::cout << "Inorder traversal: ";
    bst.inorderTraversal();
    std::cout << std::endl;

    std::cout << "Search 20: " << (bst.search(20) ? "Found" : "Not Found") << std::endl;
    std::cout << "Search 25: " << (bst.search(25) ? "Found" : "Not Found") << std::endl;

    bst.deleteNode(20);
    std::cout << "Inorder traversal after deleting 20: ";
    bst.inorderTraversal();
    std::cout << std::endl;

    bst.deleteNode(30);
    std::cout << "Inorder traversal after deleting 30: ";
    bst.inorderTraversal();
    std::cout << std::endl;

    bst.deleteNode(50);
    std::cout << "Inorder traversal after deleting 50: ";
    bst.inorderTraversal();
    std::cout << std::endl;

    return 0;
}

