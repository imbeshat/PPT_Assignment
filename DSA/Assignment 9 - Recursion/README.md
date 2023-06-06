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
