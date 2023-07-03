# **Assignment 24 - Basics of DSA**

### 💡 **Question 1**

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
SymbolValue
I 1
V 5
X 10
L 50
C 100
D 500
M 1000
For example, `2` is written as `II` in Roman numeral, just two ones added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9.
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90.
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

**Example 1:**
Input: s = "III"
Output: 3
Explanation: III = 3.

**Example 2:**
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.

## **Solution**

```cpp
int romanToInt(string s) {
  int ans = 0;
  for(int i = 0; i < s.length(); i++){
    if(s[i] == 'I'){
        if(s[i+1] == 'V'){
          ans += 4;
          i++;
        }
        else if(s[i+1] == 'X'){
          ans += 9;
            i++;
        }
        else{
          ans += 1;
        }
    }
    else if(s[i] == 'X'){
      if(s[i+1] == 'L'){
        ans += 40;
        i++;
      }
      else if(s[i+1] == 'C'){
        ans += 90;
        i++;
      }
      else{
        ans += 10;
      }
    }
    else if(s[i] == 'C'){
      if(s[i+1] == 'D'){
        ans += 400;
        i++;
      }
      else if(s[i+1] == 'M'){
        ans += 900;
        i++;
      }
      else{
        ans += 100;
      }
    }
    else if(s[i] == 'V'){
      ans += 5;
    }
    else if(s[i] == 'L'){
      ans += 50;
    }
    else if(s[i] == 'D'){
      ans += 500;
    }
    else if(s[i] == 'M'){
      ans += 1000;
    }
  }
  return ans;
}
```

### 💡 **Question 2**

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

**Example 2:**
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

**Example 3:**
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

## **Solution**

```cpp
int lengthOfLongestSubstring(string s) {
  int n = s.length();
  int ans = 0;
  int i = 0, j = 0;
  unordered_map<char, int> mp;
  while(j < n){
    mp[s[j]]++;
    if(mp.size() == j-i+1){
      ans = max(ans, j-i+1);
      j++;
    }
    else if(mp.size() < j-i+1){
      while(mp.size() < j-i+1){
        mp[s[i]]--;
        if(mp[s[i]] == 0){
          mp.erase(s[i]);
        }
        i++;
      }
      j++;
    }
  }
  return ans;
}
```

### 💡 **Question 3**

Given an array `nums` of size `n`, return *the majority element*.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**
Input: nums = [3,2,3]
Output: 3

**Example 2:**
Input: nums = [2,2,1,1,1,2,2]
Output: 2

## **Solution**

```cpp
int majorityElement(vector<int>& nums) {
  int n = nums.size();
  int ans = nums[0];
  int count = 1;
  for(int i = 1; i < n; i++){
    if(nums[i] == ans){
      count++;
    }
    else{
      count--;
    }
    if(count == 0){
      ans = nums[i];
      count = 1;
    }
  }
  return ans;
}
```

### 💡 **Question 4**

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

**Example 2:**
Input: strs = [""]
Output: [[""]]

**Example 3:**
Input: strs = ["a"]
Output: [["a"]]

