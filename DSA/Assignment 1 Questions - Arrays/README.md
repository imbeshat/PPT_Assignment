### 💡 **Q1.)**

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

**Example:**
Input: nums = [2,7,11,15], target = 9
Output [0,1]

**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1]

## **Solution:**

```javascript
var twoSum = function (nums, target) {
	let map = new Map();
	for (let i = 0; i < nums.length; i++) {
		let x = nums[i];
		let y = target - nums[i];
		if (map.has(y)) {
			return [map.get(y), i];
		}
		map.set(x, i);
	}
};
```

### 💡 **Q2.)**

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

- Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
- Return k.

**Example :**
Input: nums = [3,2,2,3], val = 3
Output: 2, nums = [2,2,_*,_*]

**Explanation:** Your function should return k = 2, with the first two elements of nums being 2. It does not matter what you leave beyond the returned k (hence they are underscores)

## **Solution:**

```javascript
var removeElement = function (nums, val) {
	let k = 0;
	for (let i = 0; i < nums.length; i++) {
		if (nums[i] != val) {
			nums[k] = nums[i];
			k++;
		}
	}
	return k;
};
```

### 💡 **Q3.)**

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with O(log n) runtime complexity.

**Example 1:**
Input: nums = [1,3,5,6], target = 5

Output: 2

### Solution:

```javascript
var searchInsert = function (nums, target) {
	let low = 0;
	let high = nums.length - 1;
	while (low <= high) {
		let mid = Math.floor((low + high) / 2);
		if (nums[mid] == target) {
			return mid;
		} else if (nums[mid] > target) {
			high = mid - 1;
		} else {
			low = mid + 1;
		}
	}
	return low;
};
```

### 💡 **Q4.**

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

**Example 1:**
Input: digits = [1,2,3]
Output: [1,2,4]

**Explanation:** The array represents the integer 123.

Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].

### Solution:

```javascript
var plusOne = function (digits) {
	let n = digits.length;
	for (let i = n - 1; i >= 0; i--) {
		if (digits[i] < 9) {
			digits[i]++;
			return digits;
		}
		digits[i] = 0;
	}
	digits.unshift(1);
	return digits;
};
```
