Tree – an undirected graph without cycles
Spanning tree – a subtree that includes every vertex (ie. every vertex, but NOT every edge)
Minimum spanning tree – the spanning tree that has the lowest sum of its edge weights, compared to all other spanning trees (only exists for weighted graphs)
Disjoint set: a set of elements partitioned into a number of disjoint (non-overlapping) subsets

A problem involving these might be: Given a group of cities and the distance between them, what is the total amount of road you must lay so every city is connected, either directly or indirectly?

Kruskal’s algorithm takes the lowest Edge that hasn’t been used yet and connects the two nodes if they aren’t already indirectly connected.

First you need a class for the edges.
	class Edge implements Comparable<Edge> {
		int vertex1, vertex2, cost;
		public Edge(int v1, int v2, int c) {
			this.vertex1 = v1;
			this.vertex2 = v2;
			this.cost = c;
		}
		public int compareTo(Edge e) {
			return this.cost - e.cost;
		}
	}

Then, you need a DisjointSet class:
	class DisJointSet {
The value at index i is the index of the parent of node i.
		int parents[];
The number of levels of children nodes this node has. (For example, a node  with two children, each with no children, would have a height of 1.)
		int heights[];
	
		public DisJointSet(int numNodes) {
			this.parents = new int[numNodes];
			this.heights = new int[numNodes];
			for (int i = 0; i < numNodes; i++) {
				parents[i] = i;
			}
		}
	
The root is the highest node in a tree.
		int findRoot(int index) {
			while (parents[index] != index) {
				index = parents[index];
			}
		
			return index;
		}
	
Returns false if the union did not occur.
		boolean union(int index1, int index2) {
			int root1 = findRoot(index1);
			int root2 = findRoot(index2);
			if (root1 == root2) return false;
		
			if (heights[root1] < heights[root2]) {
	If the first node is part of the shorter tree, place the first tree directly under the root of the second tree.
				parents[root1] = root2;
			} else if (heights[root2] < heights[root1]) {

If the second node is part of the shorter tree, place the second tree directly under the root of the first tree.
parents[root2] = root1;
			} else {
If the trees are equal in height, it doesn’t matter which tree will join the other. The first tree joins the second, and the height of the second tree increases by 1.
				parents[root1] = root2;
				heights[root2]++;
			}
		
			return true;
		}
	}	

For the algorithm itself, you need a List of Edges. Then use this method:
	int mst(Edge[] edgeList, int numNodes) {
		DisJointSet djset = new DisJointSet(numNodes);
		int edgeCount = 0, mstWeight = 0, i = 0;
	
Sort the edges by their cost.
		Arrays.sort(edgeList);
	
		while (edgeCount < numNodes-1 && i < edgeList.length){
Try to add this edge in. (The union method will return false if both vertexes are part of the same tree.)
			if (djset.union(edgeList[i].vertex1, edgeList[i].vertex2)) {
				edgeCount++;
				mstWeight += edgeList[i].cost;
			}
			i++;
		}

		if (edgeCount < numNodes-1) {
If you didn't connect every vertex (ie. there are less than the number of nodes minus 1), a minimum spanning tree doesn't exist.
			return -1;
		}
		return mstWeight;
	}
