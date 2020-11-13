# Node Notes

 - node manages modules + libraries that are used in the program
 - entry point is the primary code that is the keystone of the project - it holds everything together

# Creating the project

1. create repo/folder
2. navigate to folder in terminal
3. `npm init` - this creates the package.json file which tells node what packages/libraries need to be installed with `npm install` for future users of the project
4. ... adjust settings - entry point is the primary
5. ...

# Exporting functions/objects from a module...

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

# Importing a module

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

# Running it in the terminal
1. navigate to folder with cd
2. `node filename.js`

# .gitignore
To ignore the module files, create a .gitignore file and add `node_modules` into the file.


# SQL NOTES

## Basics

select all

 ```SQL
SELECT * FROM tablename;
```

Select given specific parameters

```SQL
 SELECT field FROM tablename
    WHERE field = 'somevalue';
    ...
    WHERE field IN ('value1', 'val2'...);
    ...
    WHERE field BETWEEN ...AND/OR...;
    ...
```

order by
```SQL
SELECT field FROM tablename
    WHERE ...
    ORDER BY... field
```

## Operations

greater/less than
```SQL
SELECT field FROM tablename
    WHERE field2 >/</>=/<=/= somevalue;
```

can calculate new fields with matches
```SQL
SELECT field, math() FROM tablename
    WHERE....
```




## Strings

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
SELECT field FROM tablename
    WHERE field LIKE '%str';
    ...
    WHERE field LIKE 'str%';
    ...
    WHERE field LIKE '%str%';
    ...
    WHERE field LIKE 'strA%strB';
    ...
```

Length of a value/string

```SQL
SELECT * FROM tablename
    WHERE LENGTH(field) = ;
```

Concatenate strings

```SQL
SELECT field FROM tablename
    WHERE field2 = concat(field, ' something')
```



