# MongoDB Methods in NodeJS

**To select database and collection to apply methods on**: We Simply specify the database name and chain the collection function where we put the collection name as a string argument, then chain any method we want to apply.

```JavaScript
db.collection('collection_name').method_name(data)
```

## Read documents methods

1. .findOne()

2. .find()

## Add documents methods

1. .insertOne()

2. .inerstMany()

## Update documents methods

1. .updateOne()

2. .updateMany()

## Delete documents methods

1. .deleteOne()

2. .deleteMany()

## Filtering and Sorting documents methods

1. .sort({field: 1 for ASC, -1 for DESC})

2. .skip(integer)

3. .limit(integer)
