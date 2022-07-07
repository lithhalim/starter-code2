# 4-database-section
## sequlize database postgress

## installation 
```javascript
npm i sequelize
```
## require section 
```javascript
require('dotenv').config()
const { Sequelize } = require('sequelize');
```
## implimentation
```javascript
//use for testing to choose run on database or sqlite
const POSTGRES_URI = process.env.NODE_ENV === 'test' ? 'sqlite:memory:' : process.env.DATABASE_URL;
//USE TO RUN THE DATABASE ON HEROKKU TO MAKE CONFIGRATION 
let sequelizeOptions =
    process.env.NODE_ENV === "production"
        ? {
            dialect: 'postgres',
            protocol: 'postgres',
            dialectOptions: {
                ssl :{require: true,rejectUnauthorized: false},
                native: true
            }
        } : {};

module.exports= new Sequelize(POSTGRES_URI,sequelizeOptions) //'postgres://user:pass@example.com:5432/dbname' Example for postgres
```


## mongodb
## installation 
```javascript
npm i mongoose
```

## implimentation 
``` javascript
const mongoose = require('mongoose');
//The Link You Get From Mongoss
mongoose.connect("mongodb+srv://lith:12345@cluster0.zolvz.mongodb.net/?retryWrites=true&w=majority")
  .then( result => {
    server.listen(8000, () => {
        console.log('listening on *:8000');
      });
  })
  .catch( err => {
    console.log(err);
  }); 


```
