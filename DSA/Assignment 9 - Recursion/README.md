# **Assignment 9 - Recursion**

### 💡 **Question 1**

Given an integer `n`, return *`true` if it is a power of two. Otherwise, return `false`*.

An integer `n` is a power of two, if there exists an integer `x` such that `n == 2x`.

**Example 1:**
Input: n = 1

Output: true

**Example 2:**
Input: n = 16

Output: true

**Example 3:**
Input: n = 3

Output: false

## Solution

```javascript
var isPowerOfTwo = function (n) {
	if (n == 1) return true;
	if (n % 2 != 0 || n == 0) return false;
	return isPowerOfTwo(n / 2);
};
```

### 💡 **Question 2**

Given a number n, find the sum of the first natural numbers.

**Example 1:**

Input: n = 3

Output: 6

**Example 2:**

Input : 5

Output : 15

## Solution

```javascript
function sum(n) {
	if (n == 1) return 1;
	return n + sum(n - 1);
}
```

### 💡 **Question 3**

Given a positive integer, N. Find the factorial of N.

**Example 1:**

Input: N = 5

Output: 120

**Example 2:**

Input: N = 4

Output: 24

## Solution

```javascript
function factorial(n) {
	if (n == 1 || n == 0) return 1;
	return n * factorial(n - 1);
}
```

### 💡 **Question 4**

Given a number N and a power P, the task is to find the exponent of this number raised to the given power, i.e. N^P.

**Example 1 :**

Input: N = 5, P = 2

Output: 25

**Example 2 :**
Input: N = 2, P = 5

Output: 32

## Solution

```javascript
function power(n, p) {
	if (p == 0) return 1;
	return n * power(n, p - 1);
}
```

### 💡 **Question 5**

Given an array of integers **arr**, the task is to find maximum element of that array using recursion.

**Example 1:**

Input: arr = {1, 4, 3, -5, -4, 8, 6};
Output: 8

**Example 2:**

Input: arr = {1, 4, 45, 6, 10, -8};
Output: 45

## Solution

```javascript
function max(arr, n) {
	if (n == 1) return arr[0];
	return Math.max(arr[n - 1], max(arr, n - 1));
}
```

### 💡 **Question 6**

Given first term (a), common difference (d) and a integer N of the Arithmetic Progression series, the task is to find Nth term of the series.

**Example 1:**

Input : a = 2 d = 1 N = 5
Output : 6
The 5th term of the series is : 6

**Example 2:**

Input : a = 5 d = 2 N = 10
Output : 23
The 10th term of the series is : 23

## Solution

```javascript
function nthTerm(a, d, n) {
	if (n == 1) return a;
	return d + nthTerm(a, d, n - 1);
}
```

### 💡 **Question 7**

Given a string S, the task is to write a program to print all permutations of a given string.

**Example 1:**

**_Input:_**

_S = “ABC”_

**_Output:_**

_“ABC”, “ACB”, “BAC”, “BCA”, “CBA”, “CAB”_

**Example 2:**

**_Input:_**

_S = “XY”_

**_Output:_**

_“XY”, “YX”_

## Solution

```javascript
function swap(str, i, j) {
	let temp = str[i];
	str[i] = str[j];
	str[j] = temp;
}

function permute(str, l, r) {
	if (l == r) console.log(str.join(""));
	else {
		for (let i = l; i <= r; i++) {
			swap(str, l, i);
			permute(str, l + 1, r);
			swap(str, l, i);
		}
	}
}

function main() {
	let str = "ABC";
	let n = str.length;
	let arr = str.split("");
	permute(arr, 0, n - 1);
}
```

### 💡 **Question 8**

Given an array, find a product of all array elements.

**Example 1:**

Input : arr[] = {1, 2, 3, 4, 5}
Output : 120
**Example 2:**

Input : arr[] = {1, 6, 3}
Output : 18

## Solution

```javascript
function product(arr, n) {
	if (n == 1) return arr[0];
	return arr[n - 1] * product(arr, n - 1);
}
```
