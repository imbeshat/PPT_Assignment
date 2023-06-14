# **Assignment 12 - Linked List**

### 💡 **Question 1**

Given a singly linked list, delete **middle** of the linked list. For example, if given linked list is 1->2->**3**->4->5 then linked list should be modified to 1->2->4->5.If there are **even** nodes, then there would be **two middle** nodes, we need to delete the second middle element. For example, if given linked list is 1->2->3->4->5->6 then it should be modified to 1->2->3->5->6.If the input linked list is NULL or has 1 node, then it should return NULL

**Example 1:**
Input:
LinkedList: 1->2->3->4->5
Output:1 2 4 5

**Example 2:**
Input:
LinkedList: 2->4->6->7->5->1
Output:2 4 6 5 1

## **Solution :**

```javascript
class Node {
	constructor(data) {
		this.data = data;
		this.next = null;
	}
}

class LinkedList {
	constructor() {
		this.head = null;
		this.size = 0;
	}

	add(data) {
		const newNode = new Node(data);
		if (this.head === null) {
			this.head = newNode;
		} else {
			let current = this.head;
			while (current.next) {
				current = current.next;
			}
			current.next = newNode;
		}
		this.size++;
	}

	print() {
		let current = this.head;
		while (current) {
			console.log(current.data);
			current = current.next;
		}
	}

	deleteMiddle() {
		let current = this.head;
		let middle = this.head;
		let prev = null;
		while (current && current.next) {
			current = current.next.next;
			prev = middle;
			middle = middle.next;
		}
		prev.next = middle.next;
		this.size--;
	}
}

const ll = new LinkedList();
ll.add(1);
ll.add(2);
ll.add(3);
ll.add(4);
ll.add(5);
ll.add(6);
ll.add(7);
ll.add(8);
ll.add(9);
ll.add(10);
ll.deleteMiddle();
ll.print();
```

### 💡 **Question 2**

Given a linked list of **N** nodes. The task is to check if the linked list has a loop. Linked list can contain self loop.

**Example 1:**
Input:
N = 3
value[] = {1,3,4}
x(position at which tail is connected) = 2
Output:True
Explanation:In above test case N = 3.
The linked list with nodes N = 3 is
given. Then value of x=2 is given which
means last node is connected with xth
node of linked list. Therefore, there
exists a loop.

**Example 2:**
Input:
N = 4
value[] = {1,8,3,4}
x = 0
Output:False
Explanation:For N = 4 ,x = 0 means
then lastNode->next = NULL, then
the Linked list does not contains
any loop.

## **Solution :**

```javascript
class Solution {
	detectLoop(head) {
		let slow = head;
		let fast = head;
		while (fast && fast.next) {
			slow = slow.next;
			fast = fast.next.next;
			if (slow === fast) {
				return true;
			}
		}
		return false;
	}
}
```

### 💡 **Question 3**

Given a linked list consisting of **L** nodes and given a number **N**. The task is to find the **N**th node from the end of the linked list.

**Example 1:**
Input:
N = 2
LinkedList: 1->2->3->4->5->6->7->8->9
Output:8
Explanation:In the first example, there
are 9 nodes in linked list and we need
to find 2nd node from end. 2nd node
from end is 8.

**Example 2:**
Input:
N = 5
LinkedList: 10->5->100->5
Output:-1
Explanation:In the second example, there
are 4 nodes in the linked list and we
need to find 5th from the end. Since 'n'
is more than the number of nodes in the
linked list, the output is -1.

## **Solution :**

```javascript
class Solution {
	getNthFromLast(head, n) {
		let slow = head;
		let fast = head;
		let count = 0;
		while (count < n) {
			if (fast === null) {
				return -1;
			}
			fast = fast.next;
			count++;
		}
		while (fast) {
			slow = slow.next;
			fast = fast.next;
		}
		return slow.data;
	}
}
```

### 💡 **Question 4**

Given a singly linked list of characters, write a function that returns true if the given list is a palindrome, else false.
**Examples:**

Input: R->A->D->A->R->NULL
**Output:** Yes
**Input:** C->O->D->E->NULL
**Output:** No

## **Solution :**

