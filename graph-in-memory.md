# Graph in Memory

3 ways to represent graphs:
1. Objects and pointers
2. Adjacency matrix
3. Adjacency lists



From the top of my head, I hope I have the facts correct.


Conceptually, graph tries to represent how a set of nodes (or vertices) are related (connected) to each other (via edges). However, in actual physical device (memory), we have a continuous array of memory cell.


So, in order to represent the graph, we can choose to use a matrix. In this case, we use the vertex index as the row and column and the entry has value 1 if the vertices are adjacent to each other, 0 otherwise.


Alternatively, you can also represent a graph by allocating an object to represent the node/vertex which points to a list of all the nodes that are adjacent to it.


The matrix representation gives the advantage when the graph is dense, meaning when most of the nodes/vertices are connected to each other. This is because in such cases, by using the entry of matrix, it saves us from having to allocate an extra pointer (which need a word size memory) for each connection.


For sparse graph, the list approach is better because you don't need to account for the 0 entries when there is no connection between the vertices.


##### Storing nodes as objects with pointers to one another
- The memory complexity for this approach is O(n) because you have as many objects as you have nodes. The number of pointers (to nodes) required is up to O(n^2) as each node object may contain pointers for up to n nodes.
- The time complexity for this data structure is O(n) for accessing any given node.

##### Storing a matrix of edge weights
- This would be a memory complexity of O(n^2) for the matrix.
- The advantage with this data structure is that the time complexity to access any given node is O(1).


Adjacency List
```
class Graph {
    //Map of adjacency lists for each node
    Map<Integer, List<Integer>> adj;

    public Graph(int[] nodes) {
        //your node labels are consecutive integers starting with one. 
        //to make the indexing easier we will allocate an array of adjacency one element larger than necessary
        adj = new HashMap<Integer, LinkedList<Integer>>();
        for (int i = 0; i < nodes.length; ++i) {
            adj.put(i, new LinkedList<Integer>());
        }
    }

    public addNeighbor(int v1, int v2) {
        adj.get(v1).add(v2);
    }

    public List<Integer> getNeighbors(int v) {
        return adj.get(v);
    }

}
```
```
g.addNeighbor(v1, v2);
g.addNeighbor(v2, v1);
```



http://stackoverflow.com/questions/3287003/three-ways-to-store-a-graph-in-memory-advantages-and-disadvantages
http://stackoverflow.com/questions/27809894/object-and-pointer-graph-representations
https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs
http://stackoverflow.com/questions/8542523/adjacency-list-for-undirected-graph