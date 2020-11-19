# Axios

# Setup

1. `npm install axios`
2. Require `const axios = require('axios').default;`


```javascript
// first use call .get on axios with the api endpoint
axios.get(`api/route/goes/here/?apikey=${process.env.APIKEY}`)
// this returns a response
.then(response =>{
    //data here
    // execute stuff here
})

```

### Other notes

- Don't forget to hide api key with
- `require('dotenv').config();`
- and putting the APIKEY in .env

- Axios is a library that makes an api call and gets a response
- In fetch, we send an api call >>  that returns data >> that then needs to be turned into json
- `fetch ('api endpoint').then(response = > response.json()).then(data => {});`
- Axios condenses the process
- and returns all the header info and data