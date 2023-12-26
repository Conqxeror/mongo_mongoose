# Performing Queries with Mongoose

One of the key features of Mongoose is its powerful querying capabilities. With Mongoose, you can easily retrieve data from your MongoDB database using a flexible and expressive query API. This guide will walk you through the process of performing queries with Mongoose.

## Basic Queries

### Find Documents

To retrieve documents from a collection, you can use the `find` method:

```javascript
const User = require('../models/user');

// Find all users
User.find()
  .then(users => {
    console.log('All users:', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });
```

### Find Documents with a Condition

You can add conditions to your query using the `find` method:

```javascript
// Find users with age greater than 25
User.find({ age: { $gt: 25 } })
  .then(users => {
    console.log('Users with age greater than 25:', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });
```

## Advanced Queries

### Querying with Regular Expressions

Mongoose allows you to use regular expressions in your queries:

```javascript
// Find users with usernames starting with 'john'
User.find({ username: /^john/ })
  .then(users => {
    console.log('Users with usernames starting with "john":', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });
```

### Limiting and Sorting Results

You can limit and sort the results using the `limit` and `sort` methods:

```javascript
// Find the first two users, sorted by age in descending order
User.find()
  .limit(2)
  .sort({ age: -1 })
  .then(users => {
    console.log('First two users, sorted by age:', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });
```

## Combining Conditions

You can combine multiple conditions in a single query:

```javascript
// Find users with age greater than 25 and email ending with 'example.com'
User.find({ age: { $gt: 25 }, email: /example\.com$/ })
  .then(users => {
    console.log('Users with age greater than 25 and email ending with "example.com":', users);
  })
  .catch(err => {
    console.error('Error finding users:', err);
  });
```

## Conclusion

Performing queries with Mongoose is a flexible and intuitive process. Whether you need to find all documents, filter based on conditions, or sort and limit the results, Mongoose provides a rich set of tools to meet your querying needs. As you explore further, consider diving into Mongoose's aggregation framework for even more advanced querying and data manipulation.