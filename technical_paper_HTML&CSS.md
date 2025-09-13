# HTML & CSS
# CSS Box Model

## Introduction

The CSS box model is a fundamental concept in web design and layout. It treats every HTML element as a rectangular box consisting of several layers that define the element's size and spacing. Understanding the box model is essential for controlling the design and layout of web pages effectively.

## Components of the Box Model

Each element is composed of four main parts, from inside out:

### 1. Content

The innermost area where text, images, or other media appear. The size of this area is controlled by the `width` and `height` properties.

### 2. Padding

The space between the content and the border. Padding clears an area around the content and is transparent. It can be set individually on each side (top, right, bottom, left) using properties like `padding-top`, `padding-right`, etc.

### 3. Border

The border wraps around the padding and content. It can have width, style, and color, and can also be set individually for each side (`border-top`, `border-right`, etc.).

### 4. Margin

The outermost transparent space that separates the element from other elements. Margins do not have a background color and are completely transparent. Margins can also be set individually on each side.

## Calculating Element Size

When you set the `width` and `height` of an element in CSS, you are defining the size of the **content area only**. The total visible size of the element is calculated by adding the padding, border, and optionally the margin.


Margins add extra space outside the border but are not included in the element’s total width and height.

## Example
```css
.box {
  width: 300px;
  height: 100px;
  padding: 20px;
  border: 5px solid black;
  margin: 15px;
  background-color: lightblue;
}

```
### Box-Sizing Property
By default, the box model uses the "content-box" sizing, where width and height apply only to the content area. Using box-sizing: border-box; changes this behavior so that padding and border are included within the specified width and height, making layout calculations easier.
# Inline vs Block Elements in HTML

Understanding the difference between **inline** and **block** elements is essential for structuring and styling web pages effectively.

---

##  Block Elements

- Start on a **new line**
- Take up the **full width** available (by default)
- Can contain **inline** or other block elements
- Commonly used for **structural layout**

###  Examples of Block Elements:

```html
<div>...</div>
<p>...</p>
<h1>...</h1>
<ul>...</ul>
<li>...</li>
<section>...</section>
<header>...</header>
<footer>...</footer>
```

###  Default Behavior:

```html
<p>This is a paragraph.</p>
<div>This is a div.</div>
```

Both will appear on separate lines, one after another.

---

##  Inline Elements

- Do **not** start on a new line
- Only take up as much width as needed
- Can contain **text** and other inline elements
- Commonly used for **formatting inside block elements**

###  Examples of Inline Elements:

```html
<span>...</span>
<a href="#">...</a>
<strong>...</strong>
<em>...</em>
<img src="..." />
<code>...</code>
```

###  Default Behavior:

```html
<p>This is <strong>bold</strong> and <em>italic</em> text.</p>
```

All inline elements will appear **within** the flow of the paragraph.

---

## Tip

You can change the default behavior using CSS:

```css
div {
  display: inline;
}

span {
  display: block;
}
```

This allows flexibility when styling HTML elements for different layouts.

---
# CSS Positioning: Relative vs Absolute

CSS `position` property allows you to control how elements are placed in the document flow. Two of the most common values are **relative** and **absolute**.

---

##  position: relative;

- The element is positioned **relative to its normal position**.
- It **still takes up space** in the document flow.
- Offsets like `top`, `right`, `bottom`, `left` will move it from its original location **without affecting other elements**.

###  Example:

```html
<div class="box relative-box">Relative Box</div>
```

```css
.relative-box {
  position: relative;
  top: 20px;
  left: 30px;
}
```

### Behavior:

- The box appears **20px lower** and **30px to the right** of where it normally would be.
- It still **reserves space** in its original location.

---

##  position: absolute;

- The element is positioned **relative to the nearest positioned ancestor** (`relative`, `absolute`, or `fixed`).
- If no such ancestor exists, it's positioned **relative to the `<html>` or `<body>` element**.
- It is **removed from the normal document flow**, so it does **not reserve space**.

###  Behavior:

- The `.absolute-box` will be placed **10px from the top and right** of its `.wrapper` container.
- Since it's removed from the flow, it may **overlap** other elements.

