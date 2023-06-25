# **Assignment 18 - Searching and Sorting**

### 💡 **Question 1**

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

**Example 1:**
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

**Example 2:**
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.

**Constraints:**

- `1 <= intervals.length <= 10000`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 10000`

## **Solution**

```cpp
class Solution {
public:
  vector<vector<int>> merge(vector<vector<int>>& intervals) {
    vector<vector<int>> ans;
    sort(intervals.begin(), intervals.end());
    int start = intervals[0][0];
    int end = intervals[0][1];
    for(int i = 1; i < intervals.size(); i++) {
        if(intervals[i][0] <= end) {
            end = max(end, intervals[i][1]);
        } else {
            ans.push_back({start, end});
            start = intervals[i][0];
            end = intervals[i][1];
        }
    }
    ans.push_back({start, end});
    return ans;
  }
};
```

### 💡 **Question 2**

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

**Example 1:**
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]

**Example 2:**
Input: nums = [2,0,1]
Output: [0,1,2]

**Constraints:**

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` is either `0`, `1`, or `2`.

## **Solution**

```cpp
class Solution {
public:
  void sortColors(vector<int>& nums) {
    int low = 0, mid = 0, high = nums.size() - 1;
    while(mid <= high) {
        if(nums[mid] == 0) {
            swap(nums[low], nums[mid]);
            low++;
            mid++;
        } else if(nums[mid] == 1) {
            mid++;
        } else {
            swap(nums[mid], nums[high]);
            high--;
        }
    }
  }
};
```

### 💡 **Question 3**

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example 1:**
Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.

**Example 2:**
Input: n = 1, bad = 1
Output: 1

**Constraints:**

- `1 <= bad <= n <= 2^31 - 1`

## **Solution**

```cpp
// The API isBadVersion is defined for you.
// bool isBadVersion(int version);
class Solution{
  public:
    int firstBadVersion(int n) {
        int low = 1, high = n;
        while(low < high) {
            int mid = low + (high - low) / 2;
            if(isBadVersion(mid)) {
                high = mid;
            } else {
                low = mid + 1;
            }
        }
        return low;
    }
}
```

### 💡 **Question 4**

Given an integer array `nums`, return *the maximum difference between two successive elements in its sorted form*. If the array contains less than two elements, return `0`.

You must write an algorithm that runs in linear time and uses linear extra space.

