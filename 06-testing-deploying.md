# Testing and Deploying

<!--toc:start-->

- [Testing and Deploying](#testing-and-deploying)
  - [Testing endpoints](#testing-endpoints)
  - [Deploying](#deploying)

<!--toc:end-->

## Testing endpoints

You can implement `POSTMAN` or `CURL` for these operations.
Make simple `HTTP` request to the server's url and check the response.

- GET `/books` Fetch all books

```sh
curl -X GET http://localhost:3000/books
```

- GET `/books/:id` Fetch a single book

```sh
curl -X GET http://localhost:3000/books/{id}
```

- POST `/books` add a new book

```sh
curl -X POST -H "Content-Type: application/json" -d '{"title":"Book Title","author":"Author Name","isbn":"1234567890","publishedDate":"2024-01-01","price":19.99}' http://localhost:3000/books
```

- PUT `/books/:id` Update a book

```sh
curl -X PUT -H "Content-Type: application/json" -d '{"title":"Updated Title"}' http://localhost:3000/books/{id}
```

- DELETE `/books/:id` Delete a book

```sh
curl -X DELETE http://localhost:3000/books/{id}
```

## Deploying

## Conclusion

By following this guide,
you have created a small-scale Node.js API for "managing" a bookstore (hopefully).

You have learned to set up an Express server, define a Mongoose model,
implement `CRUD` operations, connect to `MongoDB`, handle errors,
and deploy your application.

This foundational knowledge can be expanded with additional features and optimizations as needed.