---

## Tip

Use `position: absolute` inside a `position: relative` container for **controlled positioning**:

```html
<div class="container">
  <div class="tooltip">Tooltip text</div>
</div>
```

```css
.container {
  position: relative;
}

.tooltip {
  position: absolute;
  top: 100%;
  left: 0;
}
```

## Common CSS Structural Classes

- container  
- row  
- col / column  
- wrapper  
- section  
- header  
- footer  
- main  
- aside  
- content  
- nav  
- card  

## Common CSS Styling Classes

- text-center  
- text-left / text-right  
- bg-light / bg-dark / bg-primary  
- btn / btn-primary / btn-secondary  
- rounded / rounded-full  
- shadow / shadow-lg  
- m-0 / m-1 / m-auto (margin utilities)  
- p-0 / p-1 / p-auto (padding utilities)  
- d-block / d-inline / d-flex (display utilities)  
- hidden / visible  
- border / border-0 / border-primary  

# CSS Specificity

CSS Specificity is a set of rules browsers use to determine which CSS rule applies to an element when multiple rules could apply. Understanding specificity helps you write CSS that behaves predictably and prevents unexpected style overrides.

---

## What is Specificity?

- Specificity is a **weight** or **ranking system** for CSS selectors.
- When multiple CSS rules target the same element, the rule with the **highest specificity** wins.
- Specificity is calculated based on the types of selectors used in the rule.

---

## How Specificity is Calculated

Specificity is typically represented as a 4-part value: **(a, b, c, d)**

- **a** = Inline styles (e.g., style="...") — either 1 or 0  
- **b** = Number of ID selectors (e.g., `#header`)  
- **c** = Number of class selectors, attributes selectors, and pseudo-classes (e.g., `.menu`, `[type="text"]`, `:hover`)  
- **d** = Number of element (type) selectors and pseudo-elements (e.g., `div`, `h1`, `::before`)

The higher the value starting from `a` down to `d`, the higher the specificity.

---

## Specificity Ranking Examples

| Selector                     | Specificity (a,b,c,d) | Explanation                          |
|------------------------------|----------------------|------------------------------------|
| Inline style (`style=""`)     | (1,0,0,0)            | Highest specificity                |
| ID selector (`#navbar`)       | (0,1,0,0)            | High specificity                   |
| Class selector (`.button`)    | (0,0,1,0)            | Medium specificity                 |
| Attribute selector (`[type="text"]`) | (0,0,1,0)      | Same as class selector             |
| Pseudo-class (`:hover`)       | (0,0,1,0)            | Same as class selector             |
| Element selector (`div`)      | (0,0,0,1)            | Low specificity                   |
| Pseudo-element (`::before`)   | (0,0,0,1)            | Same as element selector           |
| Universal selector (`*`)      | (0,0,0,0)            | No specificity                    |

---


## CSS Responsive Queries

- Use media queries to apply styles based on screen size  
- Common breakpoints:  
  - max-width: 576px (mobile)  
  - min-width: 577px and max-width: 768px (tablet)  
  - min-width: 769px and max-width: 992px (small desktop)  
  - min-width: 993px and max-width: 1200px (large desktop)  
  - min-width: 1201px (extra large screens)    

## Flexbox / Grid

### Flexbox

Flexbox (Flexible Box Layout) is a CSS layout module designed for arranging items in a **one-dimensional** row or column. It makes it easier to design flexible and responsive layout structures without using floats or positioning.

- Designed for **one-dimensional layouts** — either a row or a column.
- Allows flexible distribution of space among items inside a container.
- Items can grow, shrink, and be aligned easily.

#### Common Properties:

- `display: flex;` — defines a flex container and enables flex context for its children.
- `flex-direction` — sets the direction of the flex items (row, row-reverse, column, column-reverse).
- `justify-content` — aligns items horizontally along the main axis (start, center, space-between, space-around, etc.).
- `align-items` — aligns items vertically along the cross axis (stretch, center, flex-start, flex-end).
- `flex-wrap` — controls whether flex items wrap onto multiple lines or stay on one line (`nowrap`, `wrap`, `wrap-reverse`).
- `flex-grow`, `flex-shrink`, `flex-basis` — control item flexibility and size.

