# **Assignment 13 - Linked List**

### 💡 **Question 1**

Given two linked list of the same size, the task is to create a new linked list using those linked lists. The condition is that the greater node among both linked list will be added to the new linked list.

**Examples:**
Input: list1 = 5->2->3->8
list2 = 1->7->4->5
Output: New list = 5->7->4->8

Input:list1 = 2->8->9->3
list2 = 5->3->6->4
Output: New list = 5->8->9->4

## **Solution**

```javascript
class Node {
	constructor(val) {
		this.data = val;
		this.next = null;
	}
}
function insert(root, item) {
	var ptr, temp;
	temp = new Node();
	temp.data = item;
	temp.next = null;

	if (root == null) root = temp;
	else {
		ptr = root;
		while (ptr.next != null) ptr = ptr.next;

		ptr.next = temp;
	}
	return root;
}

function newList(root1, root2) {
	var ptr1 = root1,
		ptr2 = root2,
		ptr;
	var root = null,
		temp;

	while (ptr1 != null) {
		temp = new Node();
		temp.next = null;

		// Compare for greater node
		if (ptr1.data < ptr2.data) temp.data = ptr2.data;
		else temp.data = ptr1.data;

		if (root == null) root = temp;
		else {
			ptr = root;
			while (ptr.next != null) ptr = ptr.next;

			ptr.next = temp;
		}
		ptr1 = ptr1.next;
		ptr2 = ptr2.next;
	}
	return root;
}

function display(root) {
	while (root != null) {
		document.write(root.data + "->");
		root = root.next;
	}
	document.write("<br/>");
}

// Driver code

(root1 = null), (root2 = null), (root = null);

root1 = insert(root1, 5);
root1 = insert(root1, 2);
root1 = insert(root1, 3);
root1 = insert(root1, 8);

document.write("First List: ");
display(root1);

root2 = insert(root2, 1);
root2 = insert(root2, 7);
root2 = insert(root2, 4);
root2 = insert(root2, 5);

document.write("Second List: ");
display(root2);

root = newList(root1, root2);
document.write("New List: ");
display(root);
```

### 💡 **Question 2**

Write a function that takes a list sorted in non-decreasing order and deletes any duplicate nodes from the list. The list should only be traversed once.

For example if the linked list is 11->11->11->21->43->43->60 then removeDuplicates() should convert the list to 11->21->43->60.

**Example 1:**
Input:
LinkedList:
11->11->11->21->43->43->60
Output:
11->21->43->60

**Example 2:**
Input:
LinkedList:
10->12->12->25->25->25->34
Output:
10->12->25->34

## **Solution**

```javascript
class Node {
	constructor(d) {
		this.data = d;
		this.next = null;
	}
}

let head = new Node();
function removeDuplicates() {
	let curr = head;

	while (curr != null) {
		let temp = curr;
		while (temp != null && temp.data == curr.data) {
			temp = temp.next;
		}
		curr.next = temp;
		curr = curr.next;
	}
}

function push(new_data) {
	let new_node = new Node(new_data);

	new_node.next = head;

	head = new_node;
}

function printList() {
	let temp = head;
	while (temp != null && temp.data) {
		document.write(temp.data + " ");
		temp = temp.next;
	}
	document.write("<br>");
}

/* Driver program to test above functions */
push(20);
push(13);
push(13);
push(11);
push(11);
push(11);

document.write("List before removal of duplicates ");
printList();

removeDuplicates();

document.write("List after removal of elements ");
printList();
```

### 💡 **Question 3**

Given a linked list of size **N**. The task is to reverse every **k** nodes (where k is an input to the function) in the linked list. If the number of nodes is not a multiple of *k* then left-out nodes, in the end, should be considered as a group and must be reversed (See Example 2 for clarification).

**Example 1:**
Input:
LinkedList: 1->2->2->4->5->6->7->8
K = 4
Output:4 2 2 1 8 7 6 5
Explanation:
The first 4 elements 1,2,2,4 are reversed first
and then the next 4 elements 5,6,7,8. Hence, the
resultant linked list is 4->2->2->1->8->7->6->5.

## **Solution**

