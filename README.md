<ins>What this programme does:</ins>

Open up a terminal in a certain folder and run this in NodeJS. It'll list (array []) in the console of all the folders inside that folder, and all the folders inside them, through infinite layers (folders inside folders inside folders, etc).

• The 'name' of each folder and subfolder is simply its relative path to the folder you ran this NodeJS programme from.

• This method is iterative, not recursive, to be most memory-efficient and fastest
```js
`use strict`
require('child_process').execSync('cls',{stdio:'inherit'})//console.clear(), but it always works!
console.log('Executed At: ',Date(),'\n')

const StartTime=performance.now()
,fs=require('fs')
,ListSubFolders=Path=>{
    let ToTest=fs.readdirSync(Path).filter(Item=>fs.lstatSync(Item).isDirectory())
    const SubFolders=[]
    while(ToTest.length>0){
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
    console.log('Run Time:',parseFloat(((performance.now()-StartTime)/1000).toFixed(3)),'s\n\n',SubFolders.length+' folders across '+SubFolders.map(Path=>Path=Path.split('/').length).reduce((a,b)=>Math.max(a,b))+" layers inside the '"+process.cwd()+"' folder:\n",SubFolders)
    return SubFolders
}
ListSubFolders(process.cwd())
```
Use process.cwd() for Path if you want to check the current folder where the terminal is open.

Difference in order of searching and listing - BFS VS DFS:

<img src='BFS-and-DFS-Algorithms.png' width='99%' height='99%'>

Note: this code is so good it even lists hidden folders! (and can be used for that purpose...) If it lists a folder you can't see, now you know why 😉
