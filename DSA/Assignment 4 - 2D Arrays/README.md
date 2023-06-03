# **Assignment 4 - 2D Arrays**

### **Question 1**

Given three integer arrays arr1, arr2 and arr3 **sorted** in **strictly increasing** order, return a sorted array of **only** the integers that appeared in **all** three arrays.

**Example 1:**

Input: arr1 = [1,2,3,4,5], arr2 = [1,2,5,7,9], arr3 = [1,3,4,5,8]

Output: [1,5]

**Explanation:** Only 1 and 5 appeared in the three arrays.

## **Solution**

```javascript
var arraysIntersection = function (arr1, arr2, arr3) {
	let result = [];
	let i = 0;
	let j = 0;
	let k = 0;
	while (i < arr1.length && j < arr2.length && k < arr3.length) {
		if (arr1[i] === arr2[j] && arr2[j] === arr3[k]) {
			result.push(arr1[i]);
			i++;
			j++;
			k++;
		} else if (arr1[i] < arr2[j]) {
			i++;
		} else if (arr2[j] < arr3[k]) {
			j++;
		} else {
			k++;
		}
	}
	return result;
};
```

### **Question 2**

Given two **0-indexed** integer arrays nums1 and nums2, return _a list_ answer _of size_ 2 _where:_

- answer[0] _is a list of all **distinct** integers in_ nums1 _which are **not** present in_ nums2*.*
- answer[1] _is a list of all **distinct** integers in_ nums2 _which are **not** present in_ nums1.

**Note** that the integers in the lists may be returned in **any** order.

**Example 1:**

**Input:** nums1 = [1,2,3], nums2 = [2,4,6]

**Output:** [[1,3],[4,6]]

**Explanation:**

For nums1, nums1[1] = 2 is present at index 0 of nums2, whereas nums1[0] = 1 and nums1[2] = 3 are not present in nums2. Therefore, answer[0] = [1,3].

For nums2, nums2[0] = 2 is present at index 1 of nums1, whereas nums2[1] = 4 and nums2[2] = 6 are not present in nums2. Therefore, answer[1] = [4,6].

## **Solution**

```javascript
var findDisappearedNumbers = function (nums) {
	let result = [];
	let i = 0;
	while (i < nums.length) {
		let j = nums[i] - 1;
		if (nums[i] !== nums[j]) {
			[nums[i], nums[j]] = [nums[j], nums[i]];
		} else {
			i++;
		}
	}
	for (let i = 0; i < nums.length; i++) {
		if (nums[i] !== i + 1) {
			result.push(i + 1);
		}
	}
	return result;
};
```

### **Question 3**

Given a 2D integer array matrix, return _the **transpose** of_ matrix.

The **transpose** of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

**Example 1:**

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]

Output: [[1,4,7],[2,5,8],[3,6,9]]

## **Solution**

```javascript
var transpose = function (matrix) {
	let result = [];
	for (let i = 0; i < matrix[0].length; i++) {
		let temp = [];
		for (let j = 0; j < matrix.length; j++) {
			temp.push(matrix[j][i]);
		}
		result.push(temp);
	}
	return result;
};
```

### **Question 4**

Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is **maximized**. Return _the maximized sum_.

**Example 1:**

Input: nums = [1,4,3,2]

Output: 4

**Explanation:** All possible pairings (ignoring the ordering of elements) are:

1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3

2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3

3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4

So the maximum possible sum is 4.

## **Solution**

```javascript
var arrayPairSum = function (nums) {
	nums.sort((a, b) => a - b);
	let result = 0;
	for (let i = 0; i < nums.length; i += 2) {
		result += nums[i];
	}
	return result;
};
```

### **Question 5**

You have n coins and you want to build a staircase with these coins. The staircase consists of k rows where the ith row has exactly i coins. The last row of the staircase **may be** incomplete.

Given the integer n, return _the number of **complete rows** of the staircase you will build_.

## **Solution**

```javascript
var arrangeCoins = function (n) {
	let i = 1;
	while (n >= i) {
		n -= i;
		i++;
	}
	return i - 1;
};
```

### **Question 6**

Given an integer array nums sorted in **non-decreasing** order, return _an array of **the squares of each number** sorted in non-decreasing order_.

**Example 1:**

Input: nums = [-4,-1,0,3,10]

Output: [0,1,9,16,100]

**Explanation:** After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100]

## **Solution**

```javascript
var sortedSquares = function (nums) {
	let result = [];
	let i = 0;
	let j = nums.length - 1;
	let k = nums.length - 1;
	while (i <= j) {
		if (nums[i] ** 2 > nums[j] ** 2) {
			result[k] = nums[i] ** 2;
			i++;
		} else {
			result[k] = nums[j] ** 2;
			j--;
		}
		k--;
	}
	return result;
};
```

### **Question 7**

You are given an m x n matrix M initialized with all 0's and an array of operations ops, where ops[i] = [ai, bi] means M[x][y] should be incremented by one for all 0 <= x < ai and 0 <= y < bi.

Count and return _the number of maximum integers in the matrix after performing all the operations_

## Solution

```javascript
var maxCount = function (m, n, ops) {
	let minRow = m;
	let minCol = n;
	for (let i = 0; i < ops.length; i++) {
		minRow = Math.min(minRow, ops[i][0]);
		minCol = Math.min(minCol, ops[i][1]);
	}
	return minRow * minCol;
};
```

### **Question 8**

Given the array nums consisting of 2n elements in the form [x1,x2,...,xn,y1,y2,...,yn].

_Return the array in the form_ [x1,y1,x2,y2,...,xn,yn].

**Example 1:**

**Input:** nums = [2,5,1,3,4,7], n = 3

**Output:** [2,3,5,4,1,7]

**Explanation:** Since x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 then the answer is [2,3,5,4,1,7].

## **Solution**

```javascript
var shuffle = function (nums, n) {
	let result = [];
	for (let i = 0; i < n; i++) {
		result.push(nums[i]);
		result.push(nums[i + n]);
	}
	return result;
};
```
