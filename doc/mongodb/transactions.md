# Transactions in MongoDB

Transactions in MongoDB provide a way to group multiple operations into a single, atomic unit. This ensures that the database remains in a consistent state, even in the presence of errors or failures during the transaction.

## Why Use Transactions?

### 1. Atomicity

Transactions in MongoDB are atomic, meaning that either all the operations within the transaction are applied, or none of them are. This guarantees that the database state remains consistent, and operations do not leave the database in an intermediate, invalid state.

### 2. Consistency

Transactions maintain the consistency of the database by enforcing a set of rules or constraints. If any operation within the transaction violates these rules, the entire transaction is rolled back.

### 3. Isolation

Transactions provide isolation between multiple concurrent transactions. Each transaction sees a snapshot of the database at the start of the transaction, and changes made by other transactions are not visible until they are committed.

### 4. Durability

Once a transaction is committed, the changes become permanent and are durable, even in the event of a system failure or crash.

## How to Use Transactions

### Starting a Transaction

To start a transaction in MongoDB, you use the `startSession` method to create a new session and then call the `startTransaction` method on that session:

```javascript
const session = db.getMongo().startSession();
session.startTransaction();
```

### Performing Operations in a Transaction

All operations within a transaction must be associated with the session:

```javascript
const collection = db.collection('myCollection');
const session = db.getMongo().startSession();

session.startTransaction();

try {
  // Operations within the transaction
  collection.insertOne({ name: 'John Doe' }, { session });
  collection.updateOne({ name: 'Alice' }, { $set: { age: 30 } }, { session });

  // If everything is successful, commit the transaction
  session.commitTransaction();
} catch (error) {
  // If an error occurs, abort the transaction
  print(`Transaction aborted: ${error}`);
  session.abortTransaction();
}
```

### Read Concern and Write Concern

Transactions allow you to specify read and write concerns. The read concern determines the consistency level, and the write concern controls the acknowledgment level for write operations.

```javascript
session.startTransaction({
  readConcern: { level: 'snapshot' },
  writeConcern: { w: 'majority' }
});
```

### Example: Transfer Funds

Here's a simple example of a transaction to transfer funds between two accounts:

```javascript
const session = db.getMongo().startSession();

session.startTransaction();

try {
  const accounts = db.collection('accounts');

  const sourceAccount = accounts.findOne({ accountNumber: '123' }, { session });
  const destinationAccount = accounts.findOne({ accountNumber: '456' }, { session });

  // Perform the fund transfer
  accounts.updateOne({ _id: sourceAccount._id }, { $inc: { balance: -100 } }, { session });
  accounts.updateOne({ _id: destinationAccount._id }, { $inc: { balance: 100 } }, { session });

  // Commit the transaction if everything is successful
  session.commitTransaction();
} catch (error) {
  // Abort the transaction if an error occurs
  print(`Transaction aborted: ${error}`);
  session.abortTransaction();
}
```

This example demonstrates a fund transfer transaction involving two accounts, ensuring the atomicity of the operations.

## Conclusion

Transactions in MongoDB provide a powerful mechanism for maintaining data integrity in complex scenarios. Understanding how to start, perform, and manage transactions will help you design robust and reliable MongoDB applications.