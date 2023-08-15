# Mongo Shell 'Mongosh'

## Commands

- ```cls```: clears the terminal.

- ```db```: refers to the current database.

## Methods

### Add Methods

- ```db.collection.insertOne()```: Adds one record to the database collection.

  example: ```db.bookstore.insertOne({title: "Lorem", author: "John Doe"})```

- ```db.collection.insertMany()```: Adds multiple records to the database collection.

  example: ```db.bookstore.insertMany([{title: "Lorem", author: "John Doe"}, {title: "Ipsum", author: "Jane Doe"}])```

### Find Methods

- ```db.collection.find()```: returns the first 20 records weither there is a condition or not, it recieves 2 arguments. The first argument is the filtering which we pass the field and its value and the result will be the first 20 records that has that value in thats specific field, filter object can have multiple fields. The second arguement is the fields returned from the document, note that if the field value is an array or object it can be handled as well.

  example: ```db.bookstore.find({author: "John Doe", title: "Lorem"}, {title: 1})```

- ```db.collection.findOne()```: returns the first record that matches the filter argument.

### Delete Methods

- ```db.collection.deleteOne()```: deletes one document from a collection.

  example: ```db.colllection.deleteOne(_id: ObjectId(123456789)```

- ```db.collection.deleteMany()```: deletes one document from a collection.

  example: ```db.collection.deleteMany({author: "John Doe"})```

### Update Methods

- ```db.collection.updateOne()```: updates one document in a collection, it recieves two arguments. The first argument is an object to specify which document to update, we should pass a unique value for the field. The second argument is the updated values, where we specify each key with its new value.

  example: ```db.collection.updateOne({_id: ObjectId(123456789)}, { $set: {author: "Joe Shmoe", title: "Dolor"})```

- ```db.collection.updateMany()```: updates all the documents in a collection that has the specifications in the argument.

  example: ```db.collection.updateMany({author: "John Doe" }, { $set: {author: "Joe Shmoe"})```

### Sorting & Limiting Methods

- ```db.collection.find().count()```: it brings the ammount of records returned, it is similar to length.

- ```db.collection.find().limit(n)```: it returns n number of records.

- ```db.collection.find().sort()```: it returns the records sorted by the argument we pass in, where 1 means ASC and -1 means DSC.

  example: ```db.collection.find().sort({ title: 1})```

## Operators & Complex Queries

  example: ```db.collection.find({rating: {$operator: value} })```

- $gt: stands for greater than.

- $gte: stands for greater than or equal

- $lt: stands for less than.

- $lte: stands for less than or equal.

- $or: brings records that matches one value or another.

  example: ```db.collection.find({$or: [{rating: 7}, {author: "John Doe"}]})```

- $in: brings records that matches any value of the provided array.

  example: ```db.collection.find({rating: {$in: [7,8,9]} })```

- $nin: brings records that matches any value of the provided array.

  example: ```db.collection.find({rating: {$nin: [7,8,9]} })```

- $all: brings records that matches all of the provided array of a field that has elements inside an array.

- $ne: to bring records that matches all but the passed id
  
  example: ```db.collection.find({type: {$all: ['fantasy','sci-fi','drama']} })```

- $inc: it is used to increment field's values by specific ammount

  example: ```db.collection.updateOne({_id: ObjectId(123456789)}, { $inc: {rating: 2})``` here we incremented the rating by 2 (old value = 7 ~> updated value = 9)

- $push: it is used to insert values to a specific field, incase of array.

  example: ```db.collection.updateOne({_id: ObjectId(123456789)}, { $push: {reviews: {name: "Red Cat", body: "Good Book"}})```

- $pull: it is used to remove values from a specific field, incase of array.

  example: ```db.collection.updateOne({_id: ObjectId(123456789)}, { $pull: {reviews.name: "Red Cat" })```

- $each: it is used to indicate several values.

  example: ```db.collection.updateOne({_id: ObjectId(123456789)}, { $push: {type: {$each: ["action", "comedy"] }})```

### Create index for faster fetching

db.collection.createIndex({rating: 1 for ASC -1 for DESC})

### Query excution methods

- explain: => db.collection.find({rating: 8}).explain('excutionStatus')
