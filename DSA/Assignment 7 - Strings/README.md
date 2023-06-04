# **Assignment 7 - Strings**

### 💡 **Question 1**

Given two strings s and t, _determine if they are isomorphic_.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1:**

**Input:** s = "egg", t = "add"

**Output:** true

## **Solution**

```javascript
var isIsomorphic = function (s, t) {
	if (s.length !== t.length) return false;
	let map = {};
	for (let i = 0; i < s.length; i++) {
		if (!map[s[i]]) {
			map[s[i]] = t[i];
		} else {
			if (map[s[i]] !== t[i]) return false;
		}
	}
	return true;
};
```

### 💡 **Question 2**

Given a string num which represents an integer, return true _if_ num \*is a **strobogrammatic number\***.

A **strobogrammatic number** is a number that looks the same when rotated 180 degrees (looked at upside down).

**Example 1:**

**Input:** num = "69"

**Output:**

true

## **Solution**

```javascript
var isStrobogrammatic = function (num) {
	let map = {
		0: "0",
		1: "1",
		6: "9",
		8: "8",
		9: "6",
	};
	let left = 0;
	let right = num.length - 1;
	while (left <= right) {
		if (map[num[left]] !== num[right]) return false;
		left++;
		right--;
	}
	return true;
};
```

### 💡 **Question 3**

Given two non-negative integers, num1 and num2 represented as string, return _the sum of_ num1 _and_ num2 _as a string_.

You must solve the problem without using any built-in library for handling large integers (such as BigInteger). You must also not convert the inputs to integers directly.

**Example 1:**

**Input:** num1 = "11", num2 = "123"

**Output:**

"134"

## **Solution**

```javascript
var addStrings = function (num1, num2) {
	let result = "";
	let carry = 0;
	let i = num1.length - 1;
	let j = num2.length - 1;
	while (i >= 0 || j >= 0) {
		let sum = carry;
		if (i >= 0) {
			sum += parseInt(num1[i]);
			i--;
		}
		if (j >= 0) {
			sum += parseInt(num2[j]);
			j--;
		}
		result = (sum % 10) + result;
		carry = Math.floor(sum / 10);
	}
	if (carry !== 0) result = carry + result;
	return result;
};
```

### 💡 **Question 4**

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**

**Input:** s = "Let's take LeetCode contest"

**Output:** "s'teL ekat edoCteeL tsetnoc"

## **Solution**

```javascript
var reverseWords = function (s) {
	let result = "";
	let word = "";
	for (let i = 0; i < s.length; i++) {
		if (s[i] === " ") {
			result += word + " ";
			word = "";
		} else {
			word = s[i] + word;
		}
	}
	result += word;
	return result;
};
```

### 💡 **Question 5**

Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.

If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

**Example 1:**

**Input:** s = "abcdefg", k = 2

**Output:**

"bacdfeg"

## **Solution**

```javascript
var reverseStr = function (s, k) {
	let result = "";
	let i = 0;
	while (i < s.length) {
		let j = i + k - 1;
		let word = "";
		while (j >= i) {
			if (s[j]) {
				word += s[j];
			}
			j--;
		}
		result += word;
		i += 2 * k;
		word = "";
		j = i;
		while (j < i + k) {
			if (s[j]) {
				word += s[j];
			}
			j++;
		}
		result += word;
		i += k;
	}
	return result;
};
```

### 💡 **Question 6**

Given two strings s and goal, return true _if and only if_ s _can become_ goal _after some number of **shifts** on_ s.

A **shift** on s consists of moving the leftmost character of s to the rightmost position.

- For example, if s = "abcde", then it will be "bcdea" after one shift.

**Example 1:**

**Input:** s = "abcde", goal = "cdeab"

**Output:**

true

## **Solution**

```javascript
var rotateString = function (s, goal) {
	if (s.length !== goal.length) return false;
	if (s === goal) return true;
	for (let i = 0; i < s.length; i++) {
		if (s[i] === goal[0]) {
			let temp = s.slice(i) + s.slice(0, i);
			if (temp === goal) return true;
		}
	}
	return false;
};
```

### 💡 **Question 7**

Given two strings s and t, return true _if they are equal when both are typed into empty text editors_. '#' means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

**Example 1:**

**Input:** s = "ab#c", t = "ad#c"

**Output:** true

**Explanation:**

Both s and t become "ac".

## **Solution**

```javascript
var backspaceCompare = function (s, t) {
	let i = s.length - 1;
	let j = t.length - 1;
	let skipS = 0;
	let skipT = 0;
	while (i >= 0 || j >= 0) {
		while (i >= 0) {
			if (s[i] === "#") {
				skipS++;
				i--;
			} else if (skipS > 0) {
				skipS--;
				i--;
			} else {
				break;
			}
		}
		while (j >= 0) {
			if (t[j] === "#") {
				skipT++;
				j--;
			} else if (skipT > 0) {
				skipT--;
				j--;
			} else {
				break;
			}
		}
		if (i >= 0 && j >= 0 && s[i] !== t[j]) return false;
		if (i >= 0 !== j >= 0) return false;
		i--;
		j--;
	}
	return true;
};
```

### 💡 **Question 8**

You are given an array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.

**Example 1:**
**Input:** coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]

**Output:** true

## **Solution**

```javascript
var checkStraightLine = function (coordinates) {
	let x1 = coordinates[0][0];
	let y1 = coordinates[0][1];
	let x2 = coordinates[1][0];
	let y2 = coordinates[1][1];
	for (let i = 2; i < coordinates.length; i++) {
		let x3 = coordinates[i][0];
		let y3 = coordinates[i][1];
		if ((y2 - y1) * (x3 - x1) !== (y3 - y1) * (x2 - x1)) return false;
	}
	return true;
};
```
