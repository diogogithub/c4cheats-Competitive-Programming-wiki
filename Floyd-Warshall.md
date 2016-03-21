This algorithm finds the shortest path between all indexes of a weighted or unweighted graph. This will fail if there are any negative cycles (ie. the sum of the weights of the edges of the cycle is negative).

Before using the algorithm, you must scan in all the connections between the indexes and put them into a 2D array. If the value at index (i, j) does not equal NO_EDGE, then there is a connection. The value at index (i, i) will be zero. 

NO_EDGE is a value that’s greater than any possible value for a connection, while not overflowing if added to itself (this is because if two edges are set to NO_EDGE, they will be added together, and they can’t be allowed to overflow). Generally speaking, Integer.MAX_VALUE/2 – 5 should be acceptable.

	int[][] adj = new int[numNodes][numNodes];
	for (int j = 0; j < numNodes; j++) {
		Arrays.fill(adj[j], NO_EDGE);
		adj[j][j] = 0;
	}

	for (int i = 0; i < numConnections; i++) {
		int source = scan.nextInt();
		int dest = scan.nextInt();
		int cost = scan.nextInt();
	
		adj[source][dest] = cost;
	}

The path array is only used if you need to find the actual path from i to j. Once the algorithm has been run, the value at (i, j) is the index of the last vertex reached before j when travelling on the shortest path from i to j. For example, if the path from i to j is [i -> 5 -> 3 -> 2 -> j], the value at (i, j) will be 2. You construct the array with the previous vertex for each edge (ie. i) and use -1 to indicate no edge.

	int[] path = new int[numNodes];
	for (int i = 0; i < numNodes; i++) {
		for (int j = 0; j < numNodes; j++) {
			if (adj[i][j] == NO_EDGE) {
				path[i][j] = -1;
			} else {
				path[i][j] = i;
			}
		}
	}

Then you use the algorithm:

	for (int k = 0; k < len; k++) {
		for (int i = 0; i < len; i++) {
			for (int j = 0; j < len; j++) {
				if (adj[i][j] > adj[i][k] + adj[k][j]){
					adj[i][j] = adj[i][k] + adj[k][j];
					path[i][j] = path[k][j];
				}
			}
		}
	}

The algorithm runs though the adjacency array and changes the values so that the value at (i, j) is the cost of the shortest path from vertex i to vertex j.

To find the path from index i to index j using the path array, you need to work backwards. You can add them to an ArrayList, and then print it out backwards like so:

	ArrayList<Integer> indexes = new ArrayList<Integer>();
	indexes.add(end);

	while (path[start][end] != start) {
		indexes.add(path[start][end]);
		end = path[start][end];
	}
	indexes.add(start);
	
	for (int i = indexes.size()-1; i >= 0; i--) {
		System.out.print(indexes.get(i));
		if (i > 0) System.out.print(" -> ");
	}
	System.out.println();
