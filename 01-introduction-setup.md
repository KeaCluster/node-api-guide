# Introduction and Setup

<!--toc:start-->

- [Introduction and Setup](#introduction-and-setup)
  - [Introduction](#introduction)
  - [Setup](#setup)

<!--toc:end-->

## Introduction

This guide (I hope) will guide you through a small-scale (useless for production)

- [`Node.js API`](https://nodejs.org/en) for managing a bookstore.
- We will implement [`Express.js`](https://expressjs.com/) for the server framework and
- [`Mongoose`](https://mongoosejs.com/) for a [`MongoDB`](https://www.mongodb.com/) interaction.
- And [Sequelize](https://sequelize.org/) for a _relational_ database option.
  ~~Jesus christ that's a lot of links~~

By the end of this guide you (should) will have a fully functional `API` that you can deploy and test.
At least that's the idea.

## Setup

So, let's setup our environment.

- Create the directory of the project
  - You know, where the files go
  - Name it whatever (bookstore-api)
- (Optional but recommended) initialize a git repo just in case
- Initialize a `node.js` project.
- Install dependencies
  - We'll be using `express`, `mongoose` || `sequelize`, `cors`.
    - Express is our server.
    - Mongoose is our MongoDB interaction thingy
    - Sequelize for our relational DB thingy.
    - CORS for y'know, [CORS](https://aws.amazon.com/what-is/cross-origin-resource-sharing/).

Here's the list of commands just in case.

```sh
mkdir bookstore-api
cd bookstore-api
git init
npm init -y
npm install express cors
npm install mongoose // for non-relational mongodb
npm install sequelize pg pg-hstore // for relational db
```

If using linux you might need to `sudo` some.

Choose your database and run the proper commands.
Each file contains configuration for both options.
