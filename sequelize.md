# SEQUELIZE

## Set up
1. `npm install pg` for postgres
2. `npm i sequelize`
3. `sequelize init` to set up all the sequelize files
4. set up the `config/config.json` file as needed *** IMPORTANT
5. `createdb -U postgres [dbname]` create the db w/ a specific user
6. create the model `sequelize model:create --name user --attributes firstName:string,lastName:string`

set up the table + the fields. table name should be singular as it will auto become plural. Note that the model file name will still be singular and that should be used to retrieve in js.

6. `sequelize db:migrate` migrate to connect and update the models to the db


## Configuring the models further inside the models file
We can further configure the models inside the models file
This is essentially an extended class with constructors/functions
Except we don't need to call `this.` for each

### Configuring 1:M, M:N associations
Inside `static associate(models){...}`
 - 1:M
```javascript
models.fileOrModelName.hasMany(models.fileOrModelName222);
models.fileOrModelName222.belongsTo(models.fileOrModelName);
```
- M:N
- create a table like `sequelize model:create --name petsToys --attributes petId:integer,toyId:integer` that basiaclly takes both and makes a new 3rd table
```javascript
models.fileOrModelName.belongsToMany(models.fileOrModelName222, {through: "comboedmodel"})
models.fileOrModelName222.belongsToMany(models.fileOrModelName, {through: "comboedmodel"})
```

### Configuring model datatypes for each field
Configure more specific restrictions on datatypes
- configure whether to allow/notallow null datatypes:
```javascript
title: {
      type: DataTypes.TEXT,
      allowNull: false,
    }
```
- isdate/isurl...etc
```javascript
    date: {
      type: DataTypes.DATE,
      validate: { isDate: true }
    },
    url: {
      type: DataTypes.TEXT,
      validate: { isUrl: true }
    }
```
- more here [https://sequelize.org/master/manual/validations-and-constraints.html](https://sequelize.org/master/manual/validations-and-constraints.html)

### Functions that can be called on data from the model
- functions can also be added here and called inside the "class"
```javascript
//ex
function getFullName (){
  return this.firstName + " " + this.lastName;
}
```
## Queries

- Remember that any call on a db is a promise, and any executables need to be made inside the .then

Require

```javascript
const dbname = require('./models');
```

Create new entry
```javascript
dbname.tablename.create({ // pass in an object with k:v pairs
    //this is a promise
    // uses the key:value pairs and matches them to fields in the table
    somekey: 'somevalue',
    somekey: 'somevalue',
    somekey: 'somevalue',
    // missing fields will result in a null if its not required
    // additional fields will not be put into the table (eg: a typo in the key name)
}).then(results => {
// the promise returns data values, created..etc...
// calling .get() on the returned value shows just the obj itself
// .get will return the table data due to the models set up
    console.log(results.get());
});
```

search one/all

```javascript
// findOne
// querying THE FIRST match
// it is case sensitive
dbname.tablename
  .findOne({
    // this is an object
    // where is the key/query command
    // pass an object into the WHERE query with query parameters
    where: { firstName: 'Jenny' },
  })
  .then((results) => {
    console.log(results.get()); //just return the object
  });

// findAll
// gets back all matches
  //no query parameters passed for findall
dbname.tablename.findAll().then((results) => {
  results.forEach((x => {
    console.log(x.get());
  });
});

```

Update an entry

```javascript
//update/PUT
dbname.tablename
  .update(
    // update takes 2 parameters, an object that has the new info, and the query for what needs to be changed
    { keyofthingtobeupdated: 'value of thing to be updated' }, //pass the update function an object containg what needs to
    { where: { somesearchkey: 'new value' } }
  )
  .then((numRowChanged) => {
    console.log(numRowChanged);// only returns the # of rows updated
  });
```

deleting an entry

```javascript
//deleting
dbname.tablename
  .destroy({ // passes an object with key as the type of sql command
  // and the value as what is to be deleted
    where: { keyofthingtobedel: 'somevalue' },
  })
  .then((numRowDel) => {
    console.log(numRowDel); // only returns the # of rows updated
  });

```




 - [ ] put notes in here from usreapp












### Other Notes
 - a model is a schema with a table we're creating w/ field names