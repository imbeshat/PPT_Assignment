# **Assignment 22 - Tree**

### 💡 **Question 1**

Given a Binary Tree (Bt), convert it to a Doubly Linked List(DLL). The left and right pointers in nodes are to be used as previous and next pointers respectively in converted DLL. The order of nodes in DLL must be the same as in Inorder for the given Binary Tree. The first node of Inorder traversal (leftmost node in BT) must be the head node of the DLL.

## **Solution**

```cpp
void convert(Node* root, vector<Node*> &v, int &i){
  if(root == NULL){
    return;
  }
  convert(root->left, v, i);
  v.push_back(root);
  convert(root->right, v, i);
}

Node * bToDLL(Node *root)
{
  vector<Node*> v;
  int i = 0;
  convert(root, v, i);
  for(int i = 0; i < v.size(); i++){
    if(i == 0){
        v[i]->left = NULL;
        v[i]->right = v[i+1];
    }
    else if(i == v.size()-1){
        v[i]->left = v[i-1];
        v[i]->right = NULL;
    }
    else{
        v[i]->left = v[i-1];
        v[i]->right = v[i+1];
    }
  }
  return v[0];
}
```

### 💡 **Question 2**

A Given a binary tree, the task is to flip the binary tree towards the right direction that is clockwise. See the below examples to see the transformation.

In the flip operation, the leftmost node becomes the root of the flipped tree and its parent becomes its right child and the right sibling becomes its left child and the same should be done for all left most nodes recursively.

## **Solution**

```cpp
void flip(Node* root){
  if(root == NULL){
    return;
  }
  flip(root->left);
  flip(root->right);
  if(root->left != NULL){
    Node* temp = root->left;
    root->left = root->right;
    root->right = temp;
  }
}

Node* solve(Node* root){
  flip(root);
  return root;
}
```

### 💡 **Question 3**

Given a binary tree, print all its root-to-leaf paths without using recursion. For example, consider the following Binary Tree.

Input:

```
        6
     /    \
    3      5
  /   \     \
 2     5     4
     /   \
    7     4
```

Output:

There are 4 leaves, hence 4 root to leaf paths -
6->3->2
6->3->5->7
6->3->5->4
6->5>4

## **Solution**

```cpp
void printPaths(Node* root){
  if(root == NULL){
    return;
  }
  stack<Node*> s;
  s.push(root);
  while(!s.empty()){
    Node* temp = s.top();
    s.pop();
    if(temp->left == NULL && temp->right == NULL){
      Node* temp2 = temp;
      while(temp2 != NULL){
        cout<<temp2->data<<" ";
        temp2 = temp2->parent;
      }
      cout<<endl;
    }
    if(temp->right != NULL){
      temp->right->parent = temp;
      s.push(temp->right);
    }
    if(temp->left != NULL){
      temp->left->parent = temp;
      s.push(temp->left);
    }
  }
}
```

### 💡 **Question 4**

Given Preorder, Inorder and Postorder traversals of some tree. Write a program to check if they all are of the same tree.

**Examples:**

Input :

        Inorder -> 4 2 5 1 3
        Preorder -> 1 2 4 5 3
        Postorder -> 4 5 2 3 1

Output :

Yes
Explanation :

All of the above three traversals are of
the same tree

                           1
                         /   \
                        2     3
                      /   \
                     4     5

Input :

        Inorder -> 4 2 5 1 3
        Preorder -> 1 5 4 2 3
        Postorder -> 4 1 2 3 5

Output :

No

## **Solution**

```cpp
bool checktree(int preorder[], int inorder[], int postorder[], int N)
{
    // if the array lengths are 0, then all of them are obviously equal
    if (N == 0)
        return 1;

    // if array lengths are 1, then check if all of them are equal
    if (N == 1)
        return (preorder[0] == inorder[0]) && (inorder[0] == postorder[0]);

    // search for first element of preorder in inorder array
    int idx = -1;
    for (int i = 0; i < N; ++i)
        if (inorder[i] == preorder[0]) {
            idx = i;
            break;
        }

    if (idx == -1)
        return 0;

    // matching element in postorder array
    if (preorder[0] != postorder[N - 1])
        return 0;

    // check for the left subtree
    int ret1 = checktree(preorder + 1, inorder, postorder, idx);

    // check for the right subtree
    int ret2 = checktree(preorder + idx + 1, inorder + idx + 1, postorder + idx, N - idx - 1);

    // return 1 only if both of them are correct else 0
    return (ret1 && ret2);
}
```
