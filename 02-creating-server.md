# Creating the Express Server

So let's work on the server and some basic config like ports and stuff.


## Server

Create a new file `server.js`.
This will be the entry point of our application.
It will configure and start the Express server.

```javascript
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');

// Initialize Express
const app = express();
app.use(cors());
app.use(express.json()); // Middleware to prase JSON

// Port stuff
const PORT = process.env.PORT || 3000;

// Start
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```
