# Implementing CRUD operations

<!--toc:start-->

- [Implementing CRUD operations](#implementing-crud-operations)
  - [How to CRUD](#how-to-crud)
    - [GET](#get)
    - [POST](#post)
    - [PUT](#put)

<!--toc:end-->

This section will cover the hardwork of our API when listening to certain requests.
These requests could be any type of allowed `HTTP` requests such as
`GET POST PUT DELETE`.
AKA `CRUD`.

Try to modify the code to have better control over the requests being made.
Also feel free to organize code and files in a different manner inside your API.
Follow best practices and implementations.

## How to CRUD

These are our objectives:

- Setup Database connection (either case)
  - Connect to the database through `server.js`
  - Configure connection options to handle potential deprecation
- Handle connection success and Errors
  - Log a message to know if the connection is successful
- Add Error handling middleware
  - Add middleware functions to handle errors
  - Log or send appropiate responses to the client's request

We'll handle simple CRUD endpoints for our api.
You'll see by the end, they're rather similar with slight differences regarding middleware functions.

## Relational Database protocols

```javascript
const express = require("express");
const Book = require("./models/book"); // Import Book model

// Define routes
const router = express.Router();

// Get all books
router.get("/", async (req, res) => {
  try {
    const books = await Book.findAll();
    res.json(books);
  } catch (err) {
    res.status(500).json({ message: err.message });
  }
});

// Get one book
router.get("/:id", getBook, (req, res) => {
  res.json(res.book);
});

// Add a new book
router.post("/", async (req, res) => {
  try {
    const book = await Book.create(req.body);
    res.status(201).json(book);
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
});

// Update a book
router.put("/:id", getBook, async (req, res) => {
  try {
    await res.book.update(req.body);
    res.json(res.book);
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
});

// Delete a book
router.delete("/:id", getBook, async (req, res) => {
  try {
    await res.book.destroy();
    res.json({ message: "Deleted Book" });
  } catch (err) {
    res.status(500).json({ message: err.message });
  }
});

// Middleware function to get book by ID
async function getBook(req, res, next) {
  try {
    const book = await Book.findByPk(req.params.id);
    if (book == null) {
      return res.status(404).json({ message: "Cannot find book" });
    }
    res.book = book;
    next();
  } catch (err) {
    return res.status(500).json({ message: err.message });
  }
}

module.exports = router;
```

## Non-relational Database protocols

### GET

Check this out:

```javascript
const express = require("express");
const Book = require("models/book"); // Adjust this to your structure

const router = express.Router();

// GET ALL
router.get("/", async (req, res) => {
  try {
    const books = await Book.find();
    res.json(books);
  } catch (err) {
    res.status(500).json({ message: err.message });
  }
});
```

This will listen to the endpoint `'/'` and return all books if it receives a GET request.

Now let's work on one book

```javascript
router.get("/:id", getBook, (req, res) => {
  res.jon(res.book);
});
```

This will call an async middleware function `getBook`.
You can declare it at the bottom of the file like so:

```javascript
// Middleware function to get book by parameter ID
async function getBook(req, res, next) {
  let book;
  try {
    book = await Book.findById(req.params.id);
    if (book == null) {
      return res.status(404).json({ message: "Cannot find book" });
    }
  } catch {
    return res.status(500).json({ message: err.messsage });
  }
  res.book = book;
  next();
}
```

### POST

To add a new book we'll check the payload of the request and return a `200`.

```javascript
router.post("/", async (req, res) => {
  const book = new Book({
    title: req.body.title,
    author: req.body.author,
    isbn: req.body.isbn,
    publishedDate: req.body.publishedDate,
    price: req.body.price,
  });

  try {
    const newBook = await book.save();
    res.staus(201).json(newBook); // 201 for creation sucess
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
});
```

### PUT

Let's update a record by its `id`.

```javascript
router.put("/:id", getBook, async (req, res) => {
  // You can simplify these if you want
  if (req.body.title != null) {
    res.book.title = req.body.title;
  }
  if (req.body.author != null) {
    res.book.author = req.body.author;
  }
  if (req.body.isbn != null) {
    res.book.isbn = req.body.isbn;
  }
  if (req.body.publishedDate != null) {
    res.book.publishedDate = req.body.publishedDate;
  }
  if (req.body.price != null) {
    res.book.price = req.body.price;
  }

  try {
    const updatedBook = await res.book.save();
    res.json(updatedBook);
  } catch (err) {
    res.status(400).json({ message: err.message });
  }
});
```

### DELETE

Now lets find a book and delete the data

```javascript
router.delete("/:id", getBook, async (req, res) => {
  try {
    await res.book.remove();
    res.json({ message: "Deleted Book" });
  } catch (err) {
    res.status(500).json({ message: err.message });
  }
});
```

## Implement

To add these routes inside our server just add the following lines in `server.js`
There is **no** difference regarding this implementation for either db.

```javascript
const bookRoutes = require("./routes/bookRoutes"); // Adjust as per your structure
app.use("/books", bookRoutes);
```
