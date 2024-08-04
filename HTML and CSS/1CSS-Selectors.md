# CSS-Selectors
## CSS selectors hierarchy
1. Importance - `!important`
2. Inline style- `style`
3. ID selector- `#`
4. class selector- `.`

![](assets/CSS%20cascading%20hiracy.png)In this image tells in css ***most important thing is come from the bottom***
## ex-
  ```html
  <!DOCTYPE html>
  <html lang="en">

  <head>
    <meta charset="UTF-8">
    <title>CSS Selectors</title>
    <link rel="stylesheet" href="./style.css" />
  </head>

  <body>
    <h1>CSS Selectors</h1>
    <h2>Applying CSS to Different Parts of HTML</h2>
    <!-- the CSS for all paragraph tags to "color: red" -->
    <p class="note">1. The element selector targets elements based on their HTML tag name.</p>

    <ol>
      <!-- the CSS for all elements with a class of "note" to "font-size: 20px" -->
      <li class="note">Class selectors target elements based on the value of the class attribute.</li>

      <!-- the CSS for the element with an id of "id-selector-demo" to "color: green" -->
      <li class="note" id="id-selector-demo" value="3">ID selectors target elements based on the value of the id
        attribute.</li>

      <!-- the li elements that have the "value" attribute set to "4" to have "color: blue" -->
      <li class="note" value="4">Attribute selectors target elements based on their attributes and values.</li>

      <!-- all elements to have "text-align: center" -->
      <li class="note" value="5">The universal selector targets all elements.</li>
    </ol>
  </body>

  </html>
  ```

- ./style.css
  ```css
  /* apply styles for ordered list */
  ol {
    margin-left: -40px;
    margin-top: -20px;
    list-style-position: inside;
  }

  /* all the contain with in <p> will be red */
  p {
    color: red;
  }

  /* selecting a CSS class called "note" */
  .note{
    font-size: 20px
  }

  /* selecting CSS id */
  #id-selector-demo{
    color: green
  }

  /* selecting <li> elements which only has "value=4" attribute */
  li[value="4"]{
    color: blue
  }

  /* selecting all the items using universal selector(*) */
  *{
    text-align: center;
  }
  ```
- Output
  ![](assets/Pasted%20image%2020240513142302.png)
