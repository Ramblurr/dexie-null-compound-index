# Bug description 

If you specify a compound index, and then subsequently attempt to store a record in IDB and the value for that index is null, Safari >= 10.1 blows up with the error message:

```UnknownError – "An unknown error occurred within Indexed Database.```

After this point the database is unusable. It still reports it self as open, but any subsequent calls (e.g., adding an item, opening a transaction) result in further errors.

This affects the iOS 10.3 beta as well.

On Chrome and Firefox, and Safari < 10.1 there is no error, and it works as expected.


##  Code Sample

```js
      db.version(1).stores({
        friends: "++id,name,age,shoeSize,[name+shoeSize]"
      });

      // ...
      // elsewhere in a transaction, this will except
      db.friends.add({name: "Mark", age: 29, shoeSize: null});
```

## Test case

* source: https://github.com/Ramblurr/dexie-null-compound-index/blob/master/test-case.html
* run directly: https://rawgit.com/Ramblurr/dexie-null-compound-index/master/test-case.html
