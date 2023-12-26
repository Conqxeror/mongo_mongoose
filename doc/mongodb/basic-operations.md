# Basic CRUD Operations in MongoDB

MongoDB supports the fundamental CRUD (Create, Read, Update, Delete) operations for managing data. In this guide, you'll learn how to perform these operations using the MongoDB shell and Mongoose.

## MongoDB Shell

### 1. Create (Insert) Operation

To insert a document into a collection, use the `insertOne` or `insertMany` method:

```javascript
db.users.insertOne({
  username: 'john_doe',
  email: 'john@example.com',
  age: 25
});
```

### 2. Read (Query) Operation

To query documents in a collection, use the `find` method:

```javascript
db.users.find({ username: 'john_doe' });
```

### 3. Update Operation

To update a document in a collection, use the `updateOne` or `updateMany` method:

```javascript
db.users.updateOne(
  { username: 'john_doe' },
  { $set: { age: 26 } }
);
```

### 4. Delete Operation

To delete a document from a collection, use the `deleteOne` or `deleteMany` method:

```javascript
db.users.deleteOne({ username: 'john_doe' });
```

## Mongoose

Now, let's see how to perform these basic CRUD operations using Mongoose in a Node.js application.

### 1. Create (Insert) Operation

```javascript
const User = require('../models/user');

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

### 2. Read (Query) Operation

```javascript
const User = require('../models/user');

User.find({ username: 'john_doe' })
  .then(users => {
    console.log('Found users:', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });
```

### 3. Update Operation

```javascript
const User = require('../models/user');

User.updateOne(
  { username: 'john_doe' },
  { $set: { age: 26 } }
)
  .then(result => {
    console.log('Update result:', result);
  })
  .catch(err => {
    console.error('Error updating user:', err);
  });
```

### 4. Delete Operation

```javascript
const User = require('../models/user');

User.deleteOne({ username: 'john_doe' })
  .then(result => {
    console.log('Delete result:', result);
  })
  .catch(err => {
    console.error('Error deleting user:', err);
  });
```

These examples provide a basic understanding of how to perform CRUD operations in MongoDB using both the MongoDB shell and Mongoose in a Node.js application. Feel free to adapt these examples to fit the structure of your project and explore more advanced MongoDB features as you continue learning.