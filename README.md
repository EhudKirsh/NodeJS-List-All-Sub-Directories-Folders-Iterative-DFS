Iterative method to make an array for infinite layers of folders (folders inside folders inside folders, etc):
```js
`use strict`
require('child_process').execSync('cls',{stdio:'inherit'})//console.clear(), but it always works!
console.log('Executed At: ',Date(),'\n')

const fs=require('fs')
,ListSubFolders=Path=>{
    let ToTest=fs.readdirSync(Path).filter(Item=>fs.lstatSync(Item).isDirectory())
    const SubFolders=[]
    while(ToTest.length!=0){
        const Folder=ToTest.at(-1);SubFolders.push(ToTest.pop())//DFS
        /*
            Depth First Search (DFS) is the default method because it uses .at(-1) & .pop() which are faster and more efficient because they check and remove items from the end and don't need to measure the length of an array and reindex each item when one is removed, unlike Breadth First Search (BFS) which uses [0] & .shift().
            Should you still wish to switch between the methods, I made it easy for you: just uncomment the line below and comment the line above
        */
        // const Folder=ToTest[0];SubFolders.push(ToTest.shift())//BFS

        let Contents=fs.readdirSync(Folder).filter(Item=>fs.lstatSync(`${Folder}/${Item}`).isDirectory())
        Contents=Contents.map(SubFolder=>SubFolder=`${Folder}/${SubFolder}`)
        ToTest=ToTest.concat(Contents).flat()
    }
    console.log(SubFolders.length+' folders across '+SubFolders.map(Path=>Path=Path.split('/').length).reduce((a,b)=>Math.max(a,b))+" layers inside the '"+process.cwd()+"' folder:\n",SubFolders)
    return SubFolders
}
ListSubFolders(process.cwd())
```
Use process.cwd() for Path if you want to check the current folder where the terminal is open.

Difference in order of searching and listing - BFS VS DFS:
![Image description](/BFS-and-DFS-Algorithms.png)
Note: this code is so good it even lists hidden folders! (and can be used for that purpose...) If it lists a folder you can't see, now you know why 😉
