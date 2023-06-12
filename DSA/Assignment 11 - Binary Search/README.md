# **Assignment 11 - Binary Search**

### 💡 **Question 1**

Given a non-negative integer `x`, return *the square root of* `x` *rounded down to the nearest integer*. The returned integer should be **non-negative** as well.

You **must not use** any built-in exponent function or operator.

- For example, do not use `pow(x, 0.5)` in c++ or `x ** 0.5` in python.

**Example 1:**
Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.

**Example 2:**
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.

## **Solution**

```javascript
var mySqrt = function (x) {
	let left = 0;
	let right = x;
	let mid = 0;
	while (left <= right) {
		mid = Math.floor((left + right) / 2);
		if (mid * mid === x) {
			return mid;
		} else if (mid * mid < x) {
			left = mid + 1;
		} else {
			right = mid - 1;
		}
	}
	return right;
};
```

### 💡 **Question 2**

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

**Example 1:**
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.

**Example 2:**
Input: nums = [1,2,1,3,5,6,4]
Output: 5
Explanation: Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

## **Solution**

```javascript
var findPeakElement = function (nums) {
	let size = nums.length;
	let left = 0;
	let mid = 0;
	let right = size - 1;
	while (left < right) {
		mid = Math.floor((left + right) / 2);
		if (nums[mid] > nums[mid + 1]) right = mid;
		else left = mid + 1;
	}
	return left;
};
```

### 💡 **Question 3**

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return *the only number in the range that is missing from the array.*

**Example 1:**
Input: nums = [3,0,1]
Output: 2
Explanation: n = 3 since there are 3 numbers, so all numbers are in the range [0,3]. 2 is the missing number in the range since it does not appear in nums.

**Example 2:**
Input: nums = [0,1]
Output: 2
Explanation: n = 2 since there are 2 numbers, so all numbers are in the range [0,2]. 2 is the missing number in the range since it does not appear in nums.

**Example 3:**
Input: nums = [9,6,4,2,3,5,7,0,1]
Output: 8
Explanation: n = 9 since there are 9 numbers, so all numbers are in the range [0,9]. 8 is the missing number in the range since it does not appear in nums.

## **Solution**

```cpp
class Solution {
public:
		int missingNumber(vector<int>& nums) {
				int n = nums.size();
				int sum = 0;
				for(int i=0;i<n;i++){
						sum += nums[i];
				}
				return (n*(n+1))/2 - sum;
		}
};
```

### 💡 **Question 4**
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return *this repeated number*.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

**Example 1:**
Input: nums = [1,3,4,2,2]
Output: 2

**Example 2:**
Input: nums = [3,1,3,4,2]
Output: 3

## **Solution**
```
javascript
var findDuplicate = function(nums) {
		let slow = nums[0];
		let fast = nums[0];
		do{
				slow = nums[slow];
				fast = nums[nums[fast]];
		}while(slow != fast);
		fast = nums[0];
		while(slow != fast){
				slow = nums[slow];
				fast = nums[fast];
		}
		return slow;
};
```