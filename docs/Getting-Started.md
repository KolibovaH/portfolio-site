---
id: getting-started
title: Getting Started
sidebar_position: 4
---

# Getting Started with Dojo Toolkit
The **Dojo Toolkit** is a powerful JavaScript framework for building scalable, modular, and rich web applications. 

This guide will walk you through the basics: installing Dojo, setting up your first project, and running a simple script.

## 1. Get Dojo Toolkit
You have two main options for getting Dojo:

a) **Use a CDN (Recommended for Quick Setup)**

This is the easiest way to get started. Just add the following `<script>` to your HTML file:
```
<script src="https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/dojo/dojo.js"></script>
```
b) **Download Dojo Locally**

If you prefer to host the files yourself:

1. Download from https://dojotoolkit.org/download.

2. Unzip and place the folder (commonly named `/dojo/`) in your project directory.

3. Reference `dojo/dojo.js` in your script tag.

## 2. Structure Your Project

Here's how to organize your files:

```
/your-project/
│
├── dojo/           ← (if downloaded manually)
├── index.html      ← your main web page
└── app.js          ← your custom JavaScript code
```
This setup keeps things modular and clear.

## 3. Create `index.html`
This HTML file loads the Dojo framework and your custom script:
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Dojo App</title>

  <!-- Load Dojo (adjust path if local) -->
  <script src="dojo/dojo.js" data-dojo-config="async: true"></script>

  <!-- Load your application logic -->
  <script src="app.js"></script>
</head>
<body>
  <h1 id="greeting">Hello!</h1>
</body>
</html>
```
- `data-dojo-config="async: true"` tells Dojo to load modules asynchronously (the modern way).
- The `greeting` element will be modified by your script.

## 4. Write Your First Dojo Script
Use AMD (Asynchronous Module Definition) to load modules. Here's how to change the page content using Dojo:
```
require(["dojo/dom", "dojo/domReady!"], function(dom) {
  var greetingNode = dom.byId("greeting");
  greetingNode.innerHTML = "Hello from Dojo!";
});
```
- `dojo/dom`: A module to work with DOM elements (similar to `document.getElementById`).
- `dojo/domReady!`: Ensures the DOM is fully loaded before running your script.

## 5. Run It in the Browser
Simply open `index.html` in a browser (double-click it or use a local server). 

You should see:

> Hello from Dojo!
 ...replacing the original text inside the `<h1>`.

## Next Steps
Now that you've set up a working Dojo project and manipulated the DOM with modular JavaScript and your base is ready, you might want to:

- Add **UI widgets** using `dijit`
- Use **events** with `dojo/on`
- Organize logic into **custom modules**
- Explore **themes** and styling for widgets