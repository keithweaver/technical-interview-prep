# Trees

## Binary Trees

Example:
```
		  [6]
	  [1]    [3]
	[2][4]  [4][2]
```
- Can have at most two childern
- Bottom nodes are "leafs"
- Perfect Binary tree is all spots filled
- Height of binary tree is the longest path from leaf to root
- Max number of nodes is 2^n - 1 (n being the number of levels)

Speed of:
Insert ___
Delete ___
Search ___

```
static Node tree;

public static void main(String[] args) {
	Integer[] testInts = Helper.generateTestIntegerList();
	Helper.printArrayOfIntegers(testInts);
	
	createBinaryTree(testInts);
}
public static void createBinaryTree(Integer[] testInts){
	if(testInts == null || testInts.length == 0){
		tree = null;
	}else{
		tree = new Node(testInts[0]);
		for(int i = 1;i < testInts.length;i++){
			tree = insert(tree, testInts[i]);
		}
	}
	System.out.println(tree.getKey());
	printPath(tree);
}
public static void printPath(Node currentNode){
	System.out.println("Current Value:" + currentNode.getKey());
	if(currentNode.getLeftChild() != null){
		System.out.println("Going down the left child of " + currentNode.getKey());
		printPath(currentNode.getLeftChild());
	}
	if(currentNode.getRightChild() != null){
			System.out.println("Going down the right child of " + currentNode.getKey());
		printPath(currentNode.getRightChild());
	}
}
	
public static Node insert(Node currentNode, int valueBeingInserted){
	if(valueBeingInserted <= currentNode.getKey() && currentNode.getLeftChild() == null){
		//create new left root
		Node newLeaf = new Node(valueBeingInserted);
		currentNode.setLeftChild(newLeaf);
	}else if(valueBeingInserted > currentNode.getKey() && currentNode.getRightChild() == null){
		//create new right root
		Node newLeaf = new Node(valueBeingInserted);
		currentNode.setRightChild(newLeaf);
	}else if(valueBeingInserted <= currentNode.getKey() && currentNode.getLeftChild() != null){
		//Go down the left tree
		Node leftTree = insert(currentNode.getLeftChild(), valueBeingInserted);
			currentNode.setLeftChild(leftTree);
	}else if(valueBeingInserted > currentNode.getKey() && currentNode.getRightChild() != null){
		//Go down the right tree
		Node rightTree = insert(currentNode.getRightChild(), valueBeingInserted);
		currentNode.setRightChild(rightTree);
	}
	return currentNode;
}
```


## Nary Trees

?????

## Tries

Complexity: Constant time
- No Collisions
- There is a root and leafs

Example:
```
      [1]
  [1][2][3][4][5][6][7][8][9]

```

Example #2:
Given:
```
32400
38718
31240
87770
89313
```

Diagram:
```
				        {}
                        [3|8]
    {}                                      {}
    [2|8|1]                                 [7|9]

{32400}   {38718}   {31240}          {87770}        {89313}
[]        []		[]               []             []
```

Can put the numbers at the bottom because there is no numbers following the same pattern. Ex. There is only one 32... and only one 38...


Example #2 (Variable Length):
Given:
```
32400
38718
31240
87770
89313
893 <-- add a # meaning ending character
```
Diagram:
```
				        {}
                        [3|8]
    {}                                      {}
    [2|8|1]                                 [7|9]

{32400}   {38718}   {31240}          {87770}        {}
[]        []		[]               []             [1|#]
												{89313}     {839}
												[]          []
```

Height of the trie is the longest character.

Worst Case: O(n)

Speed of:
Insert ___
Delete ___
Search ___

https://www.youtube.com/watch?v=RIUY7ieyH40


## Balance Binary Tree

- A node, all the left nodes are lesser than root
- A node, all the right nodes are higher or equal than root
- Difference between the two sub trees cannot be greater than 1

Speed of:
Insert ___
Delete ___
Search ___

https://www.youtube.com/watch?v=uZueM4b9qA0
https://www.youtube.com/watch?v=pYT9F8_LFTM


