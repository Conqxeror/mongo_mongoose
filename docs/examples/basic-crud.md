# Basic CRUD Operations with MongoDB and Mongoose

In this guide, we'll explore how to perform basic CRUD (Create, Read, Update, Delete) operations using MongoDB and Mongoose, a powerful ODM (Object-Document Mapper) for Node.js.

## Setting Up Mongoose

First, make sure you have Mongoose installed. If not, you can install it using npm:

```bash
npm install mongoose
```

Now, let's set up a basic connection to a MongoDB database using Mongoose:

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true });

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'Connection error:'));
db.once('open', () => {
  console.log('Connected to the database');
});
```

Replace "mydatabase" with the name of your MongoDB database.

## Creating Documents

### Creating a Mongoose Model

Define a Mongoose model for your collection:

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  username: String,
  email: String,
  age: Number
});

const User = mongoose.model('User', userSchema);
```

### Inserting Documents

Now, you can create and save documents:

```javascript
const newUser = new User({
  username: 'john_doe',
  email: 'john@example.com',
  age: 25
});

newUser.save()
  .then(savedUser => {
    console.log('User saved:', savedUser);
  })
  .catch(err => {
    console.error('Error saving user:', err);
  });
```

## Reading Documents

### Finding Documents

You can retrieve documents using various methods, such as `find`, `findOne`, or querying by ID:

```javascript
// Find all users
User.find()
  .then(users => {
    console.log('All users:', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });

// Find a user by ID
const userId = 'your_user_id';
User.findById(userId)
  .then(user => {
    console.log('User by ID:', user);
  })
  .catch(err => {
    console.error('Error finding user:', err);
  });
```

## Updating Documents

Update documents using methods like `updateOne`, `updateMany`, or `findOneAndUpdate`:

```javascript
// Update a user by ID
const userIdToUpdate = 'your_user_id';
User.updateOne({ _id: userIdToUpdate }, { $set: { age: 26 } })
  .then(result => {
    console.log('Update result:', result);
  })
  .catch(err => {
    console.error('Error updating user:', err);
  });
```

## Deleting Documents

Delete documents using methods like `deleteOne`, `deleteMany`, or `findByIdAndDelete`:

```javascript
// Delete a user by ID
const userIdToDelete = 'your_user_id';
User.deleteOne({ _id: userIdToDelete })
  .then(result => {
    console.log('Delete result:', result);
  })
  .catch(err => {
    console.error('Error deleting user:', err);
  });
```

## Conclusion

This guide provides a basic overview of performing CRUD operations with MongoDB and Mongoose in a Node.js environment. As you continue building your application, explore more advanced features of Mongoose, such as middleware, validation, and population, to enhance your MongoDB data interactions.