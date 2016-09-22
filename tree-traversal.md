# Tree Traversal

### Breadth First Search

- First in, first out of the queue (or stack)
- Does not matter which edge you go to but visit all edges on the level before moving on
- When "e" has no edges, remove from queue

```
* <-- where we are
```

```
Order:E
Queue:E
	*
    |
    E
  / |  \
B   C   G
| /   \ |
A      D
|
F
|
H

Order:E
Queue:EBCG
	
    |
    E*
  / |  \
B   C   G
| /   \ |
A      D
|
F
|
H

Order:EB
Queue:BCGA
	
    |
    E
  / |  \
B*  C   G
| /   \ |
A      D
|
F
|
H

Order:EB
Queue:CGA
	
    |
    E*
  / |  \
B   C   G
| /   \ |
A      D
|
F
|
H

Order:EBC
Queue:CGAD
	
    |
    E
  / |  \
B   C*   G
| /   \ |
A      D
|
F
|
H

Order:EBC
Queue:GAD
	
    |
    E*
  / |  \
B   C   G
| /   \ |
A      D
|
F
|
H

Order:EBC
Queue:AD
	
    |
    E
  / |  \
B   C   G*
| /   \ |
A      D
|
F
|
H

~Skipped a few steps of moving over~

Order:EBCGA
Queue:ADF
	
    |
    E
  / |  \
B   C   G
| /   \ |
A*      D
|
F
|
H


Order:EBCGAD
Queue:DF
	
    |
    E
  / |  \
B   C   G
| /   \ |
A      D*
|
F
|
H

Order:EBCGADF
Queue:FH
	
    |
    E
  / |  \
B   C   G
| /   \ |
A      D
|
F*
|
H

Order:EBCGADFH
Queue:H
	
    |
    E
  / |  \
B   C   G
| /   \ |
A      D
|
F
|
H*

```


https://www.youtube.com/watch?v=we2xFCPkH0Y
https://www.youtube.com/watch?v=bIA8HEEUxZI
