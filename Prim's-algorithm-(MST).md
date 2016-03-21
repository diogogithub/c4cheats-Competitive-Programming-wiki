Tree – an undirected graph without cycles
Spanning tree – a subtree that includes every vertex (ie. every vertex, but NOT every edge)
Minimum spanning tree – the spanning tree that has the lowest sum of its edge weights, compared to all other spanning trees (only exists for weighted graphs)
Disjoint set: a set of elements partitioned into a number of disjoint (non-overlapping) subsets

A problem involving these might be: Given a group of cities and the distance between them, what is the total amount of road you must lay so every city is connected, either directly or indirectly?

Prim’s algorithm only considers the edges connected to nodes already in the MST. Therefore only use Prim’s if you know all the nodes have edges that connect them.

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

In addition to the Edge class, you also need a Vertex class.
	class Vertex {
		ArrayList<Edge> edges;

		public Vertex() {
			this.edges = new ArrayList<Edge>();
		}
	}

And this is the algorithm itself.
	int numVertexes = scan.nextInt();
	int numEdges = scan.nextInt();

	boolean[] used = new boolean[numVertexes];
	Vertex[] vertexes = new Vertex[numVertexes];
	for (int j = 0; j < numVertexes; j++) {
		vertexes[j] = new Vertex();
	}
		
	for (int j = 0; j < numEdges; j++) {
		int ver1 = scan.nextInt();
		int ver2 = scan.nextInt();
		int cost = scan.nextInt();
		
		vertexes[ver1].edges.add(new Edge(ver1, ver2, cost));
		vertexes[ver2].edges.add(new Edge(ver2, ver1, cost));
	}
		
	PriorityQueue<Edge> pq = new PriorityQueue<Edge>();
		
We can start from any node, so starting from the first node is simplest.
	used[0] = true;
	pq.addAll(vertexes[0].edges);
	int mstWeight = 0;
		
	while (!pq.isEmpty()) {
		Edge current = pq.poll();
		
		if (used[current.vertex2]) continue;
			
		mstWeight += current.cost;
		used[current.vertex2] = true;
			
		pq.addAll(vertexes[current.vertex2].edges);
	}

