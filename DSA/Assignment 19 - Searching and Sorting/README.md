# **Assignment 19 - Searching and Sorting**

### 💡 **Question 1**

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

_Merge all the linked-lists into one sorted linked-list and return it._

**Example 1:**Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
1->4->5,
1->3->4,
2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6

**Example 2:**
Input: lists = []
Output: []

**Example 3:**
Input: lists = [[]]
Output: []

## **Solution**

```cpp
class Solution {
public:
  ListNode* mergeKLists(vector<ListNode*>& lists) {
    ListNode* head = NULL;
    ListNode* tail = NULL;
    priority_queue<pair<int, ListNode*>, vector<pair<int, ListNode*>>, greater<pair<int, ListNode*>>> pq;
    for(int i=0; i<lists.size(); i++){
        if(lists[i] != NULL){
            pq.push({lists[i]->val, lists[i]});
        }
    }
    while(!pq.empty()){
        pair<int, ListNode*> p = pq.top();
        pq.pop();
        if(p.second->next != NULL){
            pq.push({p.second->next->val, p.second->next});
        }
        if(head == NULL){
            head = p.second;
            tail = p.second;
        }
        else{
            tail->next = p.second;
            tail = tail->next;
        }
    }
    return head;
  }
};
```

### 💡 **Question 2**

Given an integer array `nums`, return *an integer array* `counts` *where* `counts[i]` *is the number of smaller elements to the right of* `nums[i]`.

**Example 1:**
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are2 smaller elements (2 and 1).
To the right of 2 there is only1 smaller element (1).
To the right of 6 there is1 smaller element (1).
To the right of 1 there is0 smaller element.

**Example 2:**
Input: nums = [-1]
Output: [0]

**Example 3:**
Input: nums = [-1,-1]
Output: [0,0]

## **Solution**

```cpp
class Solution {
public:
  vector<int> countSmaller(vector<int>& nums) {
    vector<int> ans(nums.size());
    vector<pair<int, int>> v;
    for(int i=0; i<nums.size(); i++){
        v.push_back({nums[i], i});
    }
    mergeSort(v, 0, nums.size()-1, ans);
    return ans;
  }
  void mergeSort(vector<pair<int, int>>& v, int l, int r, vector<int>& ans){
    if(l >= r){
        return;
    }
    int mid = (l+r)/2;
    mergeSort(v, l, mid, ans);
    mergeSort(v, mid+1, r, ans);
    merge(v, l, mid, r, ans);
  }
  void merge(vector<pair<int, int>>& v, int l, int mid, int r, vector<int>& ans){
    int i = l;
    int j = mid+1;
    int k = 0;
    vector<pair<int, int>> temp(r-l+1);
    while(i <= mid && j <= r){
        if(v[i].first <= v[j].first){
            ans[v[i].second] += j-mid-1;
            temp[k++] = v[i++];
        }
        else{
            temp[k++] = v[j++];
        }
    }
    while(i <= mid){
        ans[v[i].second] += j-mid-1;
        temp[k++] = v[i++];
    }
    while(j <= r){
        temp[k++] = v[j++];
    }
    for(int i=l; i<=r; i++){
        v[i] = temp[i-l];
    }
  }
};
```

### 💡 **Question 3**

Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in** functions in `O(nlog(n))` time complexity and with the smallest space complexity possible.

**Example 1:**
Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).

**Example 2:**
Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
Explanation: Note that the values of nums are not necessairly unique.

## **Solution**

```cpp
class Solution {
public:
  void mergeSort(vector<int>& nums, int l, int r){
    if(l >= r){
        return;
    }
    int mid = (l+r)/2;
    mergeSort(nums, l, mid);
    mergeSort(nums, mid+1, r);
    merge(nums, l, mid, r);
  }
  void merge(vector<int>& nums, int l, int mid, int r){
    int i = l;
    int j = mid+1;
    int k = 0;
    vector<int> temp(r-l+1);
    while(i <= mid && j <= r){
        if(nums[i] <= nums[j]){
            temp[k++] = nums[i++];
        }
        else{
            temp[k++] = nums[j++];
        }
    }
    while(i <= mid){
        temp[k++] = nums[i++];
    }
    while(j <= r){
        temp[k++] = nums[j++];
    }
    for(int i=l; i<=r; i++){
        nums[i] = temp[i-l];
    }
  }
  vector<int> sortArray(vector<int>& nums) {
    mergeSort(nums, 0, nums.size()-1);
    return nums;
  }
};
```