```cpp
class Solution
{
    public:
    struct node *reverse (struct node *head, int k)
    {
        node* current = head;
        node* next = NULL;
        node* prev = NULL;
        int count = 0;
        while(current != NULL && count < k){
            next = current->next;
            current->next = prev;
            prev = current;
            current = next;
            count++;
        }
        if(next != NULL){
            head->next = reverse(next, k);
        }
        return prev;
    }
};
```

### 💡 **Question 4**

Given a linked list, write a function to reverse every alternate k nodes (where k is an input to the function) in an efficient way. Give the complexity of your algorithm.

**Example:**
Inputs: 1->2->3->4->5->6->7->8->9->NULL and k = 3
Output: 3->2->1->4->5->6->9->8->7->NULL.

## **Solution**

```javascript
class Node {
	constructor(d) {
		this.data = d;
		this.next = null;
	}
}

let head;

function kAltReverse(node, k) {
	let current = node;
	let next = null,
		prev = null;
	let count = 0;

	while (current != null && count < k) {
		next = current.next;
		current.next = prev;
		prev = current;
		current = next;
		count++;
	}

	if (node != null) {
		node.next = current;
	}

	count = 0;
	while (count < k - 1 && current != null) {
		current = current.next;
		count++;
	}

	if (current != null) {
		current.next = kAltReverse(current.next, k);
	}

	/* 5) prev is new head of the input list */
	return prev;
}

function printList(node) {
	while (node != null) {
		document.write(node.data + " ");
		node = node.next;
	}
}

function push(newdata) {
	let mynode = new Node(newdata);
	mynode.next = head;
	head = mynode;
}

// Driver code
for (let i = 20; i > 0; i--) {
	push(i);
}
document.write("Given Linked List :<br>");
printList(head);
head = kAltReverse(head, 3);

document.write("<br>");
document.write("Modified Linked List :<br>");
printList(head);
```

### 💡 **Question 5**

Given a linked list and a key to be deleted. Delete last occurrence of key from linked. The list may have duplicates.

**Examples**:
Input: 1->2->3->5->2->10, key = 2
Output: 1->2->3->5->10

## **Solution**

```javascript
class Node {
	constructor(data) {
		this.data = data;
		this.next = null;
	}
}

{
	let temp = head;
	let prt = null;
	while (temp != null) {
		if (temp.data == x) ptr = temp;
		temp = temp.next;
	}

	if (ptr != null && ptr.next == null) {
		temp = head;
		while (temp.next != ptr) {
			temp = temp.next;
		}
		temp.next = null;
	}

	if (ptr != null && ptr.next != null) {
		ptr.data = ptr.next.data;
		temp = ptr.next;
		ptr.next = ptr.next.next;
	}
	return head;
}

function display(head) {
	let temp = head;
	if (head == null) {
		document.write("NULL<br>");
		return;
	}
	while (temp != null) {
		document.write(temp.data, " --> ", (end = ""));
		temp = temp.next;
	}
	document.write("NULL<br>");
}

// Driver code
let head = new Node(1);
head.next = new Node(2);
head.next.next = new Node(3);
head.next.next.next = new Node(4);
head.next.next.next.next = new Node(5);
head.next.next.next.next.next = new Node(4);
head.next.next.next.next.next.next = new Node(4);

document.write("Created Linked list: ");
display(head);

head = deleteLast(head, 4);
document.write("List after deletion of 4: ");
display(head);
```

### 💡 **Question 6**

Given two sorted linked lists consisting of **N** and **M** nodes respectively. The task is to merge both of the lists (in place) and return the head of the merged list.

**Examples:**

Input: a: 5->10->15, b: 2->3->20

Output: 2->3->5->10->15->20

Input: a: 1->1, b: 2->4

Output: 1->1->2->4

## **Solution**