---

### Grid

CSS Grid Layout is a powerful layout system for creating **two-dimensional** grid-based designs. It allows control over both rows and columns, making it ideal for complex layouts.

- Designed for **two-dimensional layouts** — rows and columns simultaneously.
- Provides precise control over layout structure.
- Supports explicit and implicit grid tracks, areas, and alignment.

#### Common Properties:

- `display: grid;` — defines a grid container and enables grid context for its children.
- `grid-template-columns` — defines the number and size of columns.
- `grid-template-rows` — defines the number and size of rows.
- `gap` (or `grid-gap`) — sets the spacing between rows and columns.
- `grid-column`, `grid-row` — specify where an item starts and ends within the grid.
- `justify-items` — aligns items along the inline (row) axis inside their grid areas.
- `align-items` — aligns items along the block (column) axis inside their grid areas.
- `grid-template-areas` — defines named grid areas for layout.

---

Both Flexbox and Grid complement each other — Flexbox excels at laying out items in a single dimension, while Grid is perfect for complex two-dimensional layouts.

---
# Common Header Meta Tags

Meta tags are placed in the `<head>` section of an HTML document. They provide metadata about the HTML page — information that is not directly visible to users but is used by browsers, search engines, and other web services.

---

## charset="UTF-8"

```html
<meta charset="UTF-8">
```

- Defines the character encoding used by the document.
- `UTF-8` (Unicode Transformation Format) is the most common encoding, supporting virtually all characters from all languages.
- Ensures that special characters (like ñ, €, ✓) display correctly in all browsers.

**Why use it?**  
To avoid character corruption and ensure consistent text rendering across browsers and platforms.

---

## name="viewport" content="width=device-width, initial-scale=1.0"

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- Controls how the website displays on mobile and tablet devices.
- `width=device-width` makes the page width match the screen width of the device.
- `initial-scale=1.0` sets the initial zoom level when the page loads.

**Why use it?**  
Essential for responsive design. Without this tag, your site may look zoomed out or squished on mobile devices.

---

## http-equiv="X-UA-Compatible" content="IE=edge"

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```

- Tells Internet Explorer to use the latest rendering engine available.
- Prevents the browser from falling back to an older compatibility mode.

**Why use it?**  
To ensure your site renders properly in older versions of Internet Explorer by using the best rendering engine.

---

## name="description" content="Brief description of the page"

```html
<meta name="description" content="Brief description of the page">
```

- Provides a summary of the webpage content.
- Often used by search engines to display in search result snippets.

**Why use it?**  
Improves SEO (Search Engine Optimization) and helps users understand what your page is about before clicking the link in search results.

---

## name="keywords" content="HTML, CSS, JavaScript"

```html
<meta name="keywords" content="HTML, CSS, JavaScript">
```

- A comma-separated list of keywords relevant to the page content.
- Historically used by search engines to categorize content.

**Why use it?**  
Not heavily used by modern search engines anymore, but can still offer minor SEO benefit or metadata clarity.

---

## name="author" content="Your Name"

```html
<meta name="author" content="Your Name">
```

- Specifies the name of the author or creator of the page.
- Useful for documentation, ownership attribution, and content management.

**Why use it?**  
Good for project documentation and helpful when multiple developers are collaborating on the same project.

---

## Summary Table

| Meta Tag                                   | Purpose                                                   |
|--------------------------------------------|------------------------------------------------------------|
| `<meta charset="UTF-8">`                   | Sets character encoding                                    |
| `<meta name="viewport" ...>`               | Makes site responsive on mobile devices                   |
| `<meta http-equiv="X-UA-Compatible" ...>`  | Ensures best rendering in Internet Explorer               |
| `<meta name="description" ...>`            | SEO summary for search engines                            |
| `<meta name="keywords" ...>`               | Legacy SEO keyword tag                                    |
| `<meta name="author" ...>`                 | Identifies the page author                                |

---