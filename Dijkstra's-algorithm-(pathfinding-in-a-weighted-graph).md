Dijkstra’s algorithm finds the shortest path from a single index to every other index. It is faster than Floyd-Warshall when there is a single origin point. (Note: this algorithm is only useful if the graph is weighted. Otherwise, simply use a Breadth or Depth First Search.) This algorithm will fail if any of the edges have a negative weight.

The Vertex class is as follows. (Note: if you need to trace the path, you can add a prevIndex int and work backwards once the algorithm is done.)

	class Vertex implements Comparable<Vertex> {
		boolean visited;
		int index, distanceFromSource;
		ArrayList<Integer> neighbors;
	
		public Vertex(int index, int NO_EDGE) {
			this.index = index;
			this.distanceFromSource = NO_EDGE;
			this.neighbors = new ArrayList<Integer>();
		}
	
		void addNeighbor(int index) {
			this.neighbors.add(index);
		}
	
		@Override
		public int compareTo(Vertex v) {
			return this.distanceFromSource - v.distanceFromSource;
		}
	}

Before using the algorithm, you must create the Vertex array and scan in all the connections between the indexes and put them into a 2D array. If the value at index (i, j) does not equal NO_EDGE, then there is a connection. The value at index (i, i) will be zero. 

No_EDGE is a value larger than any possible value of an edge, while not overflowing if added to another value. Therefore, Integer.MAX_VALUE/2 – 5 should work in most cases.

	int numVertexes = scan.nextInt();
	Vertex[] vertexes = new Vertex[numVertexes];
	for (int i = 0; i < numVertexes; i++) {
		vertexes[i] = new Vertex(i);
	}
	
	int[][] costs = new int[numVertexes][numVertexes];
	for (int i = 0; i < numVertexes; i++) {
		Arrays.fill(costs[i], NO_EDGE);
		costs[i][i] = 0;
	}
		
	int numConnections = scan.nextInt();
	for (int i = 0; i < numConnections; i++) {
		int ver1 = scan.nextInt();
		int ver2 = scan.nextInt();
		int cost = scan.nextInt();
		costs[ver1][ver2] = cost;
		costs[ver2][ver1] = cost;
		vertexes[ver1].addNeighbor(ver2);
		vertexes[ver2].addNeighbor(ver1);
	}

Next, scan in the starting vertex (and ending vertex, if there's only one). Add it to the PriorityQueue.

	int sourceIndex = scan.nextInt();
	vertexes[sourceIndex].distanceFromSource = 0;
	PriorityQueue<Vertex> pq = new PriorityQueue<Vertex>();
	pq.add(vertexes[sourceIndex]);

Finally, the algorithm itself:

	while (!pq.isEmpty()) {
		Vertex curr = pq.poll();
		
If there’s a single known destination index, you can use a break statement here. Because of the PriorityQueue, you know that if you’ve reached the destination index, that’s the shortest path, unlike some versions of BFS and DFS.

		curr.visited = true;
		for (int i : curr.neighbors) {
			if (vertexes[i].visited) continue;
			
			int newDistance = curr.distanceFromSource + distances[curr.index][i];
			
			if(newDistance < vertexes[i].distanceFromSource){
				pq.remove(vertexes[i]);
				vertexes[i].distanceFromSource = newDistance;
				pq.add(vertexes[i]);
			}
		}
	}

The length of the shortest path from the source vertex to vertex j is vertexes[j].distanceFromSource.
