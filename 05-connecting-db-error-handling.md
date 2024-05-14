# Conneting the Database

Now that our server _listens_ to requests,
let's actually give it the function to modify data on our database.

## Setup DB

First let's connect to MongoDB using Mongoose inside `server.js`.
We'll add some connection options to handle potential deprecation warnings

```javascript
mongoose
  .connect("mongodb://localhost:27017/bookstore", {
    useNewUrlParaser: true,
    useUnifiedTopology: true,
  })
  .then(() => console.log("Connected to MongoDB"))
  .catch((err) => console.error("Could not connect to MongoDB", err));
```

## Success and Errors

Let's add some middleware to log errors and handle unexpected results.

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send("Something broke on our side");
});
```

## Middleware
