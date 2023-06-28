# **Assignment 20 - Tree**

### 💡 **Question 1**

Given a binary tree, your task is to find subtree with maximum sum in tree.

Examples:

Input1 :

       1

     /   \

2      3

/ \    / \

4   5  6   7

Output1 : 28

As all the tree elements are positive, the largest subtree sum is equal to sum of all tree elements.

Input2 :

1

     /    \

-2      3

/ \    /  \

4   5  -6   2

Output2 : 7

Subtree with largest sum is :

-2

/ \

4   5

Also, entire tree sum is also 7.

## **Solution**

```cpp
int maxSum(Node* root, int &ans){
    if(root == NULL){
        return 0;
    }
    int l = maxSum(root->left, ans);
    int r = maxSum(root->right, ans);
    int temp = max(max(l, r) + root->data, root->data);
    int res = max(temp, l + r + root->data);
    ans = max(ans, res);
    return temp;
}

int findLargestSubtreeSum(Node* root){
    int ans = INT_MIN;
    maxSum(root, ans);
    return ans;
}
```

### 💡 **Question 2**

Construct the BST (Binary Search Tree) from its given level order traversal.

Example:

Input: arr[] = {7, 4, 12, 3, 6, 8, 1, 5, 10}

Output: BST:

            7

         /    \

       4     12

     /  \     /

    3   6  8

/   /   \

1  5   10

## **Solution**

```cpp
Node* constructBST(int arr[], int n){
  if(n == 0){
      return NULL;
  }
  Node* root = new Node(arr[0]);
  queue<Node*> q;
  q.push(root);
  int i = 1;
  while(i < n){
    Node* temp = q.front();
    q.pop();
    if(arr[i] < temp->data){
        temp->left = new Node(arr[i]);
        q.push(temp->left);
        i++;
    }
    if(i < n && arr[i] > temp->data){
        temp->right = new Node(arr[i]);
        q.push(temp->right);
        i++;
    }
  }
  return root;
}
```
