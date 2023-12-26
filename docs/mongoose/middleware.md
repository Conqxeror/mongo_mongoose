# Mongoose Middleware

Mongoose middleware functions allow you to execute custom logic before or after specific events in the lifecycle of a document. These events include actions like saving, updating, and removing documents. Middleware provides a powerful way to implement business logic, perform validations, and execute tasks in response to certain events.

## Types of Middleware

### 1. Document Middleware

Document middleware (also known as "pre" and "post" hooks) are functions that execute before or after specific document methods, such as `save`, `updateOne`, and `remove`.

#### Example: Pre-Save Middleware

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  username: String,
  email: String,
  age: Number
});

userSchema.pre('save', function (next) {
  // Custom logic before saving a user document
  console.log('Saving user...');
  next();
});

const User = mongoose.model('User', userSchema);
```

### 2. Query Middleware

Query middleware allows you to intercept and modify queries before they are executed. This can be useful for adding additional conditions or validations to queries.

#### Example: Pre-Find Middleware

```javascript
userSchema.pre('find', function () {
  // Custom logic before executing a find query
  console.log('Executing find query...');
});

// Now, when you execute a find query, the pre-find middleware will run
User.find({ age: { $gt: 25 } }, (err, users) => {
  if (err) {
    console.error('Error finding users:', err);
  } else {
    console.log('Users with age greater than 25:', users);
  }
});
```

### 3. Aggregate Middleware

Aggregate middleware functions execute before or after an aggregation operation. This allows you to manipulate the data during the aggregation process.

#### Example: Post-Aggregate Middleware

```javascript
userSchema.post('aggregate', function (result) {
  // Custom logic after executing an aggregate operation
  console.log('Aggregate result:', result);
});

// Now, when you execute an aggregate operation, the post-aggregate middleware will run
User.aggregate([
  { $match: { age: { $gt: 25 } } },
  { $group: { _id: '$age', count: { $sum: 1 } } }
]).exec((err, result) => {
  if (err) {
    console.error('Error aggregating users:', err);
  } else {
    console.log('Aggregate result:', result);
  }
});
```

## Middleware Execution Order

The order in which you define middleware matters. Middleware functions are executed in the order they are defined, either as pre or post hooks.

```javascript
userSchema.pre('save', function (next) {
  console.log('First middleware');
  next();
});

userSchema.pre('save', function (next) {
  console.log('Second middleware');
  next();
});

// When saving a document, the output will be:
// "First middleware"
// "Second middleware"
```

## Conclusion

Mongoose middleware provides a powerful mechanism to inject custom logic into the various stages of the document lifecycle. Whether you need to perform tasks before saving, modify queries, or handle aggregation results, middleware allows for a flexible and modular approach to handling events in your MongoDB-backed applications.