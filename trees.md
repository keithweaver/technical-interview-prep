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


### Helper.java
