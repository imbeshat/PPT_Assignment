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

## **Solution:**

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

### 💡 **Q4.)**

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

**Example 1:**
Input: digits = [1,2,3]
Output: [1,2,4]

**Explanation:** The array represents the integer 123.

Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].

## **Solution:**

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

### 💡 **Q5.)**

You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

**Example 1:**
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]

**Explanation:** The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.

## **Solution:**

```javascript
var merge = function (nums1, m, nums2, n) {
	let i = m - 1;
	let j = n - 1;
	let k = m + n - 1;
	while (i >= 0 && j >= 0) {
		if (nums1[i] > nums2[j]) {
			nums1[k] = nums1[i];
			i--;
			k--;
		} else {
			nums1[k] = nums2[j];
			j--;
			k--;
		}
	}
	while (j >= 0) {
		nums1[k] = nums2[j];
		j--;
		k--;
	}
};
```

### 💡 **Q6.)**

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

**Example 1:**
Input: nums = [1,2,3,1]

Output: true

## **Solution:**

```javascript
var containsDuplicate = function (nums) {
	let map = new Map();
	for (let i = 0; i < nums.length; i++) {
		if (map.has(nums[i])) {
			return true;
		}
		map.set(nums[i], i);
	}
	return false;
};
```

### 💡 **Q7.)**

Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the nonzero elements.

Note that you must do this in-place without making a copy of the array.

**Example 1:**
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

## **Solution:**

```javascript
var moveZeroes = function (nums) {
	let k = 0;
	for (let i = 0; i < nums.length; i++) {
		if (nums[i] != 0) {
			nums[k] = nums[i];
			k++;
		}
	}
	for (let i = k; i < nums.length; i++) {
		nums[i] = 0;
	}
};
```

### 💡 **Q8.)**

You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.

You are given an integer array nums representing the data status of this set after the error.

Find the number that occurs twice and the number that is missing and return them in the form of an array.

**Example 1:**
Input: nums = [1,2,2,4]
Output: [2,3]

## **Solution:**

```javascript
var findErrorNums = function (nums) {
	let map = new Map();
	let ans = [];
	for (let i = 0; i < nums.length; i++) {
		if (map.has(nums[i])) {
			ans.push(nums[i]);
		} else {
			map.set(nums[i], i);
		}
	}
	for (let i = 1; i <= nums.length; i++) {
		if (!map.has(i)) {
			ans.push(i);
		}
	}
	return ans;
};
```
