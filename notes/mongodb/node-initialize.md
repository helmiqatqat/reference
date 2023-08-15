# Mongo ODM Tool for NodeJS 'Mongoose'

## To install mongodb package

```cmd
npm i mongodb --save
```

## To import mongodb package and initiate it

```JavaScript
const { MongoClient } = require('mongodb')
    const { ObjectId } = require('mongodb')

    let dbConnection;

    const connectToDB = (cb) = > {
      MongoClient.connect('mongodb://localhost:27017/db_name')
      .then((client) => {
          dbConnection = client.db()
          return cb()
        })
        .catch(err => {
          console.log(err);
          return cb(err)
        })
    }

    const getDB = () => dbConnection

    let db;

    connectToDB((err) => {
      if(!err) {
        app.listen(port, () => {
          console.log(`app is listening after mongo database connection`)
        })
        db = getDB()
      }
    })

```
