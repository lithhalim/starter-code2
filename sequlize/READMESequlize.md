# Sequlize Cheat Sheet
# Project Title

### Create Table//Create Model
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


<p style="color:red">Coclusion :The Table You Will Create Is Class With Propertes And You Will Instanse To Set The Vlaue Of Attribute On The Same Class</p>




### Model synchronization
- User.sync() - This creates the table if it doesn't exist (and does nothing if it already exists)
- User.sync({ force: true }) - This creates the table, dropping it first if it already existed
- User.sync({ alter: true }) - This checks what is the current state of the table in the database (which columns it has, what are their data types, etc), and then performs the necessary changes in the table to make it match the model.



### Dropping Tables // Drop Model
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


### Insert Rows //  Create Table Value
```javascript
const Data = await Model_Name.create({ name: "Jane" });
// console.log(jane); // Don't do this
```

### Deleting Rows // Deleting an instance
```javascript
const Data= await Model_Name.destroy({
    where:{id:Name}//Remove Specific Rows -----Remove Specific Object 
});

```
### Select All Rows//Select All Object
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

### Select All Rows // Using Where 
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

### findOrCreate
```javascript
const [user, created] = await User.findOrCreate({
  where: { username: 'sdepold' },
  defaults: {
    job: 'Technical Lead JavaScript'
  }
});

```

### Update Sequlize 
```javascript
const updatedRows = await Model_Name.update(Object//The Data In Object
  {
    where: { lastName: null },
  }
);
```

### Order By Sorted Data
```javascript
    return Company.findAll({
        // Add order conditions here....
        order: [
            ['id', 'DESC'],// descending order تنازلي
            ['name', 'ASC'],//Ascending order  تصاعدي
        ],
    });

```

### Sequelize associations Create Relation
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

### Sequelize associations Get Data From Relation

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

### Create Many Associations 
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
