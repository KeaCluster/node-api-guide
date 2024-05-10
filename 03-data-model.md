# Defining the data model

We need to define the structure of the data our API will manage.
In this case, we will create a model for the books of our bookstore. 

The model will offer some basic abstraction of the main characteristics of a `book`.
Feel free to modify as required.

## Model creation

Let's create the model:

## Schema definition

You can add this file inside a `model/` directory.
So: `model/book.js`.

```javascript
const mongoose = require('mongoose');

const bookSchema = new mongoose.Schema({
    title: { type: String, required: true },
    author: { type: String, required: true },
    isbn: { type: String, required: true },
    publishedDate: { type: Date, required: true },
    price: { type: Number, required: true },
});

module.exports = mongoose.model('Book', bookSchema);
```

As you can see, the schema works on basic attributes and data types.
Feel free to modify, delete or add some extra attributes for your example.
The code `required` references that attribute as needed for each new record.