## Red Black Tree
- All leaves are red or black
- All leaves are black
- Root node is always black
- There is no path from root to leaf where two reds are in a row
- Tree is fixed by recolouring
- Each route from the root to the leaves has the same number of black nodes

Insert "10"
```
		[B:10]
```
Insert "12"
```
		[B:10]
			 [R:12]
```
Insert "11"
```
		[B:10]
			 [R:12]
		   [R:11]
```

Readjust for "11"
```
		[B:10]
			 [R:11]
		        [R:12]
```

Still not okay, readjust again for "11"
```
		[R:11]
	[B:10] [R:12]
```

Fix colors
```
		[B:11]
	[R:10] [R:12]
```

Add an "100"
```
		[B:11]
	[R:10] [R:12]
			    [R:100]
```

Fix coloring
```
		[B:11]
	[B:10] [B:12]
			    [R:100]
```

Make all new nodes red

Case:
- Add a root <-- make it black

Case #2:
- Add a new node and the parent is black (Leave it)

Case #3:
- Parent and Uncle are red.
- Add a new red node
- Change the parent to black
- Change the uncle to black
- Change the grandparent to red
- Recursively call this grandparent

Case #4:
- Uncle is black
- Parent and new node are red
- Rotate left or right depending
- Call rotate on parent which moves the new node up
- Recursively call rotate on the P after, it will use Case #5

```
		G                  G
	P		U      or    U    P
	  N                      N
```
RESULT:
```
          G                G
     N        U    or  U        N
   P                               P
```

Case #5:
- Uncle is black 
- Parent is left and node is left
- Switch parent and grandparent colors
- Rotation through grandparent

```
		G                  G
	P		U      or    U    P
  N                             N
```

RESULT:
```
		P                  P
	N		G      or    G    N
               U        U      
```

https://www.youtube.com/watch?v=tJ7niBAhDQI
https://www.youtube.com/watch?v=m9tse9Gr2pE



## Splay Tree

## AVL Tree
- BST
- We control the depth so doesnt get to big
- Left sub tree and right sub tree cant differ for more than 1
- Insert, delete, search all in O(log n)
- One rotation, double rotation
- Rotate because there cant be difference more than one (so... 2)
- One rotation you use the zig-zig pattern
- Two rotations for the zig-zag pattern

```
	ZigZig       ZigZag
           x           x
          /           /
         y           y
       	/             \
       z               z
```

Example (ZigZig):
```
			4           5
		   /           / \
		  5           4   6
		/
	   6
```

Example:
```
 4          4              6
  \          \            / \
   6   =>     6    =>    4   5
  /            \
 5              5
```

https://www.youtube.com/watch?v=9X3pIIhNi_w

http://blog.blackbam.at/2012/05/04/avl-tree-implementation-in-java/

```

public class AvlNode {

	int value;
	AvlNode leftChild;
	AvlNode rightChild;
	AvlNode parent;
	int balance;
	
	public AvlNode(int value){
		super();
		this.value = value;
		this.leftChild = null;
		this.rightChild = null;
		this.parent = null;
		this.balance = 0;
	}
	
	public AvlNode(int value, AvlNode leftChild, AvlNode rightChild, AvlNode parent, int balance) {
		super();
		this.value = value;
		this.leftChild = leftChild;
		this.rightChild = rightChild;
		this.parent = parent;
		this.balance = balance;
	}

	public int getValue() {
		return value;
	}

	public void setValue(int value) {
		this.value = value;
	}

	public AvlNode getLeftChild() {
		return leftChild;
	}

	public void setLeftChild(AvlNode leftChild) {
		this.leftChild = leftChild;
	}

	public AvlNode getRightChild() {
		return rightChild;
	}

	public void setRightChild(AvlNode rightChild) {
		this.rightChild = rightChild;
	}

	public AvlNode getParent() {
		return parent;
	}

	public void setParent(AvlNode parent) {
		this.parent = parent;
	}

	public int getBalance() {
		return balance;
	}

	public void setBalance(int balance) {
		this.balance = balance;
	}
	
}
```

