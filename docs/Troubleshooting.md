---
id: troubleshooting
title: Troubleshooting
sidebar_position: 7
---

# Troubleshooting Guide for Dojo and Dijit
If you’re running into problems while building or testing your Dojo-based feedback form, this page is here to help. Below you’ll find common issues, error messages, and simple solutions for fixing them. Whether you're just getting started or debugging a specific problem, check here first before diving deeper.



## The widgets don’t appear styled or interactive
**Symptoms:**
- The input fields look like plain HTML.
- The button isn’t styled.
- No interactivity.

**Fix:**
- Make sure you have the correct **Claro theme CSS** linked in your `<head>`:
```
<link rel="stylesheet" href="https://ajax.googleapis.com/ajax/libs/dojo/1.16.4/dijit/themes/claro/claro.css">

```
- Confirm your body tag has the correct class:
```
<body class="claro">

```
## JavaScript doesn’t run or the form does nothing
**Symptoms:**
- You click **Submit** and nothing happens.
- No results show up.

**Fix:**
- Make sure `app.js` is linked correctly in your HTML:
```
<script src="app.js"></script>

```
- Check for typos in widget IDs (for example "`submitBtn`").
- Open your browser’s **Console (F12)** to look for JavaScript errors.

## `require()` modules fail to load
**Symptoms:**
- You get error messages such as `Uncaught Error: Could not load module 'dijit/form/TextBox'`.
- White screen with no functionality.

**Fix:**
- Confirm your `<script src="...dojo/dojo.js">` is correct.
- If you're using a local copy of Dojo, verify the folder paths.
- If you're using the CDN, check your internet connection.

## Email validation never passes
**Symptoms:**
- You enter a valid email like `test@example.com` and it still shows an error.

**Fix:**
- Double-check your `regExp` attribute. Here's a safe version:
```
regExp="^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$"

```
Note the double backslashes (\\) which are required inside HTML attribute values.

## The form reloads the page on submit
**Symptoms:**
- When clicking the button, the page reloads and form data disappears.

**Fix:**
- Make sure the button has `type="button"` — not `"submit"` — to avoid triggering form submission:
```
<button data-dojo-type="dijit/form/Button" type="button">Submit</button>

```

## Still stuck?
- Check your browser console for errors (`Ctrl+Shift+J`)
- Make sure Dojo is fully loaded before running any code (`dojo/domReady!`)
- Visit the [Dojo Toolkit documentation](https://dojotoolkit.org/documentation/) for reference

[Back to Tutorial](./Tutorial)