# Introduction and Setup

## Introduction

This guide (I hope) will guide you through a small-scale (useless for production)
 [`Node.js API`](https://nodejs.org/en) for managing a bookstore.
We will implement [`Express.js`](https://expressjs.com/) for the server framework and 
[`Mongoose`](https://mongoosejs.com/) for a [`MongoDB`](https://www.mongodb.com/) interaction.
~~Jesus christ that's a lot of links~~

By the end of this guide you (should) will have a fully functional `API` that you can deploy and test.
At least that's the idea.

## Setup

So, let's setup our environment.

- Create the directory of the project
    - Jk where the files go
    - Name it whatever
- (Optional but recommended) initialize a git repo just in case
- Initialize a `node.js` project.
- Install dependencies
    - We'll be using `express`, `mongoose`, `cors`.
        - Express is our server.
        - Mongoose is our MongoDB interaction thingy
        - CORS for y'know, [CORS](https://aws.amazon.com/what-is/cross-origin-resource-sharing/).

Here's the list of commands just in case.

```sh
mkdir bookstore-api
cd bookstore-api
git init
npm init -y
npm install express mongoose cors
```

If using linux you might need to `sudo` some.
