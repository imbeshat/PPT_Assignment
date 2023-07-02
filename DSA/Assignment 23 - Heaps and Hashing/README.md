# **Assignment 23 - Heaps and Hashing**

### 💡 **Question 1**

Given preorder of a binary tree, calculate its **[depth(or height)](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/)** [starting from depth 0]. The preorder is given as a string with two possible characters.

1. ‘l’ denotes the leaf
2. ‘n’ denotes internal node

The given tree can be seen as a full binary tree where every node has 0 or two children. The two children of a node can ‘n’ or ‘l’ or mix of both.

**Examples :**

Input : nlnll
Output : 2

Input : nlnnlll
Output : 3

## **Solution**

```cpp
int findDepth(string tree, int n)
{
    int level = 0, maxlevel = 0;
    for (int i = 0; i < n; ++i) {
        if (tree[i] == 'n') {
            ++level;
            maxlevel = max(maxlevel, level);
        } else
            --level;
    }
    return maxlevel;
}
```

### 💡 **Question 2**

Given a Binary tree, the task is to print the **left view** of the Binary Tree. The left view of a Binary Tree is a set of leftmost nodes for every level.

**Examples:**

**_Input:_**

            4

          /   \

        5     2

             /   \

            3     1

           /  \

          6    7

**\*Output:** 4 5 3 6\*

**_Input:_**

                    1

                  /   \

                2       3

                 \

                   4

                     \

                        5

                           \

                             6

**Output:** 1 2 4 5 6

## **Solution**

```cpp
void leftView(Node* root)
{
    if (!root)
        return;
    queue<Node*> q;
    q.push(root);
    while (!q.empty()) {
        int n = q.size();
        for (int i = 1; i <= n; i++) {
            Node* temp = q.front();
            q.pop();
            if (i == 1)
                cout << temp->data << " ";
            if (temp->left != NULL)
                q.push(temp->left);
            if (temp->right != NULL)
                q.push(temp->right);
        }
    }
}
```

### 💡 **Question 3**

Given a Binary Tree, print the Right view of it.

The right view of a Binary Tree is a set of nodes visible when the tree is visited from the Right side.

**Examples:**

**Input:**

         1

      /     \

2        3

/   \       /  \

4     5   6    7

             \

               8

**Output**:

Right view of the tree is 1 3 7 8

**Input:**

         1

       /

    8

/

7

**Output**:

Right view of the tree is 1 8 7

## **Solution**

```cpp
void rightView(Node* root)
{
  if (!root)
    return;
  queue<Node*> q;
  q.push(root);
  while (!q.empty()) {
    int n = q.size();
    for (int i = 1; i <= n; i++) {
        Node* temp = q.front();
        q.pop();
        if (i == n)
            cout << temp->data << " ";
        if (temp->left != NULL)
            q.push(temp->left);
        if (temp->right != NULL)
            q.push(temp->right);
    }
  }
}
```

### 💡 **Question 4**

Given a Binary Tree, The task is to print the **bottom view** from left to right. A node **x** is there in output if x is the bottommost node at its horizontal distance. The horizontal distance of the left child of a node x is equal to a horizontal distance of x minus 1, and that of a right child is the horizontal distance of x plus 1.

**Examples:**

**Input:**

             20

           /     \

        8         22

    /      \         \

5         3        25

        /    \

10       14

**Output:** 5, 10, 3, 14, 25.

**Input:**

             20

           /     \

        8         22

    /      \      /   \

5         3   4     25

         /    \

     10       14

**Output:**

5 10 4 14 25.

**Explanation:**

If there are multiple bottom-most nodes for a horizontal distance from the root, then print the later one in the level traversal.

**3 and 4** are both the bottom-most nodes at a horizontal distance of 0, we need to print 4.

## **Solution**

```cpp
void bottomView(Node* root)
{
  if (!root)
      return;
  map<int, int> m;
  queue<pair<Node*, int> > q;
  q.push({ root, 0 });
  while (!q.empty()) {
    pair<Node*, int> p = q.front();
    Node* curr = p.first;
    int hd = p.second;
    m[hd] = curr->data;
    q.pop();
    if (curr->left != NULL)
        q.push({ curr->left, hd - 1 });
    if (curr->right != NULL)
      q.push({ curr->right, hd + 1 });
  }
  for (auto i = m.begin(); i != m.end(); ++i)
    cout << i->second << " ";
}
```
