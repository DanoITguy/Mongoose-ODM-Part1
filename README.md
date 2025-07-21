What You'll Do
Install Mongoose ODM and connect to a MongoDB server.
Learn how to define Mongoose schemas, then use them to define Mongoose models.
Learn to perform database operations with Mongoose methods.


Instructions
Install Mongoose
From inside the course folder (5-NodeJS-Express-MongoDB), create a new subfolder named node-mongoose and open that folder in VS Code.
Create a package.json file in the node-mongoose folder with the content as follows:
{
    "name": "node-mongoose",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index"
    }
}
Optional: If you are using nodemon, update the start script accordingly.
In this folder, install Mongoose by typing the following at the prompt:
npm install mongoose@8.4.0


Implement a Node application
Create a sub-folder named models in the node-mongoose folder.
Create a file in the models folder named campsite.js and add the following code to create a Mongoose schema:
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const campsiteSchema = new Schema({
    name: {
        type: String,
        required: true,
        unique: true
    },
    description: {
        type: String,
        required: true
    }
}, {
    timestamps: true
});

const Campsite = mongoose.model('Campsite', campsiteSchema);

module.exports = Campsite;
In the node-mongoose folder, create a file named index.js with the following code:
const mongoose = require('mongoose');
const Campsite = require('./models/campsite');

const url = 'mongodb://127.0.0.1:27017/nucampsite';
const connect = mongoose.connect(url, {});

connect.then(() => {

    console.log('Connected correctly to server');

    const newCampsite = new Campsite({
        name: 'React Lake Campground',
        description: 'test'
    });

    newCampsite.save()
    .then(campsite => {
        console.log(campsite);
        return Campsite.find();
    })
    .then(campsites => {
        console.log(campsites);
        return Campsite.deleteMany();
    })
    .then(() => {
        return mongoose.connection.close();
    })
    .catch(err => {
        console.log(err);
        mongoose.connection.close();
    });
});



Start the MongoDB server
You started the MongoDB server in the Introduction to MongoDB exercise. If it is still running, skip to the next section.
If you have closed it since then, you will need to start it again: Open a bash terminal to the 5-NodeJS-Express-MongoDB/mongodb folder and run this command:
mongod --dbpath=data
Make sure that you are in the mongodb folder when you run this command. Leave the server running in this bash terminal.
Optional:
If using Git, create a .gitignore file with the text content of node_modules in the node-mongoose folder.
Initialize a Git repository and commit your files with the message "Mongoose Part 1".
git add .
git commit -m "Mongoose Part 1"


Summary
In this exercise, you learned about the Mongoose module and used it to create schemas as well as interact with the MongoDB server.


Additional Resources
Mongoose
TutsPlus - An Introduction to Mongoose for MongoDB and Node.js
Heroku Dev Center - Object Modeling in Node.js with Mongoose
