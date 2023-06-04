# **Assignment 8 - Strings**

### 💡 **Question 1**

Given two strings s1 and s2, return _the lowest **ASCII** sum of deleted characters to make two strings equal_.

**Example 1:**

**Input:** s1 = "sea", s2 = "eat"

**Output:** 231

**Explanation:** Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.

Deleting "t" from "eat" adds 116 to the sum.

At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.

## Solution

```javascript
var minimumDeleteSum = function (s1, s2) {
	let dp = new Array(s1.length + 1).fill(0).map(() => new Array(s2.length + 1).fill(0));
	for (let i = 1; i <= s1.length; i++) {
		dp[i][0] = dp[i - 1][0] + s1.charCodeAt(i - 1);
	}
	for (let j = 1; j <= s2.length; j++) {
		dp[0][j] = dp[0][j - 1] + s2.charCodeAt(j - 1);
	}
	for (let i = 1; i <= s1.length; i++) {
		for (let j = 1; j <= s2.length; j++) {
			if (s1[i - 1] == s2[j - 1]) {
				dp[i][j] = dp[i - 1][j - 1];
			} else {
				dp[i][j] = Math.min(dp[i - 1][j] + s1.charCodeAt(i - 1), dp[i][j - 1] + s2.charCodeAt(j - 1));
			}
		}
	}
	return dp[s1.length][s2.length];
};
```

### 💡 **Question 2**

Given a string s containing only three types of characters: '(', ')' and '*', return true *if* s *is **valid\***.

The following rules define a **valid** string:

- Any left parenthesis '(' must have a corresponding right parenthesis ')'.
- Any right parenthesis ')' must have a corresponding left parenthesis '('.
- Left parenthesis '(' must go before the corresponding right parenthesis ')'.
- '\*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string "".

**Example 1:**

**Input:** s = "()"

**Output:**

true

## Solution

```javascript
var checkValidString = function (s) {
	let low = 0,
		high = 0;
	for (let i = 0; i < s.length; i++) {
		if (s[i] == "(") {
			low++;
			high++;
		} else if (s[i] == ")") {
			if (low > 0) {
				low--;
			}
			high--;
		} else {
			if (low > 0) {
				low--;
			}
			high++;
		}
		if (high < 0) {
			return false;
		}
	}
	return low == 0;
};
```

### 💡 **Question 3**

Given two strings word1 and word2, return _the minimum number of **steps** required to make_ word1 _and_ word2 _the same_.

In one **step**, you can delete exactly one character in either string.

**Example 1:**

**Input:** word1 = "sea", word2 = "eat"

**Output:** 2

**Explanation:** You need one step to make "sea" to "ea" and another step to make "eat" to "ea".

## Solution

```javascript
var minDistance = function (word1, word2) {
	let dp = new Array(word1.length + 1).fill(0).map(() => new Array(word2.length + 1).fill(0));
	for (let i = 1; i <= word1.length; i++) {
		dp[i][0] = i;
	}
	for (let j = 1; j <= word2.length; j++) {
		dp[0][j] = j;
	}
	for (let i = 1; i <= word1.length; i++) {
		for (let j = 1; j <= word2.length; j++) {
			if (word1[i - 1] == word2[j - 1]) {
				dp[i][j] = dp[i - 1][j - 1];
			} else {
				dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + 1;
			}
		}
	}
	return dp[word1.length][word2.length];
};
```

### 💡 **Question 4**

You need to construct a binary tree from a string consisting of parenthesis and integers.

The whole input represents a binary tree. It contains an integer followed by zero, one or two pairs of parenthesis. The integer represents the root's value and a pair of parenthesis contains a child binary tree with the same structure.
You always start to construct the **left** child node of the parent first if it exists.

**Input:** s = "4(2(3)(1))(6(5))"

**Output:** [4,2,6,3,1,5]

## Solution

```javascript
var str2tree = function (s) {
	if (s.length == 0) {
		return null;
	}
	let i = 0;
	while (i < s.length && s[i] != "(") {
		i++;
	}
	let root = new TreeNode(parseInt(s.substring(0, i)));
	let start = i,
		count = 0;
	for (; i < s.length; i++) {
		if (s[i] == "(") {
			count++;
		} else if (s[i] == ")") {
			count--;
		}
		if (count == 0) {
			break;
		}
	}
	if (start + 1 < i) {
		root.left = str2tree(s.substring(start + 1, i));
	}
	if (i + 2 < s.length) {
		root.right = str2tree(s.substring(i + 2, s.length - 1));
	}
	return root;
};
```

### 💡 **Question 5**

Given an array of characters chars, compress it using the following algorithm:

Begin with an empty string s. For each group of **consecutive repeating characters** in chars:

