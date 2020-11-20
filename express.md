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
5. npm install method over-ride (for delete/put)
6. `app.use(methodOverride('_method'));` set this on the app to use the override methods
7. create routes

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


### Passing info with body, params, query

Query
 - This is a route that looks like `.../?key1=value1&key2=value2...`
 - these are used with `forms + GET`, and in the address bar, these query params will show up
 - These are passed through in the `query` and can be accessed from the route request via `req.query.key`


 Params
 - Pass data through the route itself
 - these look like `.../:somevalue`
 - the actual public-facing input will be `.../somevalue`
 - access this through the route via `req.params.somevalue`
 - these are good for accessing explicit elements

 Body
 - this is info passed through a `form + POST/PUT/DEL action`
 - and can be accessed through `req.body`
 - where specific values follow the key:val format
 - When creating the form, the `method = "post/put/delete"` and `action="/route"`
 - for each input the `name="x"` gives the `key=x` and `value=[input]`
 - then access in route via `req.body.x`



### Renders

This is rendering a page in the project, and not a url.
res.render will auto search in the 'views' folder and do not need a `'/'`.
 - only render pages within a .get - because we are 'getting' a route/endpoint that can be rendered
 - post, put, delete should be redirects after they've completed their actions
 -




# Other

 - differences between routes depends on what is returned in the body/headers after theyve executed
 - url routes/endpoints need `'/'`, any actions that are looking for files inside the repo (like res.render) do not prefix with a / unless its a relative path thing.