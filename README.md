# NODE

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



// const command = process.argv[2];
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
        console.log('Read a note...')
    }

})
yargs.parse();
//console.log(yargs.argv);
