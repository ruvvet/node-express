# SEQUELIZE

## Set up
1. `npm install pg sequelize`
2. `sequelize init` to set up all the sequelize files
3. set up the `config/config.json` file as needed
4. `sequelize db: create [dbname]` create the db
5. `sequelize model:create --name user --attributes firstName:string,lastName:string`

set up the table + the fields. table name should be singular as it will auto become plural. Note that the model file name will still be singular and that should be used to retrieve in js.

6. `sequelize db:migrate` migrate to connect and update the models to the db

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



### Other Notes
 - a model is a schema with a table we're creating w/ field names