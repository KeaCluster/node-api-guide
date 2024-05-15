# Testing and Deploying

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
