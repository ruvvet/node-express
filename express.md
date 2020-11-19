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


### Routes

Should start with a `'/'` because this directing to a url path.
Use this for:
 - any `app.get ('/', ...)`, `app.post`, `app.put`, `app.delete`
 - `res.redirects('/')`
 - form action `'/'`


### Renders

This is rendering a page in the project, and not a url.
res.render will auto search in the 'views' folder and do not need a `'/'`.