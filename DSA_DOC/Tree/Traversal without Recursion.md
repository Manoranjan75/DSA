# Inorder, Preorder and Postorder without Recursion
Preorder (Root → Left → Right):
Use a stack to process the root first. Pop a node, process it, 
then push its right child followed by its left child so the left subtree is handled first.

Inorder (Left → Root → Right):
Use a stack to go as left as possible, pushing nodes. When no left child exists, pop a node, process it, 
and move to its right subtree.

Postorder (Left → Right → Root):
Use two stacks. The first collects nodes in modified order, and the second reverses it so children are processed before the root.

## Time and Space Complexity:
- Preorder: Time O(N) and Space O(H), where H is the height of the tree.
- Inorder: Time O(N) and Space O(H), where H is the height of the tree.
- Postorder: Time O(N) and Space O(N), in case of using two stacks. In case of 1 stack Space is O(H).

 ```cpp

void preorderTraversal(Node* root) {
    if (root == NULL) return;

    stack<Node*> st;
    st.push(root);

    while (!st.empty()) {
        Node* curr = st.top();
        st.pop();

        // Process root
        cout << curr->data << " ";

        // Push right first
        if (curr->right)
            st.push(curr->right);

        // Push left
        if (curr->left)
            st.push(curr->left);
    }
}



//Inorder Traversal, Time: O(N) and Space: O(H), where H is the height of the tree.
void inorderTraversal(Node* root) {
    stack<Node*> st;
    Node* curr = root;

    while (curr != NULL || !st.empty()) {

        // Step 1: Go to extreme left
        while (curr != NULL) {
            st.push(curr);
            curr = curr->left;
        }

        // Step 2: Process node
        curr = st.top();
        st.pop();
        cout << curr->data << " ";

        // Step 3: Move to right subtree
        curr = curr->right;
    }
}


//Postorder Traversal, Time: O(N) and Space: O(N).
void postorderTraversal(Node* root) {
    if (root == NULL) return;

    stack<Node*> st1, st2;
    st1.push(root);

    while (!st1.empty()) {
        Node* curr = st1.top();
        st1.pop();

        st2.push(curr);

        if (curr->left)
            st1.push(curr->left);

        if (curr->right)
            st1.push(curr->right);
    }

    while (!st2.empty()) {
        cout << st2.top()->data << " ";
        st2.pop();
    }
}

// Postorder using one stack, Time: O(N) and space: O(H).
void postorderTraversal(Node* root) {
    if (root == NULL) return;

    stack<Node*> st;
    Node* curr = root;
    Node* lastVisited = NULL;

    while (curr != NULL || !st.empty()) {

        // Step 1: Go as left as possible
        if (curr != NULL) {
            st.push(curr);
            curr = curr->left;
        } 
        else {
            Node* topNode = st.top();

            // Step 2: If right child exists and not yet visited
            if (topNode->right != NULL && lastVisited != topNode->right) {
                curr = topNode->right;
            } 
            else {
                // Step 3: Process node
                cout << topNode->data << " ";
                lastVisited = topNode;
                st.pop();
            }
        }
    }
}
