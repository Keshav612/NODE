# NODE
//[{"title":"CLothes","body":"Sweater"},{"title":"Stationery","body":"Pen,Pencil"},{"title":"List","body":"All list"}]
// const chalk=require('chalk')
const yargs = require('yargs')
const notes = require('./notes')
// const getNotes=require('./notes.js');
// const note=getNotes();
// //const validator = require('validator');

// // console.log(validator.isEmail('keshav2.mishra@example.com')) //true
// // console.log(validator.isURL('google.com'))   //true
// // console.log(validator.isURL('www.google.com')) //true
// // console.log(validator.isEmail('keshav2.mishraexample.com')) //false
// // const msg=chalk.green.bold("Success !!");

// console.log(note);
// // console.log(msg);
// const G_msg=chalk.green.inverse('Success!!!!!')
// console.log(G_msg);



// const command = process.argv[2];;
// if(command == 'add')
// {
//     console.log("Adding");
// }
//console.log('Hello');
yargs.version('1.1.0')

yargs.command({
    command: 'add',
    describe: 'Adding a new note',
    builder:{
        title: {
            describe: 'Note title',
            demandOption: true,
            type: 'string'
        },
        body:{
            describe: 'Body of title',
            demandOption: true,
            type: 'string'
        }
    },
    handler: function(argv){

        notes.addNote(argv.title,argv.body)
    }
})

yargs.command({
    command: 'remove' ,
    describe: 'Remove a note',
    builder:{
        title:{
        describe: 'remove a note.',
        demandOption:true,
        type: 'string'
        }
    } ,
    handler: function(argv){
        notes.removeNote(argv.title)
    }
}) 

yargs.command({
    command: 'list',
    describe: 'Listing notes',
    handler: function(){
        console.log('Listed all notes...')
    }
})

yargs.command({
    command:'read',
    describe:'Reading a specific note',
    handler: function(){
        console.log('Read a note....')
    }

})
yargs.parse();
//console.log(yargs.argv);
--------------------------------
Notes.js
 const fs = require('fs')
const chalk = require('chalk')
 const addNote=function(title,body){

    const notes = loadNotes(); //for better approach so as to use while adding and removing.
    const duplicateNotes = notes.filter(function(note){
        return note.title === title
    })
        if(duplicateNotes.length === 0)
        {
            notes.push({
                title:title,
                body: body
            })
        
            saveNotes(notes)
        }
        else{
            console.log('Title taken !!!')
        }


}

 const saveNotes=function(notes){
     const dataJSON = JSON.stringify(notes)
     fs.writeFileSync('notes.json',dataJSON)
     

 }
 const loadNotes = function() {
     try{
        const dataBuffer = fs.readFileSync('notes.json')
        const dataJSON = dataBuffer.toString()
        return JSON.parse(dataJSON)
     }
     catch(e)
     {
        return [] 
     }
    
 }

 const removeNote = function(title){
     const notes=loadNotes()
     const notesToKeep = notes.filter(function(note){
         return note.title !== title
     })
     if(notes.length > notesToKeep.length)
     {
         console.log(chalk.green.inverse('Note removed'))
         saveNotes(notesToKeep)
     }
     else{
        console.log(chalk.red.inverse('Note not found'))
     }
     
 }

 module.exports = {
     addNote: addNote,
     removeNote:removeNote
 }

