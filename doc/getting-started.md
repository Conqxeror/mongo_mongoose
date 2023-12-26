# Getting Started with MongoDB and Mongoose

Congratulations on successfully installing MongoDB and Mongoose! Now that you have the essentials set up, let's dive into the basics of working with MongoDB and Mongoose.

## MongoDB Basics

### Connecting to MongoDB

To start using MongoDB, you need to connect to a MongoDB server. Open a new terminal or command prompt and run the following command to connect to the local MongoDB instance:

```bash
mongo
```

This opens the MongoDB shell, allowing you to interact with the database.

### Creating a Database

In the MongoDB shell, you can create a new database using the following command:

```bash
use mydatabase
```

Replace "mydatabase" with the desired name for your database.

### Creating Collections

Collections in MongoDB are equivalent to tables in relational databases. You can create a new collection using the following command:

```bash
db.createCollection("mycollection")
```

Replace "mycollection" with the desired name for your collection.

## Mongoose Basics

Now, let's explore the basics of using Mongoose, the MongoDB object modeling tool for Node.js.

### Connecting to MongoDB with Mongoose

In your Node.js application, create a new file (e.g., `app.js`) and require Mongoose at the beginning:

```javascript
const mongoose = require('mongoose');
```

Next, connect to your MongoDB database using Mongoose:

```javascript
mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true });
```

Replace "mydatabase" with the name of your MongoDB database.

### Defining a Mongoose Schema

A Mongoose schema defines the structure of your documents. Create a simple schema for a "User" in your `app.js` file:

```javascript
const userSchema = new mongoose.Schema({
  username: String,
  email: String,
  age: Number,
});
```

### Creating a Mongoose Model

A Mongoose model is a wrapper for the schema. Create a model for the "User" schema:

```javascript
const User = mongoose.model('User', userSchema);
```

### Creating and Saving Documents

Now, you can create and save documents in your MongoDB database:

```javascript
const newUser = new User({
  username: 'john_doe',
  email: 'john@example.com',
  age: 25,
});

newUser.save((err, savedUser) => {
  if (err) return console.error(err);
  console.log('User saved:', savedUser);
});
```

This creates a new user and saves it to the "User" collection in MongoDB.

## Next Steps

Now that you've completed the basic setup and learned some fundamental MongoDB and Mongoose operations, you're ready to explore more advanced features. Check out the [MongoDB](docs/mongodb) and [Mongoose](docs/mongoose) sections for in-depth guides on various topics.

Feel free to experiment with creating more schemas, models, and documents. The key to mastering MongoDB and Mongoose is hands-on experience, so don't hesitate to build small projects or explore existing examples.

Happy coding!