### 💡 **Question 4**

Given an array of random numbers, Push all the zero’s of a given array to the end of the array. For example, if the given arrays is {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0}, it should be changed to {1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0}. The order of all other elements should be same. Expected time complexity is O(n) and extra space is O(1).

**Example:**
Input : arr[] = {1, 2, 0, 4, 3, 0, 5, 0};
Output : arr[] = {1, 2, 4, 3, 5, 0, 0, 0};

Input : arr[] = {1, 2, 0, 0, 0, 3, 6};
Output : arr[] = {1, 2, 3, 6, 0, 0, 0};

## **Solution**

```cpp
void pushZerosToEnd(int arr[], int n) {
    int count = 0;
    for(int i=0; i<n; i++){
        if(arr[i] != 0){
            arr[count++] = arr[i];
        }
    }
    while(count < n){
        arr[count++] = 0;
    }
}
```

### 💡 **Question 5**

Given an **array of positive** and **negative numbers**, arrange them in an **alternate** fashion such that every positive number is followed by a negative and vice-versa maintaining the **order of appearance**. The number of positive and negative numbers need not be equal. If there are more positive numbers they appear at the end of the array. If there are more negative numbers, they too appear at the end of the array.

**Examples:**

> Input:  arr[] = {1, 2, 3, -4, -1, 4}
> Output: arr[] = {-4, 1, -1, 2, 3, 4}

Input:  arr[] = {-5, -2, 5, 2, 4, 7, 1, 8, 0, -8}
Output: arr[] = {-5, 5, -2, 2, -8, 4, 7, 1, 8, 0}

## **Solution**

```cpp
void rearrange(int arr[], int n) {
  int i = 0;
  int j = n-1;
  while(i < j){
      while(i < n && arr[i] > 0){
          i++;
      }
      while(j >= 0 && arr[j] < 0){
          j--;
      }
      if(i < j){
          swap(arr[i], arr[j]);
      }
  }
  if(i == 0 || i == n){
      return;
  }
  int k = 0;
  while(k < n && i < n){
      swap(arr[k], arr[i]);
      k += 2;
      i++;
  }
}
```

### 💡 **Question 6**

Given two sorted arrays, the task is to merge them in a sorted manner.

**Examples:**

> Input: arr1[] = { 1, 3, 4, 5}, arr2[] = {2, 4, 6, 8} 
> Output: arr3[] = {1, 2, 3, 4, 4, 5, 6, 8}

Input: arr1[] = { 5, 8, 9}, arr2[] = {4, 7, 8}
Output: arr3[] = {4, 5, 7, 8, 8, 9}

## **Solution**

```cpp
void merge(int arr1[], int arr2[], int n, int m) {
  int i = 0;
  int j = 0;
  while(i < n && j < m){
      if(arr1[i] <= arr2[j]){
          cout<<arr1[i++]<<" ";
      }
      else{
          cout<<arr2[j++]<<" ";
      }
  }
  while(i < n){
      cout<<arr1[i++]<<" ";
  }
  while(j < m){
      cout<<arr2[j++]<<" ";
  }
}
```

### 💡 **Question 7**

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must be **unique** and you may return the result in **any order**.

**Example 1:**
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

**Example 2:**
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
Explanation: [4,9] is also accepted.

## **Solution**

```cpp
class Solution {
public:
  vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    unordered_set<int> s;
    for(int i=0; i<nums1.size(); i++){
        s.insert(nums1[i]);
    }
    vector<int> ans;
    for(int i=0; i<nums2.size(); i++){
        if(s.find(nums2[i]) != s.end()){
            ans.push_back(nums2[i]);
            s.erase(nums2[i]);
        }
    }
    return ans;
  }
};
```

### 💡 **Question 8**

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must appear as many times as it shows in both arrays and you may return the result in **any order**.

**Example 1:**
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]

**Example 2:**
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.

## **Solution**

```cpp
class Solution {
public:
  vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
    unordered_map<int, int> m;
    for(int i=0; i<nums1.size(); i++){
        m[nums1[i]]++;
    }
    vector<int> ans;
    for(int i=0; i<nums2.size(); i++){
        if(m.find(nums2[i]) != m.end() && m[nums2[i]] > 0){
            ans.push_back(nums2[i]);
            m[nums2[i]]--;
        }
    }
    return ans;
  }
};
```