```javascript
class Solution {
	isPalindrome(head) {
		let slow = head;
		let fast = head;
		let prev = null;
		while (fast && fast.next) {
			fast = fast.next.next;
			let temp = slow.next;
			slow.next = prev;
			prev = slow;
			slow = temp;
		}
		if (fast) {
			slow = slow.next;
		}
		while (slow) {
			if (slow.data !== prev.data) {
				return false;
			}
			slow = slow.next;
			prev = prev.next;
		}
		return true;
	}
}
```

### 💡 **Question 5**

Given a linked list of **N** nodes such that it may contain a loop.

A loop here means that the last node of the link list is connected to the node at position X(1-based index). If the link list does not have any loop, X=0.

Remove the loop from the linked list, if it is present, i.e. unlink the last node which is forming the loop.

**Example 1:**
Input:
N = 3
value[] = {1,3,4}
X = 2
Output:1
Explanation:The link list looks like
1 -> 3 -> 4
^ |
|\_\_\_\_|
A loop is present. If you remove it
successfully, the answer will be 1.

**Example 2:**
Input:
N = 4
value[] = {1,8,3,4}
X = 0
Output:1
Explanation:The Linked list does not
contains any loop.

**Example 3:**
Input:
N = 4
value[] = {1,2,3,4}
X = 1
Output:1
Explanation:The link list looks like
1 -> 2 -> 3 -> 4
^ |
|**\*\***\_\_**\*\***|
A loop is present.
If you remove it successfully,
the answer will be 1.

## **Solution :**

```javascript
class Solution {
	removeLoop(head) {
		let slow = head;
		let fast = head;
		while (fast && fast.next) {
			slow = slow.next;
			fast = fast.next.next;
			if (slow === fast) {
				break;
			}
		}
		if (slow !== fast) {
			return;
		}
		slow = head;
		while (slow.next !== fast.next) {
			slow = slow.next;
			fast = fast.next;
		}
		fast.next = null;
	}
}
```

### 💡 **Question 6**

Given a linked list and two integers M and N. Traverse the linked list such that you retain M nodes then delete next N nodes, continue the same till end of the linked list.

Difficulty Level: Rookie

**Examples**:
Input:
M = 2, N = 2
Linked List: 1->2->3->4->5->6->7->8
Output:
Linked List: 1->2->5->6

Input:
M = 3, N = 2
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->2->3->6->7->8

Input:
M = 1, N = 1
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->3->5->7->9

## **Solution :**

```javascript
class Solution {
	linkdelete(head, M, N) {
		let current = head;
		while (current) {
			let count = 1;
			while (count < M && current) {
				current = current.next;
				count++;
			}
			if (current === null) {
				return;
			}
			let temp = current.next;
			count = 1;
			while (count <= N && temp) {
				temp = temp.next;
				count++;
			}
			current.next = temp;
			current = temp;
		}
		return head;
	}
}
```

### 💡 **Question 7**

Given two linked lists, insert nodes of second list into first list at alternate positions of first list.
For example, if first list is 5->7->17->13->11 and second is 12->10->2->4->6, the first list should become 5->12->7->10->17->2->13->4->11->6 and second list should become empty. The nodes of second list should only be inserted when there are positions available. For example, if the first list is 1->2->3 and second list is 4->5->6->7->8, then first list should become 1->4->2->5->3->6 and second list to 7->8.

Use of extra space is not allowed (Not allowed to create additional nodes), i.e., insertion must be done in-place. Expected time complexity is O(n) where n is number of nodes in first list.

## **Solution**

```javascript
class Solution {
	merge(head1, head2) {
		let current1 = head1;
		let current2 = head2;
		while (current1 && current2) {
			let temp1 = current1.next;
			let temp2 = current2.next;
			current1.next = current2;
			current2.next = temp1;
			current1 = temp1;
			current2 = temp2;
		}
		return head1;
	}
}
```

### 💡 **Question 8**

Given a singly linked list, find if the linked list is [circular](https://www.geeksforgeeks.org/circular-linked-list/amp/) or not.

> A linked list is called circular if it is not NULL-terminated and all nodes are connected in the form of a cycle. Below is an example of a circular linked list.

## **Solution**

```javascript
class Solution {
	isCircular(head) {
		let slow = head;
		let fast = head;
		while (fast && fast.next) {
			slow = slow.next;
			fast = fast.next.next;
			if (slow === fast) {
				return true;
			}
		}
		return false;
	}
}
```
