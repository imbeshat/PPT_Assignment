# **Assignment 10 - Recursion**

### 💡 **Question 1**

Given an integer `n`, return *`true` if it is a power of three. Otherwise, return `false`*.

An integer `n` is a power of three, if there exists an integer `x` such that `n == 3x`.

**Example 1:**
Input: n = 27
Output: true
Explanation: 27 = 33

**Example 2:**
Input: n = 0
Output: false
Explanation: There is no x where 3x = 0.

**Example 3:**
Input: n = -1
Output: false
Explanation: There is no x where 3x = (-1).

## Solution

```javascript
var isPowerOfThree = function (n) {
	if (n == 1) return true;
	if (n % 3 != 0 || n == 0) return false;
	return isPowerOfThree(n / 3);
};
```

### 💡 **Question 2**

You have a list `arr` of all integers in the range `[1, n]` sorted in a strictly increasing order. Apply the following algorithm on `arr`:

- Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.
- Repeat the previous step again, but this time from right to left, remove the rightmost number and every other number from the remaining numbers.
- Keep repeating the steps again, alternating left to right and right to left, until a single number remains.

Given the integer `n`, return *the last number that remains in* `arr`.

**Example 1:**
Input: n = 9
Output: 6
Explanation:
arr = [1, 2,3, 4,5, 6,7, 8,9]
arr = [2,4, 6,8]
arr = [2, 6]
arr = [6]

**Example 2:**
Input: n = 1
Output: 1

## Solution

```cpp
class Solution {
public:
    int lastRemaining(int n) {
        if(n==1) return 1;
        return 2*(n/2+1-lastRemaining(n/2));
    }
};
```

### 💡 **Question 3**

Given a set represented as a string, write a recursive code to print all subsets of it. The subsets can be printed in any order.

**Example 1:**

Input :  set = “abc”

Output : { “”, “a”, “b”, “c”, “ab”, “ac”, “bc”, “abc”}

**Example 2:**

Input : set = “abcd”

Output : { “”, “a” ,”ab” ,”abc” ,”abcd”, “abd” ,”ac” ,”acd”, “ad” ,”b”, “bc” ,”bcd” ,”bd” ,”c” ,”cd” ,”d” }

## Solution

```javascript
function printSubsets(str, curr = "", index = 0) {
	if (index == str.length) {
		console.log(curr);
		return;
	}
	printSubsets(str, curr, index + 1);
	printSubsets(str, curr + str[index], index + 1);
}
```
