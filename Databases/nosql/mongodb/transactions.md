# Transactions

Just like in SQL, MongoDB also offers transactions! Have a look at the [sql section](../../sql/transactions.md) for the theory behind why transactions are important as that is the same.

In this section we will go into how to use transactions in MongoDB. The MongoDB team does a good of explaining how to do it in the following video:

<a href="https://www.youtube.com/watch?v=bdS03tgD2QQ">
<img src="https://via.placeholder.com/728x90.png?text=Video+Preview+Coming+Soon" alt="" />
</a>


Let's have a look at some example code. In this function we want to transfer credits from one account to another:

```js
async function transferCredits(fromAccountId, toAccountId, amount) {
  const accountsCollection = client.db("billing").collection("accounts");
  const session = client.startSession();

  try {
    await session.withTransaction(async () => {
      // Remove from fromUser
      await accountsCollection.updateOne(
        { _id: fromAccountId },
        { $inc: { credits: amount * -1 } },
        { session }
      );

      // Add to toUser
      await accountsCollection.updateOne(
        { _id: toAccountId },
        { $inc: { credits: amount } },
        { session }
      );
    });
  } catch (err) {
    await session.abortTransaction();
  } finally {
    await session.endSession();
  }
}
```

There is a lot happening there so the important things in a row:

- You need to always have a session, the `client` can provide you one
- You always need to end the session, the `finally` block helps a lot to make sure that happens
- If something goes wrong you need to abort the transaction to tell MongoDB to not apply anything! The `catch` block makes this nice and simple!
- Whenever you are doing a mutation you need to provide the `session` to the function. That is how MongoDB knows that this is part of a transaction so that it doesn't just apply it straight away!