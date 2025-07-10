# Set up a portfolio page with HTML
_Exported on 7/9/2025 at 10:42:07 GMT+2 from Cursor (1.2.2)_

---

**User**

@/TestPortfolio  Alright, so now I need to set up a portfolio page using HTML and CSS. I've gotten started: The goall, if possible to do with HTML and CSS alone, is to have a "[PRESS ENTER]" starting point for opening up the gallery. Then I want to use grid to present the contents of my portfolio.

---

**Cursor**

Of course! That's a great goal. Creating a portfolio with a unique entry animation is a nice touch.

The idea of a "[PRESS ENTER]" start is interesting. Detecting a specific key press like 'Enter' requires JavaScript. However, we can create a very similar "click to enter" experience using only HTML and CSS, which is a clever and powerful technique.

My proposal is to use a hidden checkbox that acts as a switch.
1.  We'll have a full-screen `<label>` that says "[PRESS ENTER]" which the user can click.
2.  Clicking this label will toggle a hidden `<input type="checkbox">`.
3.  We'll use the checkbox's `:checked` state in CSS to hide the splash screen and reveal your portfolio grid.

This approach achieves the effect you're looking for using just the languages you want to focus on.

How does that sound to you? If you're on board, I can guide you through the necessary changes to your `index.html` and `style.css` files.

---

**User**

Yes please :)

---

**Cursor**

Great! Let's start with your `index.html` file.

We'll add three main elements to the `<body>`:

1.  An `<input type="checkbox">` which will be our hidden switch.
2.  A `<label>` that will act as our full-screen splash page. Clicking this label will toggle the checkbox.
3.  A `<main>` element that will hold your actual portfolio content, which will be hidden initially.

Here are the changes for `index.html`:

```html:index.html
// ... existing code ...
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Portfolio</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <input type="checkbox" id="enter-checkbox" />
    <label for="enter-checkbox" id="splash-screen">
        <div class="splash-content">
            <h1>Welcome</h1>
            <span>[PRESS ENTER]</span>
        </div>
    </label>

    <main id="portfolio-content">
        <!-- Your portfolio grid will go here -->
    </main>
</body>
</html>
```

Key things to note:
*   The `<label>` has a `for` attribute that is linked to the `id` of the `<input>`. This is how clicking the label toggles the checkbox.
*   We've wrapped the main content in a `<main>` tag with an ID of `portfolio-content`. This will make it easy to target with CSS.

Once you've made these changes, we can move on to the `style.css` file to make it all work. Let me know when you're ready

```html
// ... existing code ...
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Portfolio</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <input type="checkbox" id="enter-checkbox" />
    <label for="enter-checkbox" id="splash-screen">
        <div class="splash-content">
            <h1>Welcome</h1>
            <span>[PRESS ENTER]</span>
        </div>
    </label>

    <main id="portfolio-content">
        <!-- Your portfolio grid will go here -->
    </main>
</body>
</html>
```

