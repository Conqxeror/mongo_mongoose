# Validation in Mongoose

Mongoose provides a robust set of validation features to ensure that the data stored in your MongoDB database adheres to specified rules and constraints. This guide will walk you through various aspects of validation in Mongoose.

## Schema-Level Validation

### Built-In Validators

Mongoose supports a variety of built-in validators that you can use to enforce constraints on your schema fields.

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  username: {
    type: String,
    required: true,
    unique: true,
    minlength: 3,
    maxlength: 20
  },
  email: {
    type: String,
    required: true,
    unique: true,
    validate: {
      validator: (value) => {
        return /\S+@\S+\.\S+/.test(value);
      },
      message: 'Invalid email format'
    }
  },
  age: {
    type: Number,
    min: 18,
    max: 100
  }
});

const User = mongoose.model('User', userSchema);
```

In this example:

- `username` must be a unique string with a length between 3 and 20 characters.
- `email` must be a unique string and follow a custom email format validation.
- `age` must be a number between 18 and 100.

### Custom Validators

You can also define custom validators to perform more complex validation logic.

```javascript
userSchema.path('email').validate({
  validator: (value) => {
    return /\S+@\S+\.\S+/.test(value);
  },
  message: 'Invalid email format'
});
```

## Document-Level Validation

In addition to schema-level validation, Mongoose allows you to perform validation at the document level before saving.

```javascript
const newUser = new User({
  username: 'john_doe',
  email: 'john@example', // Invalid email format
  age: 25
});

newUser.validate((err) => {
  if (err) {
    console.error('Validation error:', err.message);
  } else {
    console.log('Validation passed');
  }
});
```

## Handling Validation Errors

When saving a document, Mongoose will perform validation, and if any errors occur, they will be available in the `ValidationError` object.

```javascript
newUser.save()
  .then(savedUser => {
    console.log('User saved:', savedUser);
  })
  .catch(err => {
    if (err.name === 'ValidationError') {
      console.error('Validation errors:', err.errors);
    } else {
      console.error('Error saving user:', err);
    }
  });
```

## Conclusion

Validation in Mongoose is a critical aspect of ensuring data integrity in your MongoDB database. By leveraging built-in and custom validators, you can define clear rules for your data, both at the schema and document levels. Understanding how to handle validation errors will help you build robust and error-tolerant MongoDB-backed applications.