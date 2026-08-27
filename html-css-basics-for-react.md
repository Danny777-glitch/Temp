 # HTML + CSS Basics — Just Enough for React

Don't panic. You don't need to master HTML/CSS — you need the ~20% that shows up constantly in JSX. This covers exactly that.

---

## PART A: HTML Basics

### 1. What HTML actually is
HTML = **HyperText Markup Language**. It's not a programming language — it just describes the *structure* of a page using **tags**.

```html
<h1>This is a heading</h1>
<p>This is a paragraph.</p>
```
- Most tags come in pairs: `<tagname>content</tagname>`
- Some tags are "self-closing" (no content inside): `<img />`, `<br />`, `<input />`

### 2. The Basic Page Skeleton
```html
<!DOCTYPE html>
<html>
  <head>
    <title>My Page</title>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```
- `<head>` = metadata (title, links to CSS) — not visible on the page
- `<body>` = everything visible on the page

### 3. The Tags You'll Actually See in React/JSX
| Tag | Meaning |
|---|---|
| `<div>` | A generic box/container (most used tag, no special meaning) |
| `<span>` | A generic inline container (for small bits of text) |
| `<h1>` to `<h6>` | Headings, h1 = biggest/most important |
| `<p>` | Paragraph of text |
| `<a href="...">` | A link |
| `<img src="..." />` | An image |
| `<ul>` / `<ol>` | Unordered (bullets) / Ordered (numbered) list |
| `<li>` | A list item, goes inside `<ul>` or `<ol>` |
| `<button>` | A clickable button |
| `<input />` | A text/number/etc. input field |
| `<form>` | Wraps inputs + a submit button |

```html
<div>
  <h2>My Todo List</h2>
  <ul>
    <li>Study React</li>
    <li>Study HTML</li>
  </ul>
  <button>Add Task</button>
</div>
```
*This is basically what your JSX looks like — JSX is just this, written inside JavaScript.*

### 4. Attributes
Extra info added inside the opening tag:
```html
<img src="cat.jpg" alt="A cat" width="200" />
<a href="https://google.com">Go to Google</a>
```
In JSX, the two you'll fight with most are:
- `class` → becomes `className` in JSX
- `for` → becomes `htmlFor` in JSX
(Because `class` and `for` are reserved words in JavaScript.)

---

## PART B: CSS Basics

### 1. What CSS is
CSS = **Cascading Style Sheets**. It controls how HTML *looks* (colors, spacing, layout, fonts).

**Syntax:**
```css
selector {
  property: value;
}
```
```css
p {
  color: blue;
  font-size: 18px;
}
```
This says: "every `<p>` tag, make the text blue and 18px."

### 2. Three Ways to Apply CSS
```html
<!-- 1. Inline (on the tag itself) -->
<p style="color: red;">Red text</p>

<!-- 2. Internal (inside <head>) -->
<style>
  p { color: red; }
</style>

<!-- 3. External (separate .css file, most common) -->
<link rel="stylesheet" href="style.css" />
```
React mostly uses external (or CSS Modules) + sometimes inline style **objects** (different syntax — see below).

### 3. Selectors (how you "target" elements to style)
```css
p { color: black; }              /* every <p> */
.card { padding: 10px; }         /* every element with class="card" */
#header { background: gray; }    /* the one element with id="header" */
```
- `.classname` → class selector (use `className="card"` in HTML/JSX — reusable, most common)
- `#idname` → id selector (use `id="header"` — for one unique element)

```html
<div class="card">I'm styled by the .card rule</div>
```

### 4. The Box Model (the #1 CSS concept to understand)
Every HTML element is a rectangular box made of 4 layers, from inside out:

```
margin (space outside the border)
  border (the edge line)
    padding (space inside the border, around content)
      content (the actual text/image)
```
```css
.box {
  width: 200px;
  padding: 10px;      /* space inside the box */
  border: 2px solid black;
  margin: 20px;        /* space outside the box, pushing other elements away */
}
```

### 5. Common Layout Properties
| Property             | What it does                                                   |
| -------------------- | -------------------------------------------------------------- |
| `color`              | text color                                                     |
| `background-color`   | box's background color                                         |
| `font-size`          | text size                                                      |
| `display: flex`      | turns children into a flexible row/column layout (very common) |
| `display: none`      | hides the element                                              |
| `text-align: center` | centers text                                                   |
| `border-radius`      | rounds corners                                                 |

**Flexbox mini-example (used everywhere in real apps):**
```css
.container {
  display: flex;
  justify-content: space-between; /* spreads children horizontally */
  align-items: center;            /* centers them vertically */
}
```

### 6. CSS in React (how it differs slightly)
Inline styles in JSX are a **JavaScript object**, not a string:
```jsx
// Plain HTML: style="color: red; font-size: 20px;"
// JSX:
<div style={{ color: "red", fontSize: "20px" }}>Hello</div>
```
Notice:
- `{{ }}` — outer `{}` = "this is JS", inner `{}` = the object itself
- `font-size` → `fontSize` (camelCase, no hyphens allowed in JS object keys)
- Values are strings: `"20px"`, `"red"`

---

## PART C: Putting It Together — One Full Example

```html
<!-- style.css -->
<style>
  .card {
    border: 1px solid #ccc;
    padding: 16px;
    border-radius: 8px;
    display: flex;
    justify-content: space-between;
  }
</style>

<!-- HTML -->
<div class="card">
  <h3>Product Name</h3>
  <button>Buy Now</button>
</div>
```

Same thing in React/JSX:
```jsx
function ProductCard() {
  return (
    <div className="card">
      <h3>Product Name</h3>
      <button>Buy Now</button>
    </div>
  );
}
```

**That's it** — this covers pretty much everything you'll need to read/write JSX comfortably and understand the "Styling React" part of your syllabus.

---

## Quick Self-Check
1. What does `<div>` mean and why is it used so much?
2. What's the difference between a class selector and an id selector?
3. Name the 4 layers of the box model, inside to outside.
4. Why is it `className` instead of `class` in JSX?
5. Write the JSX version of `style="background-color: blue; font-size: 14px;"`

If you can answer these, you have enough HTML/CSS to fully understand your React syllabus. Don't try to "master" HTML/CSS right now — you just needed the vocabulary, and now you have it. 💪
