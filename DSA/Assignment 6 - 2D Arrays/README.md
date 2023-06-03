# **Assignment 6 - 2D Arrays**

**Question 1**

A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where:

- s[i] == 'I' if perm[i] < perm[i + 1], and
- s[i] == 'D' if perm[i] > perm[i + 1].

Given a string s, reconstruct the permutation perm and return it. If there are multiple valid permutations perm, return **any of them**.

**Example 1:**

**Input:** s = "IDID"

**Output:**

[0,4,1,3,2]

## **Solution**

```javascript
var diStringMatch = function (s) {
	let arr = [];
	let min = 0;
	let max = s.length;
	for (let i = 0; i < s.length; i++) {
		if (s[i] === "I") {
			arr.push(min);
			min++;
		} else {
			arr.push(max);
			max--;
		}
	}
	arr.push(min);
	return arr;
};
```

**Question 2**
You are given an m x n integer matrix matrix with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer target, return true _if_ target _is in_ matrix _or_ false _otherwise_.

You must write a solution in O(log(m \* n)) time complexity.

Example 1:
**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3

**Output:** true

## **Solution**

```javascript
var searchMatrix = function (matrix, target) {
	let row = matrix.length;
	let col = matrix[0].length;
	let start = 0;
	let end = row * col - 1;
	while (start <= end) {
		let mid = Math.floor((start + end) / 2);
		let midElement = matrix[Math.floor(mid / col)][mid % col];
		if (midElement === target) {
			return true;
		} else if (midElement < target) {
			start = mid + 1;
		} else {
			end = mid - 1;
		}
	}
	return false;
};
```

**Question 3**
Given an array of integers arr, return _true if and only if it is a valid mountain array_.

Recall that arr is a mountain array if and only if:

- arr.length >= 3
- There exists some i with 0 < i < arr.length - 1 such that:
  - arr[0] < arr[1] < ... < arr[i - 1] < arr[i]
  - arr[i] > arr[i + 1] > ... > arr[arr.length - 1]

**Example 1:**

**Input:** arr = [2,1]

**Output:**

false

## **Solution**

```javascript
var validMountainArray = function (arr) {
	let i = 0;
	let j = arr.length - 1;
	while (i < j) {
		if (arr[i] < arr[i + 1]) {
			i++;
		} else if (arr[j] < arr[j - 1]) {
			j--;
		} else {
			break;
		}
	}
	return i === j && i !== 0 && j !== arr.length - 1;
};
```

**Question 4**
Given a binary array nums, return _the maximum length of a contiguous subarray with an equal number of_ 0 _and_ 1.

**Example 1:**

**Input:** nums = [0,1]

**Output:** 2

**Explanation:**

[0, 1] is the longest contiguous subarray with an equal number of 0 and 1.

## **Solution**

```javascript
var findMaxLength = function (nums) {
	let map = new Map();
	map.set(0, -1);
	let count = 0;
	let max = 0;
	for (let i = 0; i < nums.length; i++) {
		if (nums[i] === 0) {
			count--;
		} else {
			count++;
		}
		if (map.has(count)) {
			max = Math.max(max, i - map.get(count));
		} else {
			map.set(count, i);
		}
	}
	return max;
};
```

**Question 5**
The **product sum** of two equal-length arrays a and b is equal to the sum of a[i] \* b[i] for all 0 <= i < a.length (**0-indexed**).

- For example, if a = [1,2,3,4] and b = [5,2,3,1], the **product sum** would be 1*5 + 2*2 + 3*3 + 4*1 = 22.

Given two arrays nums1 and nums2 of length n, return _the **minimum product sum** if you are allowed to **rearrange** the **order** of the elements in_ nums1.

**Example 1:**

**Input:** nums1 = [5,3,4,2], nums2 = [4,2,2,5]

**Output:** 40

**Explanation:**

We can rearrange nums1 to become [3,5,4,2]. The product sum of [3,5,4,2] and [4,2,2,5] is 3*4 + 5*2 + 4*2 + 2*5 = 40.

## **Solution**

```javascript
var minProductSum = function (nums1, nums2) {
	nums1.sort((a, b) => a - b);
	nums2.sort((a, b) => b - a);
	let sum = 0;
	for (let i = 0; i < nums1.length; i++) {
		sum += nums1[i] * nums2[i];
	}
	return sum;
};
```

**Question 6**
An integer array original is transformed into a **doubled** array changed by appending **twice the value** of every element in original, and then randomly **shuffling** the resulting array.

Given an array changed, return original _if_ changed _is a **doubled** array. If_ changed _is not a **doubled** array, return an empty array. The elements in_ original _may be returned in **any** order_.

**Example 1:**

**Input:** changed = [1,3,4,2,6,8]

**Output:** [1,3,4]

**Explanation:** One possible original array could be [1,3,4]:

- Twice the value of 1 is 1 \* 2 = 2.
- Twice the value of 3 is 3 \* 2 = 6.
- Twice the value of 4 is 4 \* 2 = 8.

Other original arrays could be [4,3,1] or [3,1,4].

## **Solution**

```javascript
var findOriginalArray = function (changed) {
	if (changed.length % 2 !== 0) {
		return [];
	}
	let map = new Map();
	let arr = [];
	changed.sort((a, b) => a - b);
	for (let i = 0; i < changed.length; i++) {
		map.set(changed[i], map.get(changed[i]) + 1 || 1);
	}
	for (let i = 0; i < changed.length; i++) {
		if (map.get(changed[i]) > 0) {
			if (map.get(changed[i] * 2) > 0) {
				arr.push(changed[i]);
				map.set(changed[i], map.get(changed[i]) - 1);
				map.set(changed[i] * 2, map.get(changed[i] * 2) - 1);
			} else {
				return [];
			}
		}
	}
	return arr;
};
```

**Question 7**
Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

**Example 1:**

**Input:** n = 3

**Output:** [[1,2,3],[8,9,4],[7,6,5]]

## **Solution**

```javascript
var generateMatrix = function (n) {
	let matrix = new Array(n).fill(0).map(() => new Array(n).fill(0));
	let top = 0;
	let bottom = n - 1;
	let left = 0;
	let right = n - 1;
	let num = 1;
	while (top <= bottom && left <= right) {
		for (let i = left; i <= right; i++) {
			matrix[top][i] = num;
			num++;
		}
		top++;
		for (let i = top; i <= bottom; i++) {
			matrix[i][right] = num;
			num++;
		}
		right--;
		for (let i = right; i >= left; i--) {
			matrix[bottom][i] = num;
			num++;
		}
		bottom--;
		for (let i = bottom; i >= top; i--) {
			matrix[i][left] = num;
			num++;
		}
		left++;
	}
	return matrix;
};
```

**Question 8**
Given two [sparse matrices](https://en.wikipedia.org/wiki/Sparse_matrix) mat1 of size m x k and mat2 of size k x n, return the result of mat1 x mat2. You may assume that multiplication is always possible.

**Example 1:**

**Input:** mat1 = [[1,0,0],[-1,0,3]], mat2 = [[7,0,0],[0,0,0],[0,0,1]]

**Output:**

[[7,0,0],[-7,0,3]]

## **Solution**

```javascript
var multiply = function (mat1, mat2) {
	let m = mat1.length;
	let n = mat2[0].length;
	let k = mat1[0].length;
	let result = new Array(m).fill(0).map(() => new Array(n).fill(0));
	for (let i = 0; i < m; i++) {
		for (let j = 0; j < n; j++) {
			for (let l = 0; l < k; l++) {
				result[i][j] += mat1[i][l] * mat2[l][j];
			}
		}
	}
	return result;
};
```
