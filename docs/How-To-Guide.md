---
id: how-to
title: How-To
sidebar_position: 5
---

# How to Create a Simple Dojo Button with an Event Handler
This guide walks you through creating a clickable button using the **Dijit library**, part of the Dojo Toolkit. When clicked, the button will update text on the page.

## Prerequisites
- Basic Dojo project already set up (see [Getting Started](https://github.com/KolibovaH/Portfolio/wiki/Getting-Started) guide).
- Dojo Toolkit downloaded or linked via CDN.
- `dijit` and `dojo` modules available.

## 1. HTML Setup (`index.html`)
Before you can use Dojo or Dijit components, you need to create a basic HTML page that loads the necessary Dojo libraries and applies a theme. In this step, we’ll link the Dojo script (from a CDN or local files), load a default Dijit theme (like Claro), and set up a placeholder for our widget.

```
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Dojo Button Example</title>
  <link rel="stylesheet" href="https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/dijit/themes/claro/claro.css">
  <script>
    var dojoConfig = {
      async: true,
      parseOnLoad: true
    };
  </script>
  <script src="https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/dojo/dojo.js"></script>
  <script src="app.js"></script>
</head>
<body class="claro">
  <div id="buttonNode"></div>
  <p id="output">Button not clicked yet.</p>
</body>
</html>
```
- The `claro` class enables a basic UI theme.
- `dojoConfig` enables auto-parsing of widgets in the DOM.

## 2. JavaScript Setup (`app.js`)
With the HTML in place, the next step is to write the JavaScript that creates and initializes your Dojo widget. We’ll use Dojo’s `require()` function to load the necessary modules, such as the `Button` widget from Dijit and basic DOM utilities. This script will render the button and define what happens when it's clicked.

```
require([
  "dijit/form/Button",
  "dojo/dom",
  "dojo/domReady!"
], function(Button, dom) {
  
  // Create a new Button
  var myButton = new Button({
    label: "Click Me!",
    onClick: function() {
      dom.byId("output").innerHTML = "Button clicked!";
    }
  }, "buttonNode");  // Attach to existing DOM node

  myButton.startup();  // Initialize the widget
});
```
## 3. Result
When you open the page in your browser, you’ll see:
- A styled button labeled **Click Me!**
- Clicking the button updates the paragraph below to say: **"Button clicked!"**

_Reusability Tip_: 
You can reuse this pattern for other widgets (like sliders, text boxes, or dialogs), making it easy to integrate interactive UI elements into your Dojo applications.