```javascript
class Node {
	constructor(d) {
		this.data = d;
		this.next = null;
	}
}

class LinkedList {
	constructor() {
		this.head = null;
	}

	addToTheLast(node) {
		if (this.head == null) {
			this.head = node;
		} else {
			let temp = this.head;
			while (temp.next != null) temp = temp.next;
			temp.next = node;
		}
	}

	printList() {
		let temp = this.head;
		while (temp != null) {
			document.write(temp.data + " ");
			temp = temp.next;
		}
		document.write("<br>");
	}
}

function sortedMerge(headA, headB) {
	let dummyNode = new Node(0);

	let tail = dummyNode;
	while (true) {
		if (headA == null) {
			tail.next = headB;
			break;
		}
		if (headB == null) {
			tail.next = headA;
			break;
		}

		if (headA.data <= headB.data) {
			tail.next = headA;
			headA = headA.next;
		} else {
			tail.next = headB;
			headB = headB.next;
		}

		tail = tail.next;
	}
	return dummyNode.next;
}

let llist1 = new LinkedList();
let llist2 = new LinkedList();

llist1.addToTheLast(new Node(5));
llist1.addToTheLast(new Node(10));
llist1.addToTheLast(new Node(15));

llist2.addToTheLast(new Node(2));
llist2.addToTheLast(new Node(3));
llist2.addToTheLast(new Node(20));

llist1.head = sortedMerge(llist1.head, llist2.head);
document.write("Merged Linked List is:<br>");
llist1.printList();
```

### 💡 **Question 7**

Given a **Doubly Linked List**, the task is to reverse the given Doubly Linked List.

**Example:**
Original Linked list 10 8 4 2
Reversed Linked list 2 4 8 10

## **Solution**

```javascript
var head;

class Node {
	constructor(val) {
		this.data = val;
		this.prev = null;
		this.next = null;
	}
}
function reverse() {
	var temp = null;
	var current = head;

	while (current != null) {
		temp = current.prev;
		current.prev = current.next;
		current.next = temp;
		current = current.prev;
	}

	if (temp != null) {
		head = temp.prev;
	}
}

function push(new_data) {
	var new_node = new Node(new_data);

	new_node.prev = null;

	new_node.next = head;

	if (head != null) {
		head.prev = new_node;
	}

	head = new_node;
}

function printList(node) {
	while (node != null) {
		document.write(node.data + " ");
		node = node.next;
	}
}

push(2);
push(4);
push(8);
push(10);

document.write("Original linked list <br/>");
printList(head);

reverse();
document.write("<br/>");
document.write("The reversed Linked List is <br/>");
printList(head);
```

### 💡 **Question 8**

Given a doubly linked list and a position. The task is to delete a node from given position in a doubly linked list.

**Example 1:**
Input:
LinkedList = 1 <--> 3 <--> 4
x = 3
Output:1 3
Explanation:After deleting the node at
position 3 (position starts from 1),
the linked list will be now as 1->3.

**Example 2:**
Input:
LinkedList = 1 <--> 5 <--> 2 <--> 9
x = 1
Output:5 2 9

## **Solution**

```javascript
class Node {
	constructor() {
		this.data = 0;
		this.prev = null;
		this.next = null;
	}
}
var head = null;

function deleteNode(del) {
	if (head == null || del == null) return null;

	if (head == del) head = del.next;

	if (del.next != null) del.next.prev = del.prev;

	if (del.prev != null) del.prev.next = del.next;

	del = null;

	return head;
}

function deleteNodeAtGivenPos(n) {
	if (head == null || n <= 0) return;

	var current = head;
	var i;

	for (i = 1; current != null && i < n; i++) {
		current = current.next;
	}

	if (current == null) return;

	deleteNode(current);
}

function push(new_data) {
	var new_node = new Node();

	new_node.data = new_data;

	new_node.prev = null;

	new_node.next = head;

	if (head != null) head.prev = new_node;

	head = new_node;
}

function printList() {
	var temp = head;
	if (temp == null) document.write("Doubly Linked list empty");

	while (temp != null) {
		document.write(temp.data + " ");
		temp = temp.next;
	}
	document.write();
}

// Driver code

push(5);
push(2);
push(4);
push(8);
push(10);

document.write("Doubly linked " + "list before deletion:<br/>");
printList();

var n = 2;

deleteNodeAtGivenPos(n);
document.write("<br/>Doubly linked " + "list after deletion:<br/>");
printList();
```
