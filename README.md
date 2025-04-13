<!---
{
  "id": "b1d02de5-2283-4672-bcbf-a4c81fcad440",
  "depends_on": ["1f867627-725b-40f7-9ecd-d1072c941367"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-04-13",
  "keywords": ["HTML", "anchor", "event handling", "JavaScript", "preventDefault"]
}
--->

# Intercepting Anchor Clicks with JavaScript

> In this exercise you will learn how to intercept anchor (`<a>`) click events using JavaScript and trigger custom actions instead of letting the browser follow the link. Furthermore we will explore how to use `preventDefault()` to override native browser navigation behavior and use it to create interactive web interfaces.

## Introduction

Anchor elements (`<a>`) are a foundational part of the web, enabling users to move from one page to another. Under normal circumstances, clicking an anchor with an `href` attribute causes the browser to immediately navigate to the target location, unloading the current page and requesting a new one. This default behavior is deeply embedded in the browser’s functionality and is what enables traditional multi-page navigation.

However, there are many cases where you may want to handle a click event on a link differently. For example:

- Show a confirmation popup before leaving the page
- Open a modal dialog instead of navigating away
- Log a user action for analytics
- Perform a validation step before continuing
- Trigger a file download or API request

To support such behavior, the browser has a built-in system for handling **events** — such as clicks, keypresses, or mouse movement. When a user interacts with a page, the browser **detects the interaction and creates an event object**, such as a `MouseEvent` for clicks. This object contains information about the interaction and is **dispatched to the relevant DOM element**.

This dispatch system is part of what’s called the **event loop** in modern browsers. The JavaScript engine is already tightly integrated with this mechanism. Developers can **“listen”** for events using methods like `addEventListener`. When the browser dispatches an event (like a click on a link), any matching listener gets called and receives the event object.

Using this object, developers can call `event.preventDefault()`, which tells the browser to **cancel its default behavior** — in this case, navigating to the `href`. The developer can then perform something else entirely, like logging or opening a popup.

By mastering this interaction pattern, you will gain hands-on experience with JavaScript-driven behavior control, a fundamental stepping stone toward building your own interactive components and dynamic logic.


### Further Readings and Other Sources

- [MDN: preventDefault](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
- [JavaScript Event Handling Basics](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- [YouTube: Understanding Event Listeners](https://www.youtube.com/watch?v=XF1_MlZ5l6M)

## Tasks

### Task 1: Create an HTML File That Intercepts a Link

Open your terminal and create a new file called `intercept.html` using `vim`:

```bash
vim intercept.html
```

Paste the following into the file:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Anchor Intercept Demo</title>
    <script>
      function handleClick(event) {
        event.preventDefault();
        alert("This link was intercepted! No page load occurred.");
      }

      window.onload = function () {
        const link = document.getElementById("intercepted-link");
        link.addEventListener("click", handleClick);
      };
    </script>
  </head>
  <body>
    <h1>Intercepting Anchor Behavior</h1>
    <p>
      <a id="intercepted-link" href="https://example.com">Click Me</a>
    </p>
    <p>
      <a href="https://example.com">This one behaves normally</a>
    </p>
  </body>
</html>
```

This HTML includes one normal link and one with an ID that is targeted by JavaScript. The `handleClick` function intercepts the click event, cancels the browser’s default navigation using `preventDefault()`, and instead displays an alert box.

Save the file and open it in your browser according to your platform.

Click both links and observe the difference in behavior.

### Task 2: Replace the Alert with a Console Log

Let’s replace the alert with a quieter alternative using the browser console.

In the `<script>` block, change the `alert(...)` line to:

```js
console.log("Custom action logged.");
```

Reload the page in your browser, press `F12` or open the developer tools, and go to the “Console” tab. Click the link again. You should see the log message appear instead of an alert.

This is helpful for debugging or writing apps where you don’t want to interrupt the user with a popup.

### Task 3: Intercept Multiple Links Dynamically

Now extend your script to intercept several links by class name.

1. Add these links to the body:

```html
<a href="https://test.com" class="intercept">Another Link</a><br>
<a href="https://elsewhere.com" class="intercept">And Another</a>
```

2. Modify the `window.onload` block:

```js
window.onload = function () {
  const links = document.querySelectorAll("a.intercept");
  links.forEach(link => link.addEventListener("click", handleClick));
};
```

Now every `<a>` with `class="intercept"` is intercepted and triggers the custom behavior.

This pattern is the basis for frameworks like Angular and React, which intercept user actions and control navigation through JavaScript.

## Questions

1. What does `event.preventDefault()` actually do?
2. How would you allow some links to navigate while others don't?
3. Why is `window.onload` used here instead of placing `<script>` at the end of the body?
4. What would happen if you didn’t call `preventDefault()`?
5. Could you trigger manual navigation via `window.location.href = ...` inside the handler?

## Advice

This exercise demonstrates a fundamental technique in web development: overriding the browser’s default behavior to implement your own logic. It's a foundational skill for modern JavaScript applications. Understanding this concept prepares you to grasp how routers in Angular and other frameworks work. Mastering event interception and flow control is the first step to building truly interactive and dynamic web interfaces.

