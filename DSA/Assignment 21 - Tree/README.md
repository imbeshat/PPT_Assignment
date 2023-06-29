# **Assignment 21 - Tree**

### 💡 **Question 1**

You are given a binary tree. The binary tree is represented using the TreeNode class. Each TreeNode has an integer value and left and right children, represented using the TreeNode class itself. Convert this binary tree into a binary search tree.

Input:

          10

        /   \

      2      7

      /   \

      8    4

Output:

          8

        /   \

      4     10

    / \

    2 7

## **Solution**

```cpp
void inorder(TreeNode* root, vector<int> &v){
  if(root == NULL){
      return;
  }
  inorder(root->left, v);
  v.push_back(root->val);
  inorder(root->right, v);
}

void convert(TreeNode* root, vector<int> &v, int &i){
  if(root == NULL){
      return;
  }
  convert(root->left, v, i);
  root->val = v[i];
  i++;
  convert(root->right, v, i);
}

TreeNode* solve(TreeNode* root){
  vector<int> v;
  inorder(root, v);
  sort(v.begin(), v.end());
  int i = 0;
  convert(root, v, i);
  return root;
}
```

### 💡 **Question 2**

Given a Binary Search Tree with all unique values and two keys. Find the distance between two nodes in BST. The given keys always exist in BST.

Example:

Consider the following BST:
**Input-1:**

n = 9

values = [8, 3, 1, 6, 4, 7, 10, 14,13]

node-1 = 6

node-2 = 14

**Output-1:**

The distance between the two keys = 4

**Input-2:**

n = 9

values = [8, 3, 1, 6, 4, 7, 10, 14,13]

node-1 = 3

node-2 = 4

**Output-2:**

The distance between the two keys = 2

## **Solution**

```cpp
int findDist(Node* root, int a, int b){
  if(root == NULL){
      return 0;
  }
  if(root->data > a && root->data > b){
      return findDist(root->left, a, b);
  }
  if(root->data < a && root->data < b){
      return findDist(root->right, a, b);
  }
  if(root->data >= a && root->data <= b){
      return findDist(root, a) + findDist(root, b) - 2;
  }
}

int findDist(Node* root, int a){
  if(root == NULL){
      return 0;
  }
  if(root->data == a){
      return 0;
  }
  if(root->data > a){
      return 1 + findDist(root->left, a);
  }
  if(root->data < a){
      return 1 + findDist(root->right, a);
  }
}
```

### 💡 **Question 3**

Write a program to convert a binary tree to a doubly linked list.

Input:

        10

       /   \

     5     20

           /   \

        30     35

Output:

5 10 30 20 35

## **Solution**

```cpp
void convert(Node* root, Node* &head, Node* &prev){
  if(root == NULL){
      return;
  }
  convert(root->left, head, prev);
  if(prev == NULL){
      head = root;
  }
  else{
      root->left = prev;
      prev->right = root;
  }
  prev = root;
  convert(root->right, head, prev);
}

Node* bToDLL(Node* root){
  Node* head = NULL;
  Node* prev = NULL;
  convert(root, head, prev);
  return head;
}
```

### 💡 **Question 4**

Write a program to connect nodes at the same level.

Input:

        1

      /   \

    2      3

/ \ / \

4 5 6 7

Output:

1 → -1

2 → 3

3 → -1

4 → 5

5 → 6

6 → 7

7 → -1

## **Solution**

```cpp
void connect(Node* root){
  if(root == NULL){
      return;
  }
  queue<Node*> q;
  q.push(root);
  q.push(NULL);
  while(!q.empty()){
      Node* temp = q.front();
      q.pop();
      if(temp != NULL){
          temp->nextRight = q.front();
          if(temp->left){
              q.push(temp->left);
          }
          if(temp->right){
              q.push(temp->right);
          }
      }
      else if(!q.empty()){
          q.push(NULL);
      }
  }
}
```
