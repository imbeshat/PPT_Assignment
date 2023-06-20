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
	removeLoop(head) {
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

### 💡 **Question 5**

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return *the reordered list*.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1:**
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]

**Example 2:**
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]

## **Solution:**

```cpp
class Solution {
public:
	ListNode* oddEvenList(ListNode* head) {
		if(head == NULL || head->next == NULL){
				return head;
		}
		ListNode* odd = head;
		ListNode* even = head->next;
		ListNode* evenHead = even;
		while(even && even->next){
				odd->next = even->next;
				odd = odd->next;
				even->next = odd->next;
				even = even->next;
		}
		odd->next = evenHead;
		return head;
	}
};
```

### 💡 **Question 6**

Given a singly linked list of size **N**. The task is to **left-shift** the linked list by **k** nodes, where **k** is a given positive integer smaller than or equal to length of the linked list.

**Example 1:**
Input:
N = 5
value[] = {2, 4, 7, 8, 9}
k = 3
Output:8 9 2 4 7
Explanation:Rotate 1:4 -> 7 -> 8 -> 9 -> 2
Rotate 2: 7 -> 8 -> 9 -> 2 -> 4
Rotate 3: 8 -> 9 -> 2 -> 4 -> 7

**Example 2:**
Input:
N = 8
value[] = {1, 2, 3, 4, 5, 6, 7, 8}
k = 4
Output:5 6 7 8 1 2 3 4

## **Solution:**

```cpp
class Solution {
public:
	Node* rotate(Node* head, int k) {
		Node* curr = head;
		while(curr->next){
				curr = curr->next;
		}
		curr->next = head;
		curr = head;
		while(k--){
				curr = curr->next;
		}
		head = curr->next;
		curr->next = NULL;
		return head;
	}
};
```

### 💡 **Question 7**

You are given the `head` of a linked list with `n` nodes.

For each node in the list, find the value of the **next greater node**. That is, for each node, find the value of the first node that is next to it and has a **strictly larger** value than it.

Return an integer array `answer` where `answer[i]` is the value of the next greater node of the `ith` node (**1-indexed**). If the `ith` node does not have a next greater node, set `answer[i] = 0`.

**Example 1:**
Input: head = [2,1,5]
Output: [5,5,0]

**Example 2:**
Input: head = [2,7,4,3,5]
Output: [7,0,5,5,0]

## **Solution:**

```cpp
class Solution {
public:
	vector<int> nextLargerNodes(ListNode* head) {
		vector<int> ans;
		stack<int> s;
		for(ListNode* curr = head; curr != NULL; curr = curr->next){
				while(!s.empty() && ans[s.top()] < curr->val){
						ans[s.top()] = curr->val;
						s.pop();
				}
				s.push(ans.size());
				ans.push_back(curr->val);
		}
		while(!s.empty()){
				ans[s.top()] = 0;
				s.pop();
		}
		return ans;
	}
};
```

### 💡 **Question 8**

Given the `head` of a linked list, we repeatedly delete consecutive sequences of nodes that sum to `0` until there are no such sequences.

After doing so, return the head of the final linked list.  You may return any such answer.

(Note that in the examples below, all sequences are serializations of `ListNode` objects.)

**Example 1:**
Input: head = [1,2,-3,3,1]
Output: [3,1]
Note: The answer [1,2,1] would also be accepted.

**Example 2:**
Input: head = [1,2,3,-3,4]
Output: [1,2,4]

**Example 3:**
Input: head = [1,2,3,-3,-2]
Output: [1]

## **Solution:**

```cpp
class Solution {
public:
	ListNode* removeZeroSumSublists(ListNode* head) {
		ListNode* dummy = new ListNode(0);
		dummy->next = head;
		unordered_map<int, ListNode*> m;
		int prefix = 0;
		for(ListNode* i = dummy; i != NULL; i = i->next){
				prefix += i->val;
				m[prefix] = i;
		}
		prefix = 0;
		for(ListNode* i = dummy; i != NULL; i = i->next){
				prefix += i->val;
				i->next = m[prefix]->next;
		}
		return dummy->next;
	}
};
```
