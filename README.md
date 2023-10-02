Iterative method to make an array for infinite layers of folders (folders inside folders inside folders, etc):

```js
`use strict`
require('child_process').execSync('cls',{stdio:'inherit'})//console.clear(), but it always works!
console.log('Executed At: '+Date()+'\n')

const fs=require('fs')
,ListSubFolders=Path=>{
    let ToTest=fs.readdirSync(Path).filter(Item=>fs.lstatSync(Item).isDirectory())
    const SubFolders=[]
    while(ToTest.length!=0){
        const Folder=ToTest.at(-1)
        SubFolders.push(ToTest.pop())

        let Contents=fs.readdirSync(Folder).filter(Item=>fs.lstatSync(`${Folder}/${Item}`).isDirectory())
        Contents=Contents.map(SubFolder=>SubFolder=`${Folder}/${SubFolder}`)

        ToTest=ToTest.concat(Contents).flat()
    }
    console.log(SubFolders)
    return SubFolders
}
ListSubFolders(process.cwd())

module.exports={ListSubFolders}
```

Use process.cwd() for Path if you want to check the current folder where the terminal is open.

This is a Depth First Search (DFS), not Breadth First Search (BFS). They both would work just as well, but the order is interesting to note!

![Image description](/BFS-and-DFS-Algorithms.png)