## **Solution**

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
  unordered_map<string, vector<string>> mp;
  for(int i = 0; i < strs.size(); i++){
    string temp = strs[i];
    sort(temp.begin(), temp.end());
    mp[temp].push_back(strs[i]);
  }
  vector<vector<string>> ans;
  for(auto it = mp.begin(); it != mp.end(); it++){
    ans.push_back(it->second);
  }
  return ans;
}
```

### 💡 **Question 5**

An **ugly number** is a positive integer whose prime factors are limited to `2`, `3`, and `5`.

Given an integer `n`, return *the* `nth` **_ugly number_**.

**Example 1:**
Input: n = 10
Output: 12
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.

**Example 2:**
Input: n = 1
Output: 1
Explanation: 1 has no prime factors, therefore all of its prime factors are limited to 2, 3, and 5.

## **Solution**

```cpp
int nthUglyNumber(int n) {
  int ugly[n];
  ugly[0] = 1;
  int i2 = 0, i3 = 0, i5 = 0;
  int next_multiple_of_2 = 2;
  int next_multiple_of_3 = 3;
  int next_multiple_of_5 = 5;
  int next_ugly_no = 1;
  for(int i = 1; i < n; i++){
    next_ugly_no = min(next_multiple_of_2, min(next_multiple_of_3, next_multiple_of_5));
    ugly[i] = next_ugly_no;
    if(next_ugly_no == next_multiple_of_2){
      i2++;
      next_multiple_of_2 = ugly[i2] * 2;
    }
    if(next_ugly_no == next_multiple_of_3){
      i3++;
      next_multiple_of_3 = ugly[i3] * 3;
    }
    if(next_ugly_no == next_multiple_of_5){
      i5++;
      next_multiple_of_5 = ugly[i5] * 5;
    }
  }
  return next_ugly_no;
}
```

### 💡 **Question 6**

Given an array of strings `words` and an integer `k`, return *the* `k` *most frequent strings*.

Return the answer **sorted** by **the frequency** from highest to lowest. Sort the words with the same frequency by their **lexicographical order**.

**Example 1:**
Input: words = ["i","love","leetcode","i","love","coding"], k = 2
Output: ["i","love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.

**Example 2:**
Input: words = ["the","day","is","sunny","the","the","the","sunny","is","is"], k = 4
Output: ["the","is","sunny","day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words, with the number of occurrence being 4, 3, 2 and 1 respectively.

## **Solution**

```cpp
vector<string> topKFrequent(vector<string>& words, int k) {
  unordered_map<string, int> mp;
  for(int i = 0; i < words.size(); i++){
    mp[words[i]]++;
  }
  priority_queue<pair<int, string>> pq;
  for(auto it = mp.begin(); it != mp.end(); it++){
    pq.push({it->second, it->first});
  }
  vector<string> ans;
  while(k--){
    ans.push_back(pq.top().second);
    pq.pop();
  }
  return ans;
}
```

### 💡 **Question 7**

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return *the max sliding window*.

**Example 1:**
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation:
Window position Max

---

[1 3 -1] -3 5 3 6 7 3
1 [3 -1 -3] 5 3 6 7 3
1 3 [-1 -3 5] 3 6 7 5
1 3 -1 [-3 5 3] 6 7 5
1 3 -1 -3 [5 3 6]7 6
1 3 -1 -3 5 [3 6 7] 7

**Example 2:**
Input: nums = [1], k = 1
Output: [1]

## **Solution**

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
  int n = nums.size();
  vector<int> ans;
  deque<int> dq;
  for(int i = 0; i < k; i++){
    while(!dq.empty() && nums[dq.back()] <= nums[i]){
      dq.pop_back();
    }
    dq.push_back(i);
  }
  ans.push_back(nums[dq.front()]);
  for(int i = k; i < n; i++){
    while(!dq.empty() && dq.front() <= i-k){
      dq.pop_front();
    }
    while(!dq.empty() && nums[dq.back()] <= nums[i]){
      dq.pop_back();
    }
    dq.push_back(i);
    ans.push_back(nums[dq.front()]);
  }
  return ans;
}
```

### 💡 **Question 8**

Given a **sorted** integer array `arr`, two integers `k` and `x`, return the `k` closest integers to `x` in the array. The result should also be sorted in ascending order.

An integer `a` is closer to `x` than an integer `b` if:

- `|a - x| < |b - x|`, or
- `|a - x| == |b - x|` and `a < b`

**Example 1:**
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]

**Example 2:**
Input: arr = [1,2,3,4,5], k = 4, x = -1
Output: [1,2,3,4]

## **Solution**

```cpp
vector<int> findClosestElements(vector<int>& arr, int k, int x) {
  int n = arr.size();
  int low = 0, high = n-1;
  while(high-low >= k){
    if(abs(arr[low]-x) > abs(arr[high]-x)){
      low++;
    }
    else{
      high--;
    }
  }
  vector<int> ans;
  for(int i = low; i <= high; i++){
    ans.push_back(arr[i]);
  }
  return ans;
}
```
