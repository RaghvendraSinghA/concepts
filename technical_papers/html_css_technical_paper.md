# Technical Paper on HTML and CSS


## Introduction

HTML and CSS are the two fundamental technologies used to build and style web pages.     
HTML (HyperText Markup Language) defines the structure and semantic meaning of content.       
CSS (Cascading Style Sheets) controls the presentation and layout of that content.



## 1. CSS Box Model

The CSS Box Model describes how the browser represents every HTML element as a rectangular box.

The box consists of four main areas:

<img src="https://miro.medium.com/v2/resize:fit:804/format:webp/1*ydgkPlP_bYrNp9FxxjYHFw.gif"
    alt="CSS Box Model" width="500">

The four parts are:

1. Content   (The content is the actual information inside the element like image, video, text etc).
2. Padding   (Padding creates space between the content and border).
3. Border    (The border surrounds the padding and content).
4. Margin    (Margin creates space outside the border).

Using these we can change BOX model of an element.

---


### box-sizing

Box-sizing is used to declare size of box-model of an element.

The default value is:

```css
box-sizing: content-box;
```

With `content-box`, the declared width represents only the content area.

For example:

```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
}
```

The total width becomes:

300 + 20 + 20 + 5 + 5
= 350px

A common CSS reset is:

```css
* {
    box-sizing: border-box;
}
```

With `border-box`, the declared width includes the content, padding, and border.

Therefore:

```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

The total width remains `300px`. It fits border, content and padding in 300px .

---

## 2. Inline vs Block Elements

HTML elements can participate in layout as block-level or inline-level elements.

### 2.1 Block Elements

Block elements generally:
* Start on a new line.
* Take whole horizontal space by default.
* Allow width and height to be controlled.
  
  Examples: div, p, h1, etc.

---

### 2.2 Inline Elements

Inline elements generally:

* Remain on the current line.
* Take only the width required by their content.
* Are commonly used within text.     

  Examples: span, a, strong, label etc.
---

### 2.3 `inline-block`

`inline-block` combines characteristics of inline and block layout to an element.

```css
.header_div {
    display: inline-block;
    width: 100px;
    padding: 10px;
}
```

The element can appear alongside other inline content while accepting dimensions.

---

### 2.4 CSS Display Property

The `display` property controls how an element participates in layout.

Common values include:

```css
display: block;  
display: inline;
display: inline-block;
display: flex;
display: grid;
display: none;
```
---

## 3. CSS Positioning

The `position` property controls how an element is positioned.

Common values are:

```css
static
relative
absolute
fixed
sticky
```

---

### 3.1 Static

Static positioning is the default.
```css
.box {
    position: static;
}
```
The element follows normal document flow.

---

### 3.2 Relative

```css
.box {
    position: relative;
    top: 20px;
    left: 10px;
}
```
The element remains in normal document flow but is visually offset from its original position.

`relative` is also commonly used to establish a containing block for absolute positioned descendants.

Example:

```css
.parent {
    position: relative;
}

.child {
    position: absolute;
    top: 0;
    right: 0;
}
```

---

### 3.3 Absolute

```css
.child {
    position: absolute;
    top: 10px;
    right: 20px;
}
```

An absolutely positioned element is removed from normal document flow and positioned relative to an appropriate containing block.
It is positioned according to a parent or grand-parent who have position: relative.

Example:

```css
.card {
    position: relative;
}

.badge {
    position: absolute;
    top: 10px;
    right: 10px;
}
```

---

### 3.4 Fixed

```css
.header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
}
```

A fixed-positioned element is positioned relative to the viewport and generally remains in place even after scrolling    
down.

---

### 3.5 Sticky

```css
.header {
    position: sticky;
    top: 0;
}
```

A sticky element behaves like a normally positioned element until it reaches the specified threshold   
It can stick to bottom or top and will not go out of screen-window.

---

## 4. Common CSS Structural Classes

CSS classes are often used to represent the structure of a page.

Common examples:

```text
.container
.wrapper
.header
.nav
.main
.content
```

Example:

```html
<div class="container">

    <header class="header">
        ...
    </header>

    <main class="main">
        ...
    </main>

    <footer class="footer">
        ...
    </footer>

</div>
```

Example CSS:

```css
.container {
    width: min(100% - 2rem, 1200px);
    margin-inline: auto;
}

.main {
    display: grid;
    grid-template-columns: 1fr 300px;
    gap: 2rem;
}
```

Structural classes should describe the role of a component rather than its visual appearance.

---

## 5. Common CSS Styling Classes

Reusable styling or utility-like classes can be created for common styles.

Examples:

```text
.text-center
.text-left
.text-right
.text-bold
.hidden
```

Example:

```css
.text-center {
    text-align: center;
}

.text-bold {
    font-weight: bold;
}

.rounded {
    border-radius: 8px;
}