```

public class AVLTree {

	protected AvlNode root; // the root node

	/*****************************
	 * Core Functions
	 ************************************/

	/**
	 * Add a new element with key "k" into the tree.
	 * 
	 * @param k
	 *            The key of the new node.
	 */
	public void insert(int k) {
		// create new node
		AvlNode n = new AvlNode(k);
		// start recursive procedure for inserting the node
		insertAVL(this.root, n);
	}

	/**
	 * Recursive method to insert a node into a tree.
	 * 
	 * @param p
	 *            The node currently compared, usually you start with the root.
	 * @param q
	 *            The node to be inserted.
	 */
	public void insertAVL(AvlNode p, AvlNode q) {
		// If node to compare is null, the node is inserted. If the root is
		// null, it is the root of the tree.
		if (p == null) {
			this.root = q;
		} else {

			// If compare node is smaller, continue with the left node
			if (q.getValue() < p.getValue()) {
				if (p.getLeftChild() == null) {
					p.setLeftChild(q);
					q.parent = p;

					// Node is inserted now, continue checking the balance
					recursiveBalance(p);
				} else {
					insertAVL(p.getLeftChild(), q);
				}

			} else if (q.getValue() > p.getValue()) {
				if (p.getRightChild() == null) {
					p.setRightChild(q);
					q.parent = p;

					// Node is inserted now, continue checking the balance
					recursiveBalance(p);
				} else {
					insertAVL(p.getRightChild(), q);
				}
			} else {
				// do nothing: This node already exists
			}
		}
	}

	/**
	 * Check the balance for each node recursivly and call required methods for
	 * balancing the tree until the root is reached.
	 * 
	 * @param cur
	 *            : The node to check the balance for, usually you start with
	 *            the parent of a leaf.
	 */
	public void recursiveBalance(AvlNode cur) {

		// we do not use the balance in this class, but the store it anyway
		setBalance(cur);
		int balance = cur.balance;

		// check the balance
		if (balance == -2) {

			if (height(cur.getLeftChild().getLeftChild()) >= height(cur.getLeftChild().getRightChild())) {
				cur = rotateRight(cur);
			} else {
				cur = doubleRotateLeftRight(cur);
			}
		} else if (balance == 2) {
			if (height(cur.getRightChild().getRightChild()) >= height(cur.getRightChild().getLeftChild())) {
				cur = rotateLeft(cur);
			} else {
				cur = doubleRotateRightLeft(cur);
			}
		}

		// we did not reach the root yet
		if (cur.parent != null) {
			recursiveBalance(cur.parent);
		} else {
			this.root = cur;
			System.out.println("------------ Balancing finished ----------------");
		}
	}

	/**
	 * Removes a node from the tree, if it is existent.
	 */
	public void remove(int k) {
		// First we must find the node, after this we can delete it.
		removeAVL(this.root, k);
	}

	/**
	 * Finds a node and calls a method to remove the node.
	 * 
	 * @param p
	 *            The node to start the search.
	 * @param q
	 *            The KEY of node to remove.
	 */
	public void removeAVL(AvlNode p, int q) {
		if (p == null) {
			// der Wert existiert nicht in diesem Baum, daher ist nichts zu tun
			return;
		} else {
			if (p.getValue() > q) {
				removeAVL(p.getLeftChild(), q);
			} else if (p.getValue() < q) {
				removeAVL(p.getRightChild(), q);
			} else if (p.getValue() == q) {
				// we found the node in the tree.. now lets go on!
				removeFoundNode(p);
			}
		}
	}

	/**
	 * Removes a node from a AVL-Tree, while balancing will be done if
	 * necessary.
	 * 
	 * @param q
	 *            The node to be removed.
	 */
	public void removeFoundNode(AvlNode q) {
		AvlNode r;
		// at least one child of q, q will be removed directly
		if (q.getLeftChild() == null || q.getRightChild() == null) {
			// the root is deleted
			if (q.parent == null) {
				this.root = null;
				q = null;
				return;
			}
			r = q;
		} else {
			// q has two children --> will be replaced by successor
			r = successor(q);
			q.setValue(r.getValue());
		}

		AvlNode p;
		if (r.getLeftChild() != null) {
			p = r.getLeftChild();
		} else {
			p = r.getLeftChild();
		}

		if (p != null) {
			p.setParent(r.getParent());
		}

		if (r.getParent() == null) {
			this.root = p;
		} else {
			if (r == r.getParent().getLeftChild()) {
				r.getParent().getLeftChild().setParent(p);
				;
			} else {
				r.getParent().setRightChild(p);
			}
			// balancing must be done until the root is reached.
			recursiveBalance(r.getParent());
		}
		r = null;
	}

	/**
	 * Left rotation using the given node.
	 * 
	 * 
	 * @param n
	 *            The node for the rotation.
	 * 
	 * @return The root of the rotated tree.
	 */
	public AvlNode rotateLeft(AvlNode n) {

		AvlNode v = n.getRightChild();
		v.setParent(n.getParent());

		n.setRightChild(v.getLeftChild());

		if (n.getRightChild() != null) {
			n.getRightChild().setParent(n);
		}

		v.setLeftChild(n);
		n.setParent(v);

		if (v.getParent() != null) {
			if (v.getParent().getRightChild() == n) {
				v.getParent().setRightChild(v);
			} else if (v.getParent().getLeftChild() == n) {
				v.getParent().setParent(v);
			}
		}

		setBalance(n);
		setBalance(v);

		return v;
	}

	/**
	 * Right rotation using the given node.
	 * 
	 * @param n
	 *            The node for the rotation
	 * 
	 * @return The root of the new rotated tree.
	 */
	public AvlNode rotateRight(AvlNode n) {

		AvlNode v = n.getLeftChild();
		v.setParent(n.getParent());

		n.setLeftChild(v.getRightChild());

		if (n.getLeftChild() != null) {
			n.getLeftChild().setParent(n);
		}

		v.setRightChild(n);
		n.setParent(v);

		if (v.parent != null) {
			if (v.getParent().getRightChild() == n) {
				v.getParent().setParent(v);
			} else if (v.getParent().getLeftChild() == n) {
				v.getParent().setLeftChild(v);
			}
		}

		setBalance(n);
		setBalance(v);

		return v;
	}

	/**
	 * 
	 * @param u
	 *            The node for the rotation.
	 * @return The root after the double rotation.
	 */
	public AvlNode doubleRotateLeftRight(AvlNode u) {
		u.setLeftChild(rotateLeft(u.getLeftChild()));
		return rotateRight(u);
	}

	/**
	 * 
	 * @param u
	 *            The node for the rotation.
	 * @return The root after the double rotation.
	 */
	public AvlNode doubleRotateRightLeft(AvlNode u) {
		u.setRightChild(rotateRight(u.getRightChild()));
		return rotateLeft(u);
	}

	/*****************************
	 * Helper Functions
	 ************************************/

	/**
	 * Returns the successor of a given node in the tree (search recursivly).
	 * 
	 * @param q
	 *            The predecessor.
	 * @return The successor of node q.
	 */
	public AvlNode successor(AvlNode q) {
		if (q.getRightChild() != null) {
			AvlNode r = q.getRightChild();
			while (r.getLeftChild() != null) {
				r = r.getLeftChild();
			}
			return r;
		} else {
			AvlNode p = q.parent;
			while (p != null && q == p.getRightChild()) {
				q = p;
				p = q.parent;
			}
			return p;
		}
	}

	/**
	 * Calculating the "height" of a node.
	 * 
	 * @param cur
	 * @return The height of a node (-1, if node is not existent eg. NULL).
	 */
	private int height(AvlNode cur) {
		if (cur == null) {
			return -1;
		}
		if (cur.getLeftChild() == null && cur.getRightChild() == null) {
			return 0;
		} else if (cur.getLeftChild() == null) {
			return 1 + height(cur.getRightChild());
		} else if (cur.getRightChild() == null) {
			return 1 + height(cur.getLeftChild());
		} else {
			return 1 + maximum(height(cur.getLeftChild()), height(cur.getRightChild()));
		}
	}

	/**
	 * Return the maximum of two integers.
	 */
	private int maximum(int a, int b) {
		if (a >= b) {
			return a;
		} else {
			return b;
		}
	}

	private void setBalance(AvlNode cur) {
		cur.balance = height(cur.getRightChild()) - height(cur.getLeftChild());
	}

}
```

### Helper.java
