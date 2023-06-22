# **Assignment 15 - Stacks**

### 💡 **Question 1**

Given an array **arr[ ]** of size **N** having elements, the task is to find the next greater element for each element of the array in order of their appearance in the array.Next greater element of an element in the array is the nearest element on the right which is greater than the current element.If there does not exist next greater of current element, then next greater element for current element is -1. For example, next greater of the last element is always -1.

**Example 1:**
Input:
N = 4, arr[] = [1 3 2 4]
Output:
3 4 4 -1
Explanation:
In the array, the next larger element
to 1 is 3 , 3 is 4 , 2 is 4 and for 4 ?
since it doesn't exist, it is -1.

**Example 2:**
Input:
N = 5, arr[] [6 8 0 1 3]
Output:
8 -1 1 3 -1
Explanation:
In the array, the next larger element to
6 is 8, for 8 there is no larger elements
hence it is -1, for 0 it is 1 , for 1 it
is 3 and then for 3 there is no larger
element on right and hence -1.

## **Solution**

```cpp
vector<long long> nextLargerElement(vector<long long> arr, int n){
    vector<long long> ans(n);
    stack<long long> s;
    for(int i=n-1;i>=0;i--){
        while(!s.empty() && s.top()<=arr[i]){
            s.pop();
        }
        if(s.empty()){
            ans[i]=-1;
        }
        else{
            ans[i]=s.top();
        }
        s.push(arr[i]);
    }
    return ans;
}
```

### 💡 **Question 2**

Given an array **a** of integers of length **n**, find the nearest smaller number for every element such that the smaller element is on left side.If no small element present on the left print -1.

**Example 1:**
Input: n = 3
a = {1, 6, 2}
Output: -1 1 1
Explaination: There is no number at the
left of 1. Smaller number than 6 and 2 is 1.

**Example 2:**
Input: n = 6
a = {1, 5, 0, 3, 4, 5}
Output: -1 1 -1 0 3 4
Explaination: Upto 3 it is easy to see
the smaller numbers. But for 4 the smaller
numbers are 1, 0 and 3. But among them 3
is closest. Similary for 5 it is 4.

## **Solution**

```cpp
vector<int> leftSmaller(int n, int a[]){
    vector<int> ans(n);
    stack<int> s;
    for(int i=0;i<n;i++){
        while(!s.empty() && s.top()>=a[i]){
            s.pop();
        }
        if(s.empty()){
            ans[i]=-1;
        }
        else{
            ans[i]=s.top();
        }
        s.push(a[i]);
    }
    return ans;
}
```

### 💡 **Question 3**

Implement a Stack using two queues **q1** and **q2**.

**Example 1:**
Input:
push(2)
push(3)
pop()
push(4)
pop()
Output:3 4
Explanation:
push(2) the stack will be {2}
push(3) the stack will be {2 3}
pop() poped element will be 3 the
  stack will be {2}
push(4) the stack will be {2 4}
pop()   poped element will be 4

**Example 2:**
Input:
push(2)
pop()
pop()
push(3)
Output:2 -1

## **Solution**

```cpp
void QueueStack :: push(int x){
    q1.push(x);
}

int QueueStack :: pop(){
    if(q1.empty()){
        return -1;
    }
    while(q1.size()!=1){
        q2.push(q1.front());
        q1.pop();
    }
    int ans=q1.front();
    q1.pop();
    while(!q2.empty()){
        q1.push(q2.front());
        q2.pop();
    }
    return ans;
}
```

### 💡 **Question 4**

You are given a stack **St**. You have to reverse the stack using recursion.

**Example 1:**
Input:St = {3,2,1,7,6}
Output:{6,7,1,2,3}

**Example 2:**
Input:St = {4,3,9,6}
Output:{6,9,3,4}

## **Solution**

```cpp
void insertAtBottom(stack<int> &s,int x){
    if(s.empty()){
        s.push(x);
        return;
    }
    int y=s.top();
    s.pop();
    insertAtBottom(s,x);
    s.push(y);
}

void reverse(stack<int> &s){
    if(s.empty()){
        return;
    }
    int x=s.top();
    s.pop();
    reverse(s);
    insertAtBottom(s,x);
}
```

### 💡 **Question 5**

You are given a string **S**, the task is to reverse the string using stack.

**Example 1:**
Input: S="GeeksforGeeks"
Output: skeeGrofskeeG

## **Solution**

```cpp
string reverseString(CQStack s){
    string ans="";
    while(!s.isEmpty()){
        ans+=s.pop();
    }
    return ans;
}
```

### 💡 **Question 6**

Given string **S** representing a postfix expression, the task is to evaluate the expression and find the final value. Operators will only include the basic arithmetic operators like **\*, /, + and -**.

**Example 1:**
Input: S = "231\*+9-"
Output: -4
Explanation:
After solving the given expression,
we have -4 as result.

**Example 2:**
Input: S = "123+\*8-"
Output: -3
Explanation:
After solving the given postfix
expression, we have -3 as result.

## **Solution**

```cpp
int evaluatePostfix(string S){
    stack<int> s;
    for(int i=0;i<S.size();i++){
        if(S[i]>='0' && S[i]<='9'){
            s.push(S[i]-'0');
        }
        else{
            int a=s.top();
            s.pop();
            int b=s.top();
            s.pop();
            if(S[i]=='+'){
                s.push(b+a);
            }
            else if(S[i]=='-'){
                s.push(b-a);
            }
            else if(S[i]=='*'){
                s.push(b*a);
            }
            else if(S[i]=='/'){
                s.push(b/a);
            }
        }
    }
    return s.top();
}
```

### 💡 **Question 7**

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top(); // return 0
minStack.getMin(); // return -2

## **Solution**

```cpp
class MinStack {
public:
    /** initialize your data structure here. */
    stack<int> s;
    int minEle;
    MinStack() {
        minEle=INT_MAX;
    }

    void push(int val) {
        if(s.empty()){
            s.push(val);
            minEle=val;
        }
        else if(val>=minEle){
            s.push(val);
        }
        else{
            s.push(2*val-minEle);
            minEle=val;
        }
    }

    void pop() {
        if(s.top()>=minEle){
            s.pop();
        }
        else{
            minEle=2*minEle-s.top();
            s.pop();
        }
    }

    int top() {
        if(s.top()>=minEle){
            return s.top();
        }
        else{
            return minEle;
        }
    }

    int getMin() {
        return minEle;
    }
};
```

### 💡 **Question 8**

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

## **Solution**

```cpp
int trap(vector<int>& height) {
    int n=height.size();
    int left[n],right[n];
    left[0]=height[0];
    for(int i=1;i<n;i++){
        left[i]=max(left[i-1],height[i]);
    }
    right[n-1]=height[n-1];
    for(int i=n-2;i>=0;i--){
        right[i]=max(right[i+1],height[i]);
    }
    int ans=0;
    for(int i=0;i<n;i++){
        ans+=min(left[i],right[i])-height[i];
    }
    return ans;
}
```
