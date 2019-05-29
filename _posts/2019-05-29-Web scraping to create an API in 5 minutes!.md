---
tags: Node.js Puppeteer

---
Presuming you have Node.js installed lets jump right in and create the endpoint! _(If you don't head over to_ [_https://nodejs.org/en/_](https://nodejs.org/en/ "https://nodejs.org/en/")_)_

Fire up a terminal and type the code below to get a default package.json - no questions asked!

```javascript
npm init -y
```

With that same terminal window we can install the dependencies that we're going to use.

```javascript
npm i -S express puppeteer
npm i -D nodemon
```

The `-S` tells npm to save `express` (used for creating our endpoint) and `puppeteer` (used to scrape our webpage) in our `package.json` under dependencies.

The `-D` tells npm to save `nodemon` (used for hot-reloading our `node.js` code) in our package.json under devDependencies.

Now lets create a file called index.js in the root of our project.
Inside we can add a basic server using the code below.

```javascript
const express = require("express");
const app = express();

app.listen(3000);

app.get("/hello-world", function(req, res) {
 res.status(200).json({ text: "hello world" });
});
```

Lets jump into the package.json and modify the scripts object to look like below

```javascript
"scripts": {
 "start": "nodemon index.js"
},
```

Now run npm start and head over to chrome and navigate to localhost:3000. You should be greeted with a JSON response that looks like the response below.

![](/uploads/json-hello-world.png)

Now lets get scraping...

## Scraping the data

Lets start by renaming our endpoint to what we want to achieve. I'm going to scrape the title from the most recent post on my own website so I'll name my endpoint philipgriffin/title like so.

```javascript
 app.get("/philipgriffin/title", function(req, res) {
```

Lets modify the code within the get callback and replace it with the code below

```javascript
app.get("/philipgriffin/title", function(req, res) {

 void (async() => {

  const browser = await puppeteer.launch({ headless: true });

  try {

  const page = await browser.newPage();
  await page.goto("https://philip-griffin.com");

  const postTitleElement = await page.$(".post-title");
  const postTitle = await page.evaluate(postTitleElement => postTitleElement.textContent.trim(), postTitleElement);

  await browser.close();
  res.status(200).json({ postTitle: postTitle });

  } catch (e) {

  await browser.close();
   res.status(500).json({ error: "error" });
  }
 })();
});
```

Okay! Lets explain this...

```javascript
    void (async() => { //body })();
```

Here we simply create an asynchronous immediately invoked function expression. This is required so that we can use the await keyword to wait for promises to complete. async and await were introduced in ES 2017 and allows us to deal with promises in a cleaner fashion - something we'll see in a few moments.

```javascript
    const browser = await puppeteer.launch({ headless: true });
```

Using await we can tell puppeteer to launch in a headless mode so that we don't physically watch the scraping occurring. Feel free to change this to false if you want to watch!

The launch function returns a promise although rather than allowing asynchronous execution we will wait until the promise has completed by specifying the await keyword as we need to use the browser.

From here on we tell puppeteer to connect to our desired website and begin scraping. Once we get what we need we can return it like before and we now have our own API to scrape a website!

Check it out below along with the source code.

Source code: [https://github.com/philipgriffin/scrapingApi](https://github.com/philipgriffin/scrapingApi "https://github.com/philipgriffin/scrapingApi")

Demo;

![](/uploads/scraping.gif)
