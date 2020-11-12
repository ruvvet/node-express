# node-express

### creating repo + initializing node in the project
1. create repo/folder
2. navigate to folder in terminal
3. `npm init`
4. ... adjust settings - entry point is the file you use as the entry point
5. ... 

### Notes:

```javascript

// in the module, export functions as an object using
module.exports  = { //the functions go here
};

// in another file, import the module and specify which ones are being used
const {//the functions to be imported
} = require("./modulename");

//then call the function
functionName();

// can also call the functions from the module by

const someModule = require("./modulename");

someModule.functionName();

```

### Running it in the terminal
1. navigate to folder with cd
2. `node filename.js`
