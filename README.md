<ins>What this programme does:</ins>

Open up a terminal in a certain folder and run this in NodeJS.

<img src='Example Folder.jpg' width='99%' height='99%'>
<img src='Terminal Command Line.jpg' width='99%' height='99%'>

It'll list (array []) in the console of all the folders inside that folder, and all the folders inside them, through infinite layers (folders inside folders inside folders, etc). The 'name' of each folder and subfolder is simply its relative path to the folder you ran this NodeJS programme from.

<img src='Terminal Outcome.jpg' width='99%' height='99%'>

This method is iterative, not recursive, to be most memory-efficient and fastest
```js
`use strict`
require('child_process').execSync('cls',{stdio:'inherit'})//console.clear(), but it always works!
console.log('Executed at: ',Date(),'\n')

const StartTime=performance.now()
,fs=require('fs')
,MaxOccurance=(c,A)=>{// largest number of occurances of a character c in any string in array A
    let L=A.length,m=A[--L].split(c).length-1
    while(--L>=0){
        const n=A[L].split(c).length-1
        n>m&&(m=n)
    }
    return m
}// e.g. MaxOccurance('/',['Folder','Folder/inside folder','Folder/inside folder/another nested folder']) ➜ 2
,ListSubFolders=Path=>{
    let ToTest=fs.readdirSync(Path).filter(Item=>fs.lstatSync(Item).isDirectory())
    ,i=ToTest.length,L=i;const SubFolders=[]
    while(--i>=0){
        const Folder=ToTest.at(-1);SubFolders.push(ToTest.pop())//DFS
        /*
            Depth First Search (DFS) is the default method because it uses .at(-1) & .pop() which are faster and more efficient because they check and remove items from the end and don't need to measure the length of an array and reindex each item when one is removed, unlike Breadth First Search (BFS) which uses [0] & .shift().
            Should you still wish to switch between the methods, I made it easy for you: just uncomment the line below and comment the line above
        */
        // const Folder=ToTest[0];SubFolders.push(ToTest.shift())//BFS

        let Contents=fs.readdirSync(Folder).filter(Item=>fs.lstatSync(`${Folder}/${Item}`).isDirectory())
        const j=Contents.length;i+=j;L+=j
        for(let k=-1;++k<j;)
            ToTest.push(`${Folder}/${Contents[k]}`)// Contents[k] = SubFolder
    }
    console.log(L,'folders across',1+MaxOccurance('/',SubFolders),"layers inside the '"+process.cwd()+"' folder:\n",SubFolders,'\n\n'+'Run time:',Number(((performance.now()-StartTime)/1000).toFixed(3)),'s\n')
}
ListSubFolders(process.cwd())
```
Use process.cwd() for Path if you want to check the current folder where the terminal is open.

Difference in order of searching and listing - BFS VS DFS:

<img src='BFS-and-DFS-Algorithms.png' width='99%' height='99%'>

Note: this code is so good it even lists hidden folders! (and can be used for that purpose...) If it lists a folder you can't see, now you know why 😉
