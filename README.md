Notes + stuff

***
***
# Node Notes

 - node manages modules + libraries that are used in the program
 - entry point is the primary code that is the keystone of the project - it holds everything together

### Creating the project

1. create repo/folder
2. navigate to folder in terminal
3. `npm init` - this creates the package.json file which tells node what packages/libraries need to be installed with `npm install` for future users of the project
4. ... adjust settings - entry point is the primary
5. ...

### Exporting functions/objects from a module...

```javascript

// in the module, export functions as an object using
module.exports  = { //the functions go here
};
```
```javascript
//exporting the array from foods.js
// the array is the value
// when only exporting one element, can use this
module.exports = [
    'watermelon',
    'peaches',
    'clementines',
//...
]

//otherwise it is better to declare an object with key:value pairs
//ex
// module.exports = {foods:[arr] }

```

### Importing a module

```javascript
// in another file, import the module and specify which ones are being used
const {//the functions to be imported
} = require("./modulename");

//then call the function
functionName();

// can also call the functions from the module by

const someModule = require("./modulename");

someModule.functionName();

```

```javascript
// call the module and associated functions/elements
const path = require('path');
```

```javascript
// printing each element from the imported array
// imported foods array
const foods = require('./foods.js')

// printing the foods
for (let i=0; i<foods.length; i++){
    console.log(foods[i]);
}
```

### Running it in the terminal
1. navigate to folder with cd
2. `node filename.js`

### .gitignore
To ignore the module files, create a .gitignore file and add `node_modules` into the file.

***
***

# EXPRESS NOTES

1. npm install express
2. in entry point file, create import express
```javascript
const express = require('express');
```
3. create an app/instance
```javascript
const app = express();
```
4. set the view to use the ejs engine - this renders the ejs/html files
```javascript
app.set('view engine', 'ejs');
```
5. create routes

### REQ + RES

 - **REQ** : is an object of 'typically' json data that makes up the request from the endpoint (`req.body`, `req.params`, `req.query`)
 - **RES** : what's sent back (`res.send()` for simple response, `res.sendFile()` for html, `res.render()` renders with selected engine 'like ejs', `res.json()` to send back a json obj)

### Home route

```javascript
app.get('/', function(req, res){
    //...res
};
```

### Creating other Routes

homeroute '/' followed by whatever.

 - **`:endpointname` is a url route parameter**

 - **`search?key=val&key2=val2` is a url query**


starting the server
```javascript
app.listen(5000, () => {
    //localhost:5000
});
```

### Sending Responses and rendering it on the page

Level 0 - basic get - gets route and sends response

```javascript
app.get('/', function(req, res){
    res.send('Hello World');
    // this is printed to the page
})
```

Level 1 - send html page

```javascript
app.get('/', function(req, res){
    res.sendFile(__dirname+'/views/index.html');
    res.status(200);
    //dirname gets the relative path regardless of where its deployed
})
```

Level 2 - send ejs page

```javascript
// res is an object that express provides
// that represents the response that needs to be sent, based on the route that was requested
// this object can contain html, code, js, database...etc

app.get('/blog/:date', function(req, res){
    // the req is an object with multiple predefined keys such as params: and query:
    // and the value is what req from each endpoint

    res.render('blog', {date: req.params.date});
    // here we the date is an object
    // at this endpoint {date: somedate} is the parameter requested by the endpoint
    // we pass that into our render arguments
    // to pass into our ejs page so it can render it

});
```
Rendering it in html. The ejs engine `app.set('view engine', 'ejs');` converts the ejs to html before its rendered on the page.

```HTML
<!-- no = means this executes the js but does not render it -->
<% const x = 10; %>
<!-- grabs info passed from res arguments and renders to page -->
<% = date%>
<!-- makes an ejs page accessible -->
<%- include('nav') %>
```

***
***
# SQL NOTES

### Basics

select all

 ```SQL
SELECT * FROM tablename;
```

Select given specific parameters

```SQL
    field = 'somevalue';
    ...
    field IN ('value1', 'val2'...);
    ...
    field BETWEEN ...AND/OR...;
    ...
```

order by

```SQL
    ORDER BY... field
```

rename as

```SQL
    AS newname
```

### Conditionals

```SQL
AND
OR
XOR --true if one or the other, not both
```

### Operations

greater/less than
```SQL
SELECT field FROM tablename
    WHERE field2 >/</>=/<=/= somevalue;
```

can calculate new fields with matches
```SQL
SELECT field, mathstuffhere() FROM tablename
    WHERE....
```

### Strings

Select w/ wildcards
- % is a wildcard that can be any length
- _ (underscore) is one char slot
- use (str)% to find wildcards that start with the str
- %(str) that end with the str
- %(str)% contains the str
- (str start)%(str end) that returns any matches that start + end
- '%a%a%a%' finding any matches with 3 a's
- '_t%' where t is the second char in the string


```SQL

     LIKE '%str';
    ...
     LIKE 'str%';
    ...
     LIKE '%str%';
    ...
     LIKE 'strA%strB';
    ...
```

Length of a value/string

```SQL
    LENGTH(field) = ;
```

Concatenate strings

```SQL
    field2 = CONCAT(field, ' something');
```

Escaping single quote

```SQL
    People''s --double up the quote
```

### Functions

Get leftmost values

```SQL
    LEFT(field, #);
```

Round to specific # of decimal places

```SQL
    ROUND(#, number of decimal places);
```

Sum, count functions that aggregate results

```SQL
    SUM(field) --sum of returned matches

    COUNT(field) --# of returned matches
```

Max, Distinct which filter after query

```SQL
    DISTINCT(field) -- gives unique matches

    MAX(field) --gives max
```

Case for 'if/elif/else'

```SQL
CASE WHEN ...THEN...ELSE...END
```


Coalesce gets first non-null value

```SQL
    COALESCE (arg1, arg2) -- takes arguments and returns first non-null value
```

Group by, having which also filter after the query is returned

```SQL
    GROUP BY field -- used with sum/count where fields are aggrgated in select output
    HAVING -- filters displayed output (unlike WHERE which filters ths query)
```

Use a boolean to order things

```SQL
    WHERE field IN ('...') -- returns a boolean
    -- then order by the boolean
    ORDER BY field IN ('...')
```

Select in select

```SQL
--identify diff aliases for inner/outer select tables
SELECT continent, name, area
    FROM world x --name of outer
    WHERE area >=
        ALL
            (SELECT area
                FROM world y -- name of inner
                WHERE y.continent=x.continent AND area>0);
```

### Joins

```SQL
(INNER) JOIN -- returns all rows from both where ther are no null values
LEFT (OUTER) JOIN -- retiurns all from left, and matching from right, this means left can have null values
RIGHT (OUTER) JOIN -- returns all from right table, matching from left, so right table can have null
FULL (OUTER) JOIN -- returns all when there is a match in either table
```

