Iterative method to make an array for infinite layers of folders (folders inside folders inside folders, etc):
code-reference-in-readme/src/ListSubFolders.js
Use process.cwd() for Path if you want to check the current folder where the terminal is open.

This is a Depth First Search (DFS), not Breadth First Search (BFS). They both would work just as well, but the order is interesting to note!
![Image description](/BFS-and-DFS-Algorithms.png)
