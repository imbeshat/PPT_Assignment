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

## Solution

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
