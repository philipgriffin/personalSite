---

---
# Creating your own API with web scraping - Node.js & Puppeteer  in 5 minutes!

Presuming you have Node.js installed lets jump right in! _(If you don't head over to_ [_https://nodejs.org/en/_](https://nodejs.org/en/ "https://nodejs.org/en/")_)_

Fire up a terminal and type the code below to get a default package.json - no questions asked!

    npm init -y

With that same terminal window we can install the dependencies that we're going to use.

    npm i -S express puppeteer
    npm i -D nodemon

The ```-S``` tells npm to save express (used for creating our endpoint) and puppeteer (used to scrape our webpage) in our package.json under dependencies.

The ```-D``` tells npm to save nodemon (used for hot-reloading our node.js code) in our package.json under devDependencies.

Now lets create a file called index.js in the root of our project.
Inside we can add a basic server using the code below.

const express = require("express");
const app = express();

app.listen(3000);

app.get("/hello-world", function(req, res) {
  res.status(200).json({ text: "hello world" });
});


  "scripts": {
    "start": "nodemon index.js"
  },