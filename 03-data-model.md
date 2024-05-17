# Defining the data model

<!--toc:start-->

- [Defining the data model](#defining-the-data-model)
  - [Relational Database](#relational-database)
    - [Relational Model and definition](#relational-model-and-definition)
    - [Relational db config](#relational-db-config)
  - [Non relational Database](#non-relational-database)
    - [Non relational Model and definition](#non-relational-model-and-definition)
  - [Considerations](#considerations)

<!--toc:end-->

We need to define the structure of the data our API will manage.
In this case, we will create a model for the books of our bookstore.

The model will offer some basic abstraction of the main characteristics of a `book`.
Feel free to modify as required.

## Relational Database

### Relational Model and definition

Let's create the model inside `model/book.js`:

```javascript
const { DataTypes } = require("sequelize");
const sequelize = require("../config/database");

const Book = sequelize.define("Book", {
  title: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  author: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  isbn: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  publishedDate: {
    type: DataTypes.DATE,
    allowNull: false,
  },
  price: {
    type: DataTypes.FLOAT,
    allowNull: false,
  },
});

module.exports = Book;
```

### Relational db config

Create a file `config/database.js`

```javascript
const { Sequelize } = require("sequelize");

const sequelize = new Sequelize("database", "username", "password", {
  host: "localhost",
  dialect: "postgress", // Change to 'mysql' or other supported DBs
});
```

## Non relational Database

### Non relational Model and definition

You can add this file inside a `model/` directory.
So: `model/book.js` just like before.

```javascript
const mongoose = require("mongoose");

const bookSchema = new mongoose.Schema({
  title: { type: String, required: true },
  author: { type: String, required: true },
  isbn: { type: String, required: true },
  publishedDate: { type: Date, required: true },
  price: { type: Number, required: true },
});

module.exports = mongoose.model("Book", bookSchema);
```

## Considerations

As you can see, both schemas work on basic attributes and data types.
Feel free to modify, delete or add some extra attributes for your example.

In the case of _non-relational db_,
the code `required` references that attribute as needed for each new record.
The same applies with `allowNull` for the _relational db_.
