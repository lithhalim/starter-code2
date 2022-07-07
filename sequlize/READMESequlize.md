## 🔗 Sequlize Cheat Sheet

## 🔗 Create Table @ Create Model
```javascript
//First Thing Define The DataType
const { STRING,INTEGER,Text } = require('sequelize');

// Database.define(TableName, properties, options)
const User = Database.define('TableName', {
  // Model attributes are defined here
  id:{
    type: INTEGER,//
    primaryKey: true,
  },
  firstName: {
    type: STRING,
  }
}, {
    // don't forget to enable timestamps!
  timestamps: true,

  // I CreatedAt To Get The pecific Time I Created
  createdAt: true,

  // I want updatedAt to actually be called updateTimestamp
  updatedAt: true

});


//The All Atributes You Will Used
attributes:{
        type: DataTypes.STRING,//To pecific Type
        allowNull: false,//To Prevent False Value
        autoIncrement: true,//Auto Ictement
        primaryKey: true//The Primery Key
        defaultValue: "John Doe"//If Clinent Dosend Send Value
        unique: true//Is Nut Primery Key But You Cant Repeat
}


```


## 🔗 Dropping Tables @ Drop Model
- To drop the table related to a model:
```javascript
await User.drop();
console.log("User table dropped!");
```
- To drop all tables:
```javascript
await sequelize.drop();
console.log("All tables dropped!");
```


## 🔗 Insert Rows @  Create Table Value
```javascript
const Data = await Model_Name.create({ name: "Jane" });
// console.log(jane); // Don't do this
```

## 🔗 Deleting Rows @ Deleting an instance
```javascript
const Data= await Model_Name.destroy({
    where:{id:Name}//Remove Specific Rows -----Remove Specific Object 
});

```
## 🔗 Select All Rows @ Select All Object
```javascript
// Find all users
const users = await User.findAll();
//Select Specific Column 
Model.findAll({
  attributes: ['foo', 'bar']
});
//Exclude Specific Column
Model.findAll({
  attributes: { exclude: ['baz'] }
});


```

## 🔗 Select All Rows @ Using Where 
```javascript
Post.findAll({
  where: {
    authorId: {
      [Op.eq]: 2
    },
    id: [1,2,3] // Same as using `id: { [Op.in]: [1,2,3] }`
  }
});
// SELECT * FROM post WHERE authorId = 2;
```

## 🔗 findOrCreate 
```javascript
const [user, created] = await User.findOrCreate({
  where: { username: 'sdepold' },
  defaults: {
    job: 'Technical Lead JavaScript'
  }
});

```
## 🔗 Update Sequlize @ Update Rows
```javascript
const updatedRows = await Model_Name.update(Object//The Data In Object
  {
    where: { lastName: null },
  }
);
```

## 🔗 Order By Sorted Data
```javascript
    return Company.findAll({
        // Add order conditions here....
        order: [
            ['id', 'DESC'],// descending order تنازلي
            ['name', 'ASC'],//Ascending order  تصاعدي
        ],
    });

```

## 🔗 Sequelize associations Create Relation
```javascript

//Use To Connect To Model Together

const Model1=require("../post-model/Model1-model");
const Model2=require("../post-model/Model1-model");

  //Relation for postes
  Model1.hasMany(Model2,{
    foreignKey:"posteId",//Secand Model
    sourceKey:"id"//Main Model
  })
  Model2.belongsTo(Model1,{
    foreignKey:"posteId",
    targetKey:"id"
  })


//The Connection Is The Primery Key For First Table===Forgen Key The Secand Table

```

## 🔗 Sequelize associations Get Data From Relation

```javascript
const Main_model=required("/data/main-model/")
module.exports=async(req,res)=>{
    const data=await Main_model.findAll(
        {
            include: [{
                model:postes,
                include:[{
                    model:comment,
                    required: true,
                    {where:{id:id}}
                },
                {
                    model:images,
                }]
               }]
        }
    )}


//Include Mean Geve me The All Model Include With All Propirtes 

```

## 🔗 Create Many Associations 
```javascript
return Product.create({
  title: 'Chair',
  user: {
    firstName: 'Mick',
    lastName: 'Broadstone',
    addresses: [{
      type: 'home',
      line1: '100 Main St.',
    }]
  }
}, {
  include: [{
    association: Product.User,
    include: [ User.Addresses ]
  }]
});


```

## 🔗 Getters, Setters 
```javascript
// Function Use To Encapsulation The Data To Specified The Data Get And Return
const Post = Database.define('TableName', {
  content: {
    type: DataTypes.TEXT,
    //The Seter and get put in proprites to modify data befor input and send
    get() {
      const storedValue = this.getDataValue('content');//The Data In Content Will Insert Here
      return `${storedValue}++`//you modify data befor send it 
    },
    set(value) {//The Value Is The Content
      let data=`${value}$$$$`//the data will put in database
      this.setDataValue('content', data);//use setDataValue to set data
    }
  }
});


```


## 🔗 Virtual fields
```javascript
//create property can use in server but without save in the database
const User = sequelize.define('user', {
  firstName: DataTypes.TEXT,
  lastName: DataTypes.TEXT,
  fullName: {
    type: DataTypes.VIRTUAL,//The Value Of Full Name Will Not Save In Database
    get() {
      return `${this.firstName} ${this.lastName}`;
    },
    set(value) {
      throw new Error('Do not try to set the `fullName` value!');
    }
  }
});

```


## 🔗 Model synchronization
- User.sync() - This creates the table if it doesn't exist (and does nothing if it already exists)
- User.sync({ force: true }) - This creates the table, dropping it first if it already existed
- User.sync({ alter: true }) - This checks what is the current state of the table in the database (which columns it has, what are their data types, etc), and then performs the necessary changes in the table to make it match the model.


### ORM standes for Object Relation Mapping --:>technique query and mapping database using oop
![ORM](ORM.jpg)

## 🔗 Create Connection With Database

## 🔗 installation
```javascript
npm install --save sequelize

# One of the following:
$ npm install --save pg pg-hstore # Postgres
$ npm install --save mysql2
$ npm install --save mariadb
$ npm install --save sqlite3
$ npm install --save tedious # Microsoft SQL Server

```



## 🔗 Connection With Database
```javascript
//use for testing to choose run on database or sqlite
const POSTGRES_URI = process.env.NODE_ENV === 'test' ? 'sqlite:memory:' : process.env.DATABASE_URL;
//USE TO RUN THE DATABASE ON HEROKKU TO MAKE CONFIGRATION 
let sequelizeOptions =
    process.env.NODE_ENV === "production"
        ? {
            dialect: 'postgres',//The Sequlize Use Absrtaction You Can Choose (Mysql,sql server,postgress)
            protocol: 'postgres',
            dialectOptions: {
                ssl :{require: true,rejectUnauthorized: false},
                native: true
            }
        } : {};

module.exports= new Sequelize(POSTGRES_URI,sequelizeOptions) //'postgres://user:pass@example.com:5432/dbname' Example for postgres

```


## 🔗 check connection Database 
```javascript
try {
  await sequelize.authenticate();
  console.log('Connection has been established successfully.');
} catch (error) {
  console.error('Unable to connect to the database:', error);
}

```



## 🔗 Why We Will Usa sequlize 
- Write less code 
- Avoid Sql quires
- Abstract the db system  <---->  you can use muktible type database 






