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