**Example 1:**
Input: nums = [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either (3,6) or (6,9) has the maximum difference 3.

**Example 2:**
Input: nums = [10]
Output: 0
Explanation: The array contains less than 2 elements, therefore return 0.

**Constraints:**

- `1 <= nums.length <= 10^5`
- `0 <= nums[i] <= 10^9`

## **Solution**

```cpp
class Solution {
public:
  int maximumGap(vector<int>& nums) {
    int n = nums.size();
    if(n < 2) return 0;
    int maxNum = *max_element(nums.begin(), nums.end());
    int minNum = *min_element(nums.begin(), nums.end());
    int bucketSize = max(1, (maxNum - minNum) / (n - 1));
    int bucketNum = (maxNum - minNum) / bucketSize + 1;
    vector<int> bucketMin(bucketNum, INT_MAX);
    vector<int> bucketMax(bucketNum, INT_MIN);
    for(int i = 0; i < n; i++) {
        int bucketIdx = (nums[i] - minNum) / bucketSize;
        bucketMin[bucketIdx] = min(bucketMin[bucketIdx], nums[i]);
        bucketMax[bucketIdx] = max(bucketMax[bucketIdx], nums[i]);
    }
    int ans = 0;
    int prev = minNum;
    for(int i = 0; i < bucketNum; i++) {
        if(bucketMin[i] == INT_MAX && bucketMax[i] == INT_MIN) continue;
        ans = max(ans, bucketMin[i] - prev);
        prev = bucketMax[i];
    }
    return ans;
  }
};
```

### 💡 **Question 5**

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

**Example 1:**
Input: nums = [1,2,3,1]
Output: true

**Example 2:**
Input: nums = [1,2,3,4]
Output: false

**Example 3:**
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true

**Constraints:**

- `1 <= nums.length <= 10^5`
- `109 <= nums[i] <= 10^9`

## **Solution**

```cpp
class Solution {
public:
  bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> s;
    for(int i = 0; i < nums.size(); i++) {
        if(s.find(nums[i]) != s.end()) return true;
        s.insert(nums[i]);
    }
    return false;
  }
};
```

### 💡 **Question 6**

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose **horizontal diameter** stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up **directly vertically** (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is **burst** by an arrow shot at `x` if `xstart <= x <= xend`. There is **no limit** to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return *the **minimum** number of arrows that must be shot to burst all balloons*.

**Example 1:**
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:

- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].

**Example 2:**
Input: points = [[1,2],[3,4],[5,6],[7,8]]
Output: 4
Explanation: One arrow needs to be shot for each balloon for a total of 4 arrows.

**Example 3:**
Input: points = [[1,2],[2,3],[3,4],[4,5]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:

- Shoot an arrow at x = 2, bursting the balloons [1,2] and [2,3].
- Shoot an arrow at x = 4, bursting the balloons [3,4] and [4,5].

## **Solution**

```cpp
class Solution{
  public:
  static bool comp(vector<int>& a,vector<int>& b){
    if(a[0]==b[0]) return a[1]<b[1];
    return a[0]<b[0];
  }
  int findMinArrowShots(vector<vector<int>>& points) {
    int n=points.size();
    if(n<=1) return 1;
    sort(points.begin(),points.end(),comp);
    int last=points[0][1];
    int ans=1;
    for(int i=1;i<n;i++){
        if(points[i][0]>last){
            ans++;
            last=points[i][1];
        }
        last=min(last,points[i][1]);
    }
    return ans;
  }
}
```

### 💡 **Question 7**

Given an integer array `nums`, return \*the length of the longest **strictly increasing\***

**_subsequence_**

**Example 1:**
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**
Input: nums = [0,1,0,3,2,3]
Output: 4

**Example 3:**
Input: nums = [7,7,7,7,7,7,7]
Output: 1

**Constraints:**

- `1 <= nums.length <= 2500`
- `-10^4 <= nums[i] <= 10^4`

## **Solution**

```cpp
class Solution {
public:
  int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, 1);
    int ans = 1;
    for(int i = 1; i < n; i++) {
        for(int j = 0; j < i; j++) {
            if(nums[i] > nums[j]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
        ans = max(ans, dp[i]);
    }
    return ans;
  }
};
```

### 💡 **Question 8**

Given an array of `n` integers `nums`, a **132 pattern** is a subsequence of three integers `nums[i]`, `nums[j]` and `nums[k]` such that `i < j < k` and `nums[i] < nums[k] < nums[j]`.

Return `true` *if there is a **132 pattern** in* `nums`*, otherwise, return* `false`_._

**Example 1:**
Input: nums = [1,2,3,4]
Output: false
Explanation: There is no 132 pattern in the sequence.

**Example 2:**
Input: nums = [3,1,4,2]
Output: true
Explanation: There is a 132 pattern in the sequence: [1, 4, 2].

**Example 3:**
Input: nums = [-1,3,2,0]
Output: true
Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].

**Constraints:**

- `n == nums.length`
- `1 <= n <= 2 * 10^5`
- `-10^9 <= nums[i] <= 10^9`

## **Solution**

```cpp
class Solution {
public:
  bool find132pattern(vector<int>& nums) {
    int n = nums.size();
    if(n < 3) return false;
    vector<int> minNum(n);
    minNum[0] = nums[0];
    for(int i = 1; i < n; i++) {
        minNum[i] = min(minNum[i - 1], nums[i]);
    }
    stack<int> s;
    for(int i = n - 1; i >= 0; i--) {
        if(nums[i] > minNum[i]) {
            while(!s.empty() && s.top() <= minNum[i]) {
                s.pop();
            }
            if(!s.empty() && s.top() < nums[i]) return true;
            s.push(nums[i]);
        }
    }
    return false;
  }
};
```
