Iterative method to make an array for infinite layers of folders (folders inside folders inside folders, etc):

https://github.com/EhudKirsh/NodeJS-list-all-sub-directories-folders-Iterative-DFS/blob/c140abdb0e056638a7c2131be923e5d196846c7a/ListSubFolders.js#L1-L23

Use process.cwd() for Path if you want to check the current folder where the terminal is open.

This is a Depth First Search (DFS), not Breadth First Search (BFS). They both would work just as well, but the order is interesting to note!
![Image description](/BFS-and-DFS-Algorithms.png)
Note: this code is so good it even lists hidden folders! (and can be used for that purpose...) If it lists a folder you can't see, now you know why 😉
