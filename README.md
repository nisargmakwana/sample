# Linked List
class Node {
	constructor(data, next = null) {
		this.data = data;
		this.next = next;
	}
}

class LinkedList {
	constructor() {
		this.head = null;
	}
}

// Insert at the beginning
LinkedList.prototype.insertAtBeginning = function (data) {
	// const newNode = new Node(data);
	// this.head = newNode;

	// the above 2 lines of code is from tut. following code is more universal

	const newNode = new Node(data);
	if (!this.head) {
		this.head = newNode;
		return;
	}
	newNode.next = this.head;
	this.head = newNode;
};

// Insert at the end
LinkedList.prototype.insertAtEnd = function (data) {
	const newNode = new Node(data);

	// if LL is empty
	if (!this.head) {
		this.head = newNode;
		return;
	}

	// if LL is not empty
	let current = this.head; // assumption that head is the current element
	while (current.next) {
		current = current.next;
	}
	current.next = newNode;
};

// Insert at after a given node

LinkedList.prototype.insertAfter = function (prevNode, data) {
	if (!prevNode) {
		console.log("prevNode cannot be null");
		return;
	}
	const newNode = new Node(data, prevNode.next);
	prevNode.next = newNode;
};

// Deleting first node or delete head

LinkedList.prototype.deleteFirstNode = function () {
	if (!this.head) {
		return "Linked List is empty";
	}
	this.head = this.head.next;
};

// Deleting Last node

LinkedList.prototype.deleteLastNode = function () {
	// If LL is empty
	if (!this.head) {
		return "The Linked List is already empty";
	}

	// If LL has one element
	if (!this.head.next) {
		this.head = null;
		return;
	}

	// if LL has more than one element
	let secondcurrent = this.head; // Assume that second current element is the head
	while (secondcurrent.next.next) {
		secondcurrent = secondcurrent.next;
	}
	secondcurrent.next = null;
};

// Delete a node with given key

LinkedList.prototype.deleteByKey = function (key) {
	// If LL is empty
	if (!this.head) {
		return "The linked list is empty";
	}

	// If key is at head
	if (this.head.data == key) {
		this.head = this.head.next;
		return;
	}

	// in other cases
	let current = this.head;
	while (current.next !== null) {
		if (current.next.data === key) {
			current.next = current.next.next;
			return;
		}
		current = current.next;
	}
	console.log("No node found with key: ", key);
};

// Search operation
LinkedList.prototype.search = function (key) {
	let current = this.head;
	while (current) {
		if (current.data === key) {
			return true;
		}
		current = current.next;
	}
	return false;
};

// Linked List Traversal
LinkedList.prototype.printList = function () {
	let current = this.head;
	let listValues = [];
	while (current) {
		listValues.push(current.data);
		current = current.next;
	}
	listValues
		? console.log(listValues.join(" -> "))
		: console.log("LinkedList is empty");
};

// Reverse a Linked List

LinkedList.prototype.reverse = function () {
	let current = this.head;
	let prev = null;
	let next = null;

	while (current) {
		next = current.next;
		current.next = prev;
		prev = current;
		current = next;
	}
	this.head = prev;
};

# Doubly Linked List

"use strict";

class Node {
	constructor(data, prev = null, next = null) {
		this.data = data;
		this.prev = prev;
		this.next = next;
	}
}

class DoublyLinkedList {
	constructor() {
		this.head = null;
		this.tail = null;
	}
}

// Insert at the beginning
DoublyLinkedList.prototype.insertAtBeginning = function (data) {
	const newNode = new Node(data, null, this.head);
	if (this.head !== null) {
		this.head.prev = newNode;
	}
	this.head = newNode;
	if (this.tail === null) {
		this.tail = newNode;
	}
};

// Insert at the end
DoublyLinkedList.prototype.insertAtEnd = function (data) {
	const newNode = new Node(data, this.tail, null);
	if (this.tail !== null) {
		this.tail.next = newNode;
	}
	this.tail = newNode;
	if (this.head === null) {
		this.head = newNode;
	}
};

const myDLL = new DoublyLinkedList();
console.log(myDLL);
myDLL.insertAtBeginning(7);
console.log(myDLL);
myDLL.insertAtEnd(6);
myDLL.insertAtEnd(5);
console.log(myDLL);

// Insert after a key
DoublyLinkedList.prototype.insertAfter = function (data, prevNode) {
	if (prevNode === null) {
		console.log("Invalid prev node");
		return;
	}
	const newNode = new Node(data, prevNode, prevNode.next);

	if (prevNode.next === null) {
		this.tail = newNode;
	}
	prevNode.next = newNode;
	if (prevNode.next !== null) {
		prevNode.next.prev = newNode;
	}
};

// Delete the first Node of Doubly linked list

DoublyLinkedList.prototype.deleteFirstNode = function () {
	if (this.head === null) {
		console.log("The LL is already empty");
		return;
	}
	if (this.head === this.tail) {
		this.head = null;
		this.tail = null;
		// this.head = this.tail = null;
	} else {
		this.head = this.head.next;
		this.head.prev = null;
	}
};

// Delete the last node of Doubly linked list
DoublyLinkedList.prototype.deleteLastNode = function () {
	if (!this.tail) {
		console.log("the DLL is already empty");
		return;
	}
	if (this.tail === this.head) {
		this.tail = null;
		this.head = null;
	} else {
		this.tail = this.tail.prev;
		this.tail.next = null;
	}
};

// Reverse a Doubly Linked List
DoublyLinkedList.prototype.reverse = function () {
	if (!this.head) {
		console.log("DLL is empty");
		return;
	}
	if (this.head === this.tail) {
		return;
	}
	let current = this.head;
	let temp = null;
	if (this.head !== this.tail) {
		while (current) {
			temp = current.prev;
			current.prev = current.next;
			current.next = temp;
			current = current.prev;
		}
		if (temp !== null) {
			this.tail = this.head;
			this.head = temp.prev;
		}
	}
};
