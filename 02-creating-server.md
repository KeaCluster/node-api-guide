# Creating the Express Server

<!--toc:start-->

- [Creating the Express Server](#creating-the-express-server)
  - [Server](#server)

<!--toc:end-->

So let's work on the server and some basic config like ports and stuff.

## Server

Create a new file `server.js` if you don't have it already.
This will be the entry point of our application.
It will configure and start the Express server.

```javascript
const express = require("express");
const cors = require("cors");

// Initialize Express
const app = express();
app.use(cors()); // yknow - for cors
app.use(express.json()); // Middleware to prase JSON

// Port stuff
const PORT = process.env.PORT || 3000;

// Start
app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```