- If the group's length is 1, append the character to s.
- Otherwise, append the character followed by the group's length.

The compressed string s **should not be returned separately**, but instead, be stored **in the input character array chars**. Note that group lengths that are 10 or longer will be split into multiple characters in chars.

After you are done **modifying the input array,** return _the new length of the array_.

You must write an algorithm that uses only constant extra space.

**Example 1:**

**Input:** chars = ["a","a","b","b","c","c","c"]

**Output:** Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]

**Explanation:**

The groups are "aa", "bb", and "ccc". This compresses to "a2b2c3".

## Solution

```javascript
var compress = function (chars) {
	let i = 0,
		j = 0;
	while (i < chars.length) {
		let count = 0;
		let ch = chars[i];
		while (i < chars.length && chars[i] == ch) {
			count++;
			i++;
		}
		chars[j++] = ch;
		if (count > 1) {
			let str = count.toString();
			for (let k = 0; k < str.length; k++) {
				chars[j++] = str[k];
			}
		}
	}
	return j;
};
```

### 💡 **Question 6**

Given two strings s and p, return _an array of all the start indices of_ p*'s anagrams in* s. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** s = "cbaebabacd", p = "abc"

**Output:** [0,6]

**Explanation:**

The substring with start index = 0 is "cba", which is an anagram of "abc".

The substring with start index = 6 is "bac", which is an anagram of "abc".

## Solution

```javascript
var findAnagrams = function (s, p) {
	let map = new Map();
	for (let i = 0; i < p.length; i++) {
		if (map.has(p[i])) {
			map.set(p[i], map.get(p[i]) + 1);
		} else {
			map.set(p[i], 1);
		}
	}
	let count = map.size;
	let i = 0,
		j = 0;
	let ans = [];
	while (j < s.length) {
		if (map.has(s[j])) {
			map.set(s[j], map.get(s[j]) - 1);
			if (map.get(s[j]) == 0) {
				count--;
			}
		}
		if (j - i + 1 < p.length) {
			j++;
		} else if (j - i + 1 == p.length) {
			if (count == 0) {
				ans.push(i);
			}
			if (map.has(s[i])) {
				map.set(s[i], map.get(s[i]) + 1);
				if (map.get(s[i]) == 1) {
					count++;
				}
			}
			i++;
			j++;
		}
	}
	return ans;
};
```

### 💡 **Question 7**

Given an encoded string, return its decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there will not be input like 3a or 2[4].

The test cases are generated so that the length of the output will never exceed 105.

**Example 1:**

**Input:** s = "3[a]2[bc]"

**Output:** "aaabcbc"

## Solution

```javascript
var decodeString = function (s) {
	let stack = [];
	for (let i = 0; i < s.length; i++) {
		if (s[i] == "]") {
			let str = "";
			while (stack[stack.length - 1] != "[") {
				str = stack.pop() + str;
			}
			stack.pop();
			let num = "";
			while (stack.length > 0 && stack[stack.length - 1].charCodeAt(0) >= 48 && stack[stack.length - 1].charCodeAt(0) <= 57) {
				num = stack.pop() + num;
			}
			num = parseInt(num);
			let temp = "";
			for (let j = 0; j < num; j++) {
				temp += str;
			}
			stack.push(temp);
		} else {
			stack.push(s[i]);
		}
	}
	let ans = "";
	while (stack.length > 0) {
		ans = stack.pop() + ans;
	}
	return ans;
};
```

### 💡 **Question 8**

Given two strings s and goal, return true _if you can swap two letters in_ s _so the result is equal to_ goal*, otherwise, return* false*.*

Swapping letters is defined as taking two indices i and j (0-indexed) such that i != j and swapping the characters at s[i] and s[j].

- For example, swapping at indices 0 and 2 in "abcd" results in "cbad".

**Example 1:**

**Input:** s = "ab", goal = "ba"

**Output:** true

**Explanation:** You can swap s[0] = 'a' and s[1] = 'b' to get "ba", which is equal to goal.

## Solution

```javascript
var buddyStrings = function (s, goal) {
	if (s.length != goal.length) {
		return false;
	}
	if (s == goal) {
		let set = new Set();
		for (let i = 0; i < s.length; i++) {
			if (set.has(s[i])) {
				return true;
			}
			set.add(s[i]);
		}
		return false;
	}
	let first = -1,
		second = -1;
	for (let i = 0; i < s.length; i++) {
		if (s[i] != goal[i]) {
			if (first == -1) {
				first = i;
			} else if (second == -1) {
				second = i;
			} else {
				return false;
			}
		}
	}
	return second != -1 && s[first] == goal[second] && s[second] == goal[first];
};
```
