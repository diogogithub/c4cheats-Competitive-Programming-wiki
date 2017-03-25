# Depth First Search

A depth first search (DFS) algorithm is used to traverse a graph. The best way to think about it is that it follows these steps:

1. I have a starting point and an ending point.
2. I go in a certain direction until I can't keep going that direction anymore.
3. If I can't go in that direction, I try a different direction, while making sure I haven't already been to the exact spot I will attempt to go to next.
4. If I can't go anywhere, I backtrack one step and try a different direction again, ruling out the places I've already been to.
5. I stop the program in two cases:
--I've reached my destination.
--I've been everywhere within my reach, but none of these are my destination.

Specifics on this algorithm's implementation vary from problem to problem, but it is useful to use in solutions that deal with traversing mazes, various paths, graphs, etc.

A typical algorithm would look like this:

    static int[] X = {1, 0, -1, 0};
    static int[] Y = {0, 1, 0, -1};

    static void dfs(int startX, int startY, int endX, int endY, char[][] graph, boolean[][] v){
                v[startX][startY] = true;
		if(startX == endX && startY == endY){
			return;
		}
		for(int i = 0; i < 4; i++){ //check all 4 cardinal directions
                        int nX = startX+X[i];
                        int nY = startY+Y[i];
			if(inBounds(nX, nY, graph){
                            if(!v[nX][nY]) dfs(nX, nY, endX, endY, graph, v);
                        }
		}
		return;
    }
    
    static boolean inBounds(int x, int y, char[][] graph){
        if(x >= 0 && y >= 0 && x < graph.length && y <= graph[0].length) return true;
        return false;
    }

This algorithm succesfuly traverses through the entire 2d array without going out of bounds and making sure not to get stuck revisiting already visited places.