.full-width {
    width: 100%;
}
```

The exact naming convention depends on the project's CSS architecture.

---


## 6. CSS Specificity

Specificity determines which CSS declaration wins when multiple declarations apply to the same element.

A simplified priority order is:

```text

!important declaration > Inline style > ID selector > Class / Attribute / Pseudo-class > Element / Pseudo-element >Inherited styles

```

Example:

```css
p {
    color: blue;
}

.text {
    color: green;
}

#message {
    color: red;
}
```

HTML:

```html
<p id="message" class="text">
    Hello
</p>
```

The ID selector has higher specificity than the class and element selectors, so the text becomes red.

---

## 7. Responsive Web Design

Responsive Web Design means designing websites that adapt to different screen sizes and devices.

A responsive website should work well on:

```text
Mobile, Tablet, Laptop, Desktop, Large screens
```

Responsive design commonly uses:

* Relative units
* Flexbox
* CSS Grid
* Media queries

For example:

```css
.container {
    width: min(100% - 2rem, 1200px);
    margin-inline: auto;
}
```

This allows the container to shrink on smaller screens while remaining constrained on larger screens.

---

## 8. CSS Media Queries

Media queries allow CSS to apply conditionally based on the environment, such as viewport width or orientation.

Syntax:

```css
@media (condition) {
    /* CSS rules */
}
```

Example:

```css
.container {
    width: 100%;
}

@media (min-width: 768px) {
    .container {
        width: 750px;
    }
}
```

---

### 8.1 `max-width`

```css
@media (max-width: 600px) {
    .sidebar {
        display: none;
    }
}
```

---

### 8.2 `min-width`

```css
@media (min-width: 768px) {
    .container {
        max-width: 1200px;
    }
}
```

---

### 8.3 Orientation

```css
@media (orientation: landscape) {
    body {
        background: lightgray;
    }
}
```

---

### 8.4 Multiple Conditions

```css
@media (min-width: 768px) and (max-width: 1200px) {
    .container {
        padding: 20px;
    }
}
```

Modern media query syntax also supports range expressions:

```css
@media (width >= 768px) {
    .container {
        padding: 2rem;
    }
}
```
---


## 9. Flexbox
Flexbox is a one-dimensional CSS layout system.
It is useful for arranging elements along a row or column.

Basic example:

```css
.container {
    display: flex;
}
```

Now .container have flexbox property, Next we will see how to change elements inside flexbox.

### 9.1 flex-direction

```css
.container {
    display: flex;
    flex-direction: row;
}
```

flex-direction :row ; means elements inside flexbox will be arranged left to right in row (default).

Possible values:

```text
row
row-reverse
column
column-reverse
```

---

### 9.2 justify-content

Controls distribution along the main axis. justify-content controls horizontal/main-axis alignment by default.        
But, if we use flex-direction: column then, main axis will be changed from horizontal(x) to vertical(y) axis.


```css
.container {
    display: flex;
    justify-content: center;
}
```

Common values:

```text
flex-start
center
flex-end
space-between
space-around
space-evenly
```

---

### 9.3 align-items

Controls alignment along the cross axis. align-items controls vertical/cross-axis.        
But, if we use flex-direction: column; then, cross-axis will be changed from vertical(y) to horizontal(x) axis.

```css
.container {
    display: flex;
    align-items: center;
}
```

---

### 9.4 gap

Adds spacing between flex items.

```css
.container {
    display: flex;
    gap: 20px;
}
```

---

### 9.5 flex-wrap

Allows items to move onto multiple lines.

```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```

---

### 9.6 flex

The `flex` shorthand can represent:

```text
flex-grow
flex-shrink
flex-basis
```
---

## 10. CSS Grid

CSS Grid is primarily a two-dimensional layout system.
It allows developers to control rows and columns.    

Example:

```css
.container {
    display: grid;
}
```
---

### 10.1 Grid Columns

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```
This creates three equal columns.

---

### 10.2 Grid Rows

```css
.container {
    display: grid;
    grid-template-rows: 100px 200px;
}
```
This creates 2 rows of size 100px and 200px

---

### 10.3 gap

```css
.container {
    display: grid;
    gap: 20px;
}
```
This creates a 20px gap between rows and columns.


---

### 10.4 repeat()

Instead of:

```css
grid-template-columns: 1fr 1fr 1fr;
```

we can use:

```css
grid-template-columns: repeat(3, 1fr);
```

---

### 10.5 minmax()

```css
grid-template-columns:
    repeat(auto-fit, minmax(200px, 1fr));
```
It means, create as many columns as can fit, where each column is at least 200px wide and can grow    
to fill available space.
This can create responsive card layouts.

---

## 11. Common HTML Meta Tags

Meta tags provide information about an HTML document.
They are placed inside:

```html
<head>
```

---

### 11.1 Character Encoding

```html
<meta charset="UTF-8">
```

Specifies the character encoding of the document.

---

