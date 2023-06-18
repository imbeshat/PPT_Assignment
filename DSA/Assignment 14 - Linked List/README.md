# **Assignment 14 - Linked List**

### 💡 **Question 1**

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

## **Solution:**

```javascript
class Solution {
	//Function to remove a loop in the linked list.
	removeLoop(head) {
		// code here
		// remove the loop without losing any nodes
		let slow = head;
		let fast = head;
		let loop = false;
		while (fast && fast.next) {
			slow = slow.next;
			fast = fast.next.next;
			if (slow === fast) {
				loop = true;
				break;
			}
		}
		if (loop) {
			slow = head;
			if (slow === fast) {
				while (fast.next !== slow) {
					fast = fast.next;
				}
			} else {
				while (slow.next !== fast.next) {
					slow = slow.next;
					fast = fast.next;
				}
			}
			fast.next = null;
		}
	}
}
```

### 💡 **Question 2**

A number **N** is represented in Linked List such that each digit corresponds to a node in linked list. You need to add 1 to it.

**Example 1:**
Input:
LinkedList: 4->5->6
Output:457

**Example 2:**
Input:
LinkedList: 1->2->3
Output:124

## **Solution:**

```javascript
class Solution {
	addOne(head) {
		//code here
		let curr = head;
		let prev = null;
		let next = null;
		let carry = 1;
		while (curr) {
			next = curr.next;
			curr.next = prev;
			prev = curr;
			curr = next;
		}
		head = prev;
		curr = head;
		while (curr) {
			let sum = curr.data + carry;
			carry = sum >= 10 ? 1 : 0;
			curr.data = sum % 10;
			if (curr.next === null && carry === 1) {
				curr.next = new Node(1);
				break;
			}
			curr = curr.next;
		}
		prev = null;
		curr = head;
		next = null;
		while (curr) {
			next = curr.next;
			curr.next = prev;
			prev = curr;
			curr = next;
		}
		head = prev;
		return head;
	}
}
```

### 💡 **Question 3**

Given a Linked List of size N, where every node represents a sub-linked-list and contains two pointers:(i) a **next** pointer to the next node,(ii) a **bottom** pointer to a linked list where this node is head.Each of the sub-linked-list is in sorted order.Flatten the Link List such that all the nodes appear in a single level while maintaining the sorted order. **Note:** The flattened list will be printed using the bottom pointer instead of next pointer.

**Example 1:**
Input:
5 -> 10 -> 19 -> 28
| | | |
7 20 22 35
| | |
8 50 40
| |
30 45
Output: 5-> 7-> 8- > 10 -> 19-> 20->
22-> 28-> 30-> 35-> 40-> 45-> 50.
Explanation:
The resultant linked lists has every
node in a single level.(Note:| represents the bottom pointer.)

**Example 2:**
Input:
5 -> 10 -> 19 -> 28
| |
7 22
| |
8 50
|
30
Output: 5->7->8->10->19->22->28->30->50
Explanation:
The resultant linked lists has every
node in a single level.

(Note:| represents the bottom pointer.)

## **Solution:**

```javascript
class Solution {
	flatten(root) {
		if (root === null || root.next === null) {
			return root;
		}
		root.next = this.flatten(root.next);
		root = this.merge(root, root.next);
		return root;
	}
	merge(a, b) {
		if (a === null) {
			return b;
		}
		if (b === null) {
			return a;
		}
		let result;
		if (a.data < b.data) {
			result = a;
			result.bottom = this.merge(a.bottom, b);
		} else {
			result = b;
			result.bottom = this.merge(a, b.bottom);
		}
		result.next = null;
		return result;
	}
}
```

### 💡 **Question 4**

You are given a special linked list with **N** nodes where each node has a next pointer pointing to its next node. You are also given **M** random pointers, where you will be given **M** number of pairs denoting two nodes **a** and **b**  **i.e. a->arb = b** (arb is pointer to random node)**.**

Construct a copy of the given list. The copy should consist of exactly **N** new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes **X** and **Y** in the original list, where **X.arb** **-->** **Y**, then for the corresponding two nodes **x** and **y** in the copied list, **x.arb --> y.**

Return the head of the copied linked list.

**Note** :- The diagram isn't part of any example, it just depicts an example of how the linked list may look like.

**Example 1:**
Input:
N = 4, M = 2
value = {1,2,3,4}
pairs = {{1,2},{2,4}}
Output:1
Explanation:In this test case, there
are 4 nodes in linked list.  Among these
4 nodes,  2 nodes have arbitrary pointer
set, rest two nodes have arbitrary pointer
as NULL. Second line tells us the value
of four nodes. The third line gives the
information about arbitrary pointers.
The first node arbitrary pointer is set to
node 2.  The second node arbitrary pointer
is set to node 4.

**Example 2:**
Input:
N = 4, M = 2
value[] = {1,3,5,9}
pairs[] = {{1,1},{3,4}}
Output:1
Explanation:In the given testcase ,
applying the method as stated in the
above example, the output will be 1.

## **Solution:**

```javascript
class Solution {
	copyList(head) {
		//code here
		let curr = head;
		let next = null;
		while (curr) {
			next = curr.next;
			curr.next = new Node(curr.data);
			curr.next.next = next;
			curr = next;
		}
		curr = head;
		while (curr) {
			if (curr.next) {
				curr.next.arb = curr.arb ? curr.arb.next : curr.arb;
			}
			curr = curr.next ? curr.next.next : curr.next;
		}
		let original = head;
		let copy = head.next;
		let temp = copy;
		while (original && copy) {
			original.next = original.next ? original.next.next : original.next;
			copy.next = copy.next ? copy.next.next : copy.next;
			original = original.next;
			copy = copy.next;
		}
		return temp;
	}
}
```
