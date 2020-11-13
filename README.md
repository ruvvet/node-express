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




