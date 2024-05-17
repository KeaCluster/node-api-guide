# Conneting the Database

<!--toc:start-->

- [Conneting the Database](#conneting-the-database)

  - [Relational DB config](#relational-db-config)
  - [Non-relational DB config](#non-relational-db-config)
  - [Success and Errors](#success-and-errors)
  - [Middleware](#middleware)

  <!--toc:end-->

Now that our server _listens_ to requests,
let's actually give it the function to modify data on our database.

## Relational DB config

```javascript
const sequelize = require("./config/database");
const Book = require("./models/book"); // import Book model created in the prev section

// Connection

sequelize
  .sync()
  .then(() => console.log("Databse synced"))
  .catch((err) => console.error("Could not connect to DB", err));
```

## Non-relational DB config

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

## Environment variables

To keep our `database` credentials more secure,
we can implement a `.env` file at the root of our project.
As of `Node v 20+`,
we have available a command to find and configure env variables automatically

Inside the .env file:

```env
# For MongoDB
MONGODB_URI="mongodb://localhost:27017/bookstore"

# For PostgreSQL
DATABASE_URL="postgres://your_username:your_password@localhost:5432/your_database_name"

```

Make sure to use update the data with your proper credentials

Now, when running the server, just add the following flag to the command:

```sh
node --env-file=.env server.js
```

Alternatively, you can add a script inside your `package.json` to do that automatically:

```json
"scripts": {
  "dev": "node --env-file=.env server.js",
  "test": "echo \"Error: no test specified\" && exit 1"
},
```

With this you can run `npm run dev` and it will automatically execute the parameters.

## Success and Errors

Let's add some middleware to log errors and handle unexpected results.

### Middleware

Y'know.
Middleware functions that have access to the request object (`req`),
the response object (`res`),
and the next middleware function in the app's `request-response` cycle.
They can execute any code, modify or manipulate the `request` and `response`,
as well as end the cycle, and call proceeding middleware functions.

```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send("Something broke on our side");
});
```
