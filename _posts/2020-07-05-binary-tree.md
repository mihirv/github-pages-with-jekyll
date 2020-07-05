---
title: "Binary Tree"
date: 2020-07-05
---

> The method of solution involves the development of a theory of finite automata operating on infinite trees.

A binary tree is a data structure that is useful for representing hierarchy. Binary tree is a tree with either 
1. empty subtree or 
2. a root node r together with two disjoint binary tree (left binary tree and a right binary tree).

## Properties
### Definitions
Each node, except the root, is itself the root of a left subtree or a right subtree. Often the node stores additional data. Its prototype is listed as follows:
```java
public static class BinaryTreeNode<T> {
	public T data;  
	public BinaryTreeNode<T> left, right;
}
```

- **Leaf:** A node that has no descendants except for itself is called a leaf.
- **Depth:** The depth of a node n is the number of nodes on the search path from the root to n, not including n itself. 
- **Height:** The height of a binary tree is the maximum depth of any node in that tree.

**Types of Binary trees**
- **Full binary tree** is a binary tree in which every node other than the leaves has two children. 
- **Complete binary tree** is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
- **Perfect binary tree** is a full binary tree in which all leaves are at the same depth, and in which every parent has two children.

**Number of Nodes**
- The number of nonleaf nodes in a full binary tree is one less than the number of leaves.
- A perfect binary tree of height h contains exactly 2<sup>h</sup> - 1 nodes, of which 2h are leaves.
- A complete binary tree on n nodes has height Lg n. 
- A left-skewed tree is a tree in which no node has a right child.
- A right-skewed tree is a tree in which no node has a left child.

### Binary Tree Traversal / Walking
A key computation on a binary tree is traversing / walking all the nodes in the tree. Let T be a binary tree of n nodes, with height h. Implemented recursively, these traversals have 0(n) time complexity and 0(h) additional space complexity (The space complexity is dictated by the maximum depth of the function call stack.) If each node has a parent field, the traversals can be done with 0(1) additional space complexity.

#### 1. Inorder traversal
Traverse the left subtree, visit the root, then traverse the right subtree.

Using **recursive** strategy
```java
public static void inOrderTraversal(BinaryTreeNode node) {
	if (node == null) {
		return;
	}

	inOrderTraversal(node.left);
	System.out.println(node);
	inOrderTraversal(node.right);
}
```
Using **iterative** strategy (Stack)
```java
public static void inOrderTraversal(BinaryTreeNode node) {
	Stack<BinaryTreeNode> stack = new Stack<>();
	pushToStack(node, stack);
	while(!stack.isEmpty()) {
		node = stack.pop()
		System.out.println(node);
		pushToStack(node.right, stack);
	}
}

static void pushToStack(BinaryTreeNode node, Stack<BinaryTreeNode> stack) {
	while(node != null) {
		stack.push(node);
	}
}
```

#### 2. Preorder traversal
Visit the root, traverse the left subtree, then traverse the right subtree.

Using **recursive** strategy
```java
public static void preOrderTraversal(BinaryTreeNode node) {
	if (node == null) {
		return;
	}

	System.out.println(node);
	preOrderTraversal(node.left);
	preOrderTraversal(node.right);
}
```
Using **iterative** strategy (Queue)
```java
public static void preOrderTraversal(BinaryTreeNode node) {
	Queue<BinaryTreeNode> q = new Queue<>()
	q.offer(node);
	while (!q.isEmpty()) {
		node = q.poll();
		System.out.println(node);
		addToQueue(node.left);
		addToQueue(node.right);
	}
}

static void addToQueue(BinaryTreeNode node, Queue<BinaryTreeNode> q) {		
	if (node != null) {
		q.offer(node);
	}
}
```
Using **iterative** strategy (Stack)
```java
public static void preOrderTraversal(BinaryTreeNode node) {
	Stack<BinaryTreeNode> stack = new Stack<>()
	stack.push(node);
	
	while(!stack.isEmpty()) {
		node = stack.pop();
		System.out.println(node);
		pushToStack(node.right);
		pushToStack(node.left);
	}
}

static void pushToStack(BinaryTreeNode node, Stack<BinaryTreeNode> stack) {
	while(node != null) {
		stack.push(node);
	}
}
```

#### 3. Postorder traversal
Traverse the left subtree, traverse the right subtree, and then visit the root.

Using **recursive** strategy
```java
public static void postOrderTraversal(BinaryTreeNode node) {
	if (node == null) {
		return;
	}

	postOrderTraversal(node.left);
	postOrderTraversal(node.right);
	System.out.println(node);
}
```
Using **iterative** strategy (Using two stack with printing 2nd stack)
```java
public static void postOrderTraversal(BinaryTreeNode node) {
	Stack<BinaryTreeNode> stack1 = new Stack<>();
	Stack<BinaryTreeNode> stack2 = new Stack<>();
	stack1.push(node);
	
	while(!stack1.isEmpty()) {
		node = stack1.pop();
		pushToStack(node, stack2);
		pushToStack(node.left, stack1);
		pushToStack(node.right, stack1);
	}
}

static void pushToStack(BinaryTreeNode node, Stack<BinaryTreeNode> stack) {
	while(node != null) {
		stack.push(node);
	}
}
```

## Questions
1. [Leetcode - 110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - A binary tree is said to be height-balanced if for each node in the tree, the difference in the height of its left and right subtrees is at most one.
2. [Leetcode - 101. Symmetric Tree](https://leetcode.com/problems/symmetric-tree/) - A binary tree is symmetric if you can draw a vertical line through the root and then the left subtree is the mirror image of the right subtree.
3. [Leetcode - 236. Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) - Any two nodes in a binary tree have a common ancestor, namely the root. The lowest common ancestor (LCA) of any two nodes in a binary tree is the node furthest from the root that is an ancestor of both nodes.
4. [Leetcode - 1022. Sum of Root To Leaf Binary Numbers](https://leetcode.com/problems/sum-of-root-to-leaf-binary-numbers/)
5. [Leetcode - 129. Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)
6. [Leetcode - 112. Path Sum](https://leetcode.com/problems/path-sum/) - Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.
7. [GeeksForGeeks - Find n-th node of inorder traversal](https://www.geeksforgeeks.org/find-n-th-node-inorder-traversal/)
8. [GeeksForGeeks - Inorder Successor of a node in Binary Tree](https://www.geeksforgeeks.org/inorder-succesor-node-binary-tree/)
9. Form a linked list from the leaves of a binary tree
10. [Find Leaves of Binary Tree](https://zhuhan0.blogspot.com/2017/05/leetcode-366-find-leaves-of-binary-tree.html)
11. [GeeksForGeeks - Boundary Traversal of binary tree](https://www.geeksforgeeks.org/boundary-traversal-of-binary-tree/)
