# CSS CHEATSHEAT

## What is CSS

Created by World Wide Web Consortium (W3C), CSS stands for Cascading Style Sheets, and describes how HTML elements are to be displayed on screen, paper, or in other media.

While HTML was created to describe the content of a web page, CSS describes the styles for the HTML contents of the web page.

## 3 ways of importing CSS

### Inline (directly in HTML)

Adding styles trough `style` attr.

```html
<h1 style="color:blue;margin-left: 20px;">Hello there!</h1>
```

### Internal style sheet (using the `<style>` tag)

Adding it to your header with `style` tag

```html
<style>
  body {
    background-color: red;
  }
</style>
```

### External style sheet (imported in the HTML document)

Practically this suggests that the styles be externalized to a `.css` file,
which is the cleanest way to handle css when having a lot of different UI components.

```html
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

### Ordering

How does CSS cascades itself? Prioritizing styles is often great headache for developers.

CSS operates on strict series of rules. Generally speaking we can say that all the styles will “cascade” into a new “virtual” style sheet based on a strict order of overriding. The order in which styles override each other is:

- Inline style (inside an HTML element)
- External and internal style sheets (in the head section)
- Browser default

So, an inline style (inside a specific HTML element) has the highest priority, which means that it will override a style defined inside the <head> tag, or in an external style sheet, or a browser default value.

One more critical override is `!important`. This will override even the inline style.

Take a look at this.

```html
<div class="red" id="some_id"></div>
```

```css
div {
  background-color: red;
}

#some_id {
  background-color: blue;
}

.red {
  background-color: green;
}
```

What will be the background color? Looking at the sematnics of the CSS you would say the last one (`.red`). But no, style with a `id` gets the priority.

## CSS Selectors

The <b>selector</b> selects a specific elements from the HTML document.

The <b>declaration</b> block allows you to add properties to selector selected elements.

### Types of selectors

Universal Selector: The universal selector works like a wildcard character, selecting all elements on a page. In the given example, the provided styles will get applied to all the elements on the page.

```css
* {
  color: 'green';
  font-size: 20px;
  line-height: 25px;
}
```

Element Type Selector: This selector matches one or more HTML elements of the same name. In the given example, the provided styles will get applied to all the ul elements on the page.

```css
ul {
  line-style: none;
  border: solid 1px #ccc;
}
```

ID Selector: This selector matches any HTML element that has an ID attribute with the same value as that of the selector. In the given example, the provided styles will get applied to all the elements having ID as a container on the page.

```css
#container {
  width: 960px;
  margin: 0 auto;
}
```

Class Selector: The class selector also matches all elements on the page that have their class attribute set to the same value as the class. In the given example, the provided styles will get applied to all the elements having ID as the box on the page.

```css
.box {
  padding: 10px;
  margin: 10px;
  width: 240px;
}
```

Descendant Combinator: The descendant selector or, more accurately, the descendant combinator lets you combine two or more selectors so you can be more specific in your selection method.

```css
#container .box {
  float: left;
  padding-bottom: 15px;
}
```

Child Combinator: A selector that uses the child combinator is similar to a selector that uses a descendant combinator, except it only targets immediate child elements.

```css
#container > .box {
  float: left;
  padding-bottom: 15px;
}
```

General Sibling Combinator: A selector that uses a general sibling combinator to match elements based on sibling relationships. The selected elements are beside each other in the HTML.

```css
h2 ~ p {
  margin-bottom: 20px;
}
```

Adjacent Sibling Combinator: A selector that uses the adjacent sibling combinator uses the plus symbol (+), and is almost the same as the general sibling selector. The difference is that the targeted element must be an immediate sibling, not just a general sibling.

```css
p + p {
  text-indent: 1sem;
  margin-bottom: 0;
}
```

By attributes: since CSS is supports the selection of HTML elements, it makes sense to also select
HTML elements based on their attributes.

```css
a[target] {
  // This will select all of the a elements that have the target attribute
}
a[target="https://test.ts"]
{
  // This will select all the as that point to our site
}
```

## Box model

A rectangle box is wrapped around every HTML element. The box model is used to determine the height and width of the rectangular box. The CSS Box consists of Width and height (or in the absence of that, default values and the content inside), padding, borders, margin.

- Content: Actual Content of the box where the text or image is placed.
- Padding: Area surrounding the content (Space between the border and content).
- Border: Area surrounding the padding.
- Margin: Area surrounding the border.

Total element width = width + left padding + right padding + left border + right border + left margin + right margin

## Block, inline-block, inline

Block Element: The block elements always start on a new line. They will also take space for an entire row or width. List of block elements are `<div>`, `<p>`.

Inline Elements: Inline elements don't start on a new line, they appear on the same line as the content and tags beside them. Some examples of inline elements are `<a>`, `<span>` , `<strong>`, and `<img>` tags.

Inline Block Elements: Inline-block elements are similar to inline elements, except they can have padding and margins and set height and width values.

## CSS preprocessors

A CSS Preprocessor is a tool used to extend the basic functionality of default vanilla CSS through its own scripting language. It helps us to use complex logical syntax like – variables, functions, mixins, code nesting, and inheritance to name a few, supercharging your vanilla CSS.

SASS: Sass is the acronym for “Syntactically Awesome Style Sheets”. SASS can be written in two different syntaxes using SASS or SCSS

### SASS vs SCSS

- SASS is based on indentation and SCSS(Sassy CSS) is not.
- SASS uses .sass extension while SCSS uses .scss extension.
- SASS doesn’t use curly brackets or semicolons. SCSS uses it, just like the CSS.

## Reset vs Normalize

<b>Reset CSS</b>: CSS resets aim to remove all built-in browser styling. For example margins, paddings, font-sizes of all elements are reset to be the same.

<b>Normalize CSS</b>: Normalize CSS aims to make built-in browser styling consistent across browsers. It also corrects bugs for common browser dependencies.

## Difference between pseudo-elements and pseudo-classes

<b>Pseudo-elements</b> allows us to create items that do not normally exist in the document tree, for example ::after.

- ::before
- ::after
- ::first-letter
- ::first-line
- ::selection

```css
p::first-line {
  color: #ffOOOO;
  font-variant: small-caps;
}
```

<b>Pseudo-classes</b> select regular elements but under certain conditions like when the user is hovering over the link. They don't have content option.

- :link
- :visited
- :hover
- :active
- :focus

```css
a:hover {
  color: red;
}
```

## Adaptive vs Responsive

A pretty sharp interview question is <b>“What is the difference between adaptive websites and responsive websites?”</b>

It’s easy:

- Adaptive website change their appearance at precise points of resolution
- Responsive websites shrink and grow like an elastic depending on resolutions.

## BEM

According to creator definition of BEM is as follows:

"BEM is a highly useful, powerful, and simple naming convention that makes your front-end code easier to read and understand, easier to work with, easier to scale, more robust and explicit, and a lot more strict."

<b>BEM structure</b>

```scss
.block {
  //usually a wrapper that containes component
  position: relative;
  width: 100%;

  &--element {
    //this is how we define element inside of a block
    opacity: 0;

    &-modifier {
      opacity: 1;
      //modifier, such as "open", "disabled" ect
    }
  }
}
```

<b>Example of BEM usage</b>

```scss
.select {
  position: relative;
  width: 100%;

  &--header {
    position: relative;
    cursor: pointer;

    svg {
      fill: red;
      transform: rotateX(0deg);
      transition: all 0.4s ease;
    }

    &-open {
      svg {
        transform: rotateX(180deg);
        fill: blue;
      }
    }
  }
}
```
