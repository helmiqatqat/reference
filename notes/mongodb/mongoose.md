# Mongoose

## Install package and require it in the system

### Terminal

To install the package, we write the following command in ubuntu terminal

```cmd
npm i mongoose
```

### NodeJS require

To effientally require mongoose we need to write the following lines of code:

```JS
  const mongoose = require('mongoose')
  mongoose.connect(process.env.DATABASE_URL).then(() => console.log('Connected to Database'))
```


## Create Schema

```JS
  const mongoose = require('mongoose')
  const userSchema = new mongoose.Schema({
    username: {
      type: String
    }
  })
  
  module.exports = mongoose.model('Users', userSchema)
```

## Methods

- findOne()
- findByIdAndUpdate()
- .select(): to select certain columns to be returned in the record.
- 