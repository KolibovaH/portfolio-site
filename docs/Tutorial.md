---
id: tutorial
title: Tutorial
sidebar_position: 6
---

# Build a Simple Feedback Form with Dojo and Dijit
This tutorial will guide you through creating an interactive feedback form using the Dojo Toolkit and Dijit UI components. You'll learn how to create form fields, add a submit button, and display submitted data dynamically — perfect for showing off your UI documentation and scripting skills.

## What You’ll Learn
- How to include Dojo and Dijit in your web page
- How to create input fields using Dijit widgets
- How to use JavaScript to respond to form input
- How to update the page dynamically with the submitted data
- And as a bonus, how to add a basic form validation to avoid submitting incomplete or incorrect data.

## What Will Be Your Result
A user-friendly form with:
- Name field (`dijit/form/TextBox`)
- Email field (`dijit/form/ValidationTextBox`)
- Message area (`dijit/form/Textarea`)
- Submit button (`dijit/form/Button`)

A message area that displays the submitted input.

## 1. Project Setup
Before we write any code, let’s organize the project files.
Create a folder with the following structure:
```
/dojo-form/
├── dojo/        ← Dojo Toolkit (if not using CDN)
├── index.html
└── app.js
```
_Tip_: If you're new to Dojo, using the [Dojo CDN](https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/) is easier and requires no download. However, you can download Dojo locally.

## 2. HTML Layout (`index.html`)
This file contains the basic structure of the page, loads the Dojo and Dijit libraries, and sets up the form.

Follow comments in the code (`<!-->`) to get explanation step-by-step.
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Dojo Feedback Form</title>

  <!-- Apply the Dijit 'claro' theme for nice default styling -->
  <link rel="stylesheet" href="https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/dijit/themes/claro/claro.css">

  <!-- Configure Dojo to load modules asynchronously and parse widgets -->
  <script>
    var dojoConfig = {
      async: true,
      parseOnLoad: true
    };
  </script>

  <!-- Load the Dojo Toolkit from the CDN -->
  <script src="https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/dojo/dojo.js"></script>

  <!-- Load our custom JavaScript -->
  <script src="app.js"></script>
</head>

<!-- 'claro' class enables Dijit styling -->
<body class="claro">
  <h2>Feedback Form</h2>

  <!-- The feedback form -->
  <form id="feedbackForm">
    <label for="name">Name:</label>
    <input data-dojo-type="dijit/form/TextBox" id="name" name="name" />

    <label for="email">Email:</label>
    <input data-dojo-type="dijit/form/ValidationTextBox" id="email" name="email" required="true" />

    <label for="message">Message:</label>
    <textarea data-dojo-type="dijit/form/Textarea" id="message" name="message"></textarea>

    <!-- Button that will trigger the event -->
    <button data-dojo-type="dijit/form/Button" id="submitBtn" type="button">Submit</button>
  </form>

  <!-- Area to display submitted feedback -->
  <div id="result"></div>
</body>
</html>

```

### Key concepts:
- `data-dojo-type` tells Dojo to turn regular HTML elements into interactive widgets.
- `ValidationTextBox` adds basic built-in form checks.
- `claro.css` provides modern visual styling.


## 3. JavaScript Logic (`app.js`)
This file contains the code that responds when the user clicks the **Submit** button.

Follow comments in the code (`//`) to get explanation step-by-step.
```
require([
  "dojo/dom",           // Helps get elements by ID
  "dojo/on",            // Lets us attach event listeners
  "dijit/registry",     // Accesses widgets like the TextBox or Button
  "dojo/domReady!"      // Waits until the page is fully loaded
], function(dom, on, registry) {

  // Grab the 'Submit' button widget by its ID
  var button = registry.byId("submitBtn");

  // When the button is clicked, run this function
  on(button, "click", function() {
    // Get values from each form field
    var name = registry.byId("name").get("value");
    var email = registry.byId("email").get("value");
    var message = registry.byId("message").get("value");

    // Insert the values into the result area
    var resultNode = dom.byId("result");
    resultNode.innerHTML =
      "<h3>Submitted Feedback</h3>" +
      "<p><strong>Name:</strong> " + name + "</p>" +
      "<p><strong>Email:</strong> " + email + "</p>" +
      "<p><strong>Message:</strong> " + message + "</p>";
  });

});

```
###  What’s happening here?
- `require()` loads the modules we need.
- `on(button, "click", fn)` listens for a click event.
- `innerHTML` updates the page with the submitted text.

## 4. Test It
1. Open `index.html` in your browser.
2. Fill out the form and click **Submit**.
3. You should see the submitted data displayed below the form.

Congratulations! You've built your first interactive Dojo form.

# Adding Basic Form Validation
To help users avoid submitting incomplete or incorrect data, Dojo's Dijit widgets include built-in validation features. Here's how you can take advantage of them with minimal code changes.

## We'll Cover
- Requiring that **name** and **message** are filled in
- Enforcing that **email** follows a valid format
- Preventing submission if any field is invalid

## Step 1: Add Validation Attributes in HTML
Update your form inputs like this:
```
<input data-dojo-type="dijit/form/TextBox"
       id="name"
       name="name"
       required="true"
       placeHolder="Enter your name" />

<input data-dojo-type="dijit/form/ValidationTextBox"
       id="email"
       name="email"
       required="true"
       placeHolder="email@example.com"
       regExp="^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$"
       invalidMessage="Please enter a valid email address." />

<textarea data-dojo-type="dijit/form/Textarea"
          id="message"
          name="message"
          required="true"
          placeHolder="Write your message..."></textarea>

```
**Explanation:**
- `required="true"` ensures the field can’t be left empty.
- `regExp` on the email field uses a simple pattern to check valid format.
- `invalidMessage` gives users a friendly error message if the check fails.
- `placeHolder` adds helpful placeholder text.

## Step 2: Check for Validity in JavaScript
Before displaying the result, check whether each widget is valid:
```
on(button, "click", function() {
  var nameWidget = registry.byId("name");
  var emailWidget = registry.byId("email");
  var messageWidget = registry.byId("message");

  // Check validity of all widgets
  if (!nameWidget.isValid() || !emailWidget.isValid() || !messageWidget.isValid()) {
    alert("Please fill out all fields correctly.");
    return;
  }

  var name = nameWidget.get("value");
  var email = emailWidget.get("value");
  var message = messageWidget.get("value");

  var resultNode = dom.byId("result");
  resultNode.innerHTML =
    "<h3>Submitted Feedback</h3>" +
    "<p><strong>Name:</strong> " + name + "</p>" +
    "<p><strong>Email:</strong> " + email + "</p>" +
    "<p><strong>Message:</strong> " + message + "</p>";
});
```
Now if the user tries to submit the form with empty fields or an invalid email, they'll see built-in red error outlines, get helpful messages on hover, and be prevented from submitting until everything is valid.

### Need Help?

Check the [Troubleshooting Guide](./Troubleshooting.md) for common errors and how to fix them.