### 11.2 Viewport

```html
<meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
>
```
This is important for responsive webpages, It sets the viewport for rendering website.

---

### 11.3 Description

```html
<meta
    name="description"
    content="Learn HTML and CSS fundamentals."
>
```

Provides a description of the page,This is for screen-reader like AI tools or screen reader for blind people.    
Also for SEO.

---

### 11.4 Robots

```html
<meta name="robots" content="index, follow">
```

Provides instructions to search-engine crawlers.

Web crawlers are automated programs used by search engines to discover and read webpages.   
The robots meta tag provides instructions about whether a page of website should be indexed 
in google search engine database for search result and whether page links can be followed     
to visit and see their contents.

e.g - noindex pages : (payment page, login page)
    - nofollow links : (payment page link, cart page link)

---

### 11.5 Theme Color

```html
<meta name="theme-color" content="#ffffff">
```

Can influence browser UI theming on supported platforms.

---

## 12. CSS Variables

CSS custom properties allow reusable values to be defined.    
Like using this we can store css values in variables and can apply DRY principle.

Example:

```css
:root {
    --primary-color: #2563eb;
    --text-color: #222;
    --spacing: 16px;
}
```

Use them with:

```css
.button {
    background-color: var(--primary-color);
    color: white;
    padding: var(--spacing);
}
```

---

### Fallback Values

It is used to set fallback value of CSS variables.

```css
color: var(--text-color, black);
```

If `--text-color` does not exist, `black` is used.

---

## 13. Pseudo-classes

Pseudo-classes select elements based on their state or position.

Common pseudo-classes:

```text
:hover
:focus
:active
:visited
:first-child
:last-child
:nth-child()
```

Example:

```css
button:hover {
    background-color: darkblue;
}
```

Focus:

```css
input:focus {
    outline: 2px solid blue;
}
```

Nth child:

```css
li:nth-child(2) {
    color: red;
}
```

---

## 14. Pseudo-elements

Pseudo-elements style a specific part of an element or create generated content after     
or before of an element.

Common pseudo-elements:

```text
::before
::after
::first-letter
::first-line
::selection    
```
::selection -: Styles the text when the user selects/highlights it with mouse or touch.

Example:

```css
.title::before {
    content: "★ ";
}
```

---

## 15. Transitions

CSS transitions create smooth changes between states of elements.    
Used with pseudo classes.    

Example:

```css
.button {
    background-color: blue;
    transition: background-color 0.3s ease;
}

.button:hover {
    background-color: darkblue;
}
```

Common transition properties:

```text
transition-property
transition-duration
transition-timing-function
transition-delay
```

Shorthand:

```css
transition: all 0.3s ease;
```
It is generally better to transition only the properties that need animation rather than using `all` indiscriminately.


## 16. Animations
CSS animations allow elements to change styles over time. They are defined using @keyframes.

```css
@keyframes move {
    0% {
        transform: translateX(0);
    }

    50% {
        transform: translateX(100px);
    }

    100% {
        transform: translateX(200px);
    }
}

.box {
    animation: move 2s ease-in-out;
}
```

Common animation properties:

```text
animation-name
animation-duration
animation-timing-function
animation-delay
animation-iteration-count
animation-direction
animation-fill-mode
```

Animation shorthand:

```css
.box {
    animation: move 2s ease-in-out infinite;
}
```

* @keyframes -> defines the animation stages.
* animation-duration -> defines how long the animation takes.
* animation-iteration-count -> defines how many times it runs.
* animation-direction -> controls the direction of the animation.

---
## References

### HTML

- web.dev — Learn HTML
   https://web.dev/learn/html/

### CSS

- MDN Web Docs — CSS
   https://developer.mozilla.org/en-US/docs/Web/CSS

- MDN — CSS Box Model
   https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Box_model

- MDN — CSS Selectors
   https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Selectors

- MDN — CSS Specificity
   https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Specificity

### Layout

- web.dev — CSS Layout
   https://web.dev/learn/css/layout

- web.dev — Flexbox
   https://web.dev/learn/css/flexbox

- web.dev — CSS Grid
    https://web.dev/learn/css/grid

- MDN — CSS Positioning
    https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Positioning

### Responsive Design

- web.dev — Learn Responsive Design
    https://web.dev/learn/design

- MDN — Responsive Web Design
    https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design

- MDN — CSS Media Queries
    https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Media_queries

- MDN — Media Queries
    https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Media_queries


### Extra own topics :

- CSS variables
    W3Schools (https://www.w3schools.com/css/css3_variables.asp)
  
- Pseudo-elements and classes
    W3Schools (https://www.w3schools.com/css/css_pseudo_elements.asp)

- Transition and Animation
    Youtube (dave gray) - (https://youtube.com/playlist?list=PL0Zuz27SZ-6Mx9fd9elt80G1bPcySmWit&si=9EnQ5tAUqO1cF4za)




