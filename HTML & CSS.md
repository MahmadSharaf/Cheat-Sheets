# 1MAC Fullstack

- [1MAC Fullstack](#1mac-fullstack)
  - [HTML Notes](#html-notes)
    - [HTML Head Elements](#html-head-elements)
    - [HTML Body Elements](#html-body-elements)
  - [Rules](#rules)
  - [CSS Notes](#css-notes)
    - [Notes](#notes)
    - [Style properties](#style-properties)
  - [Tips and notes](#tips-and-notes)
  - [Resources](#resources)
    - [Validators](#validators)

## HTML Notes

HTML stands for Hypertext Markup language

Hypertext: links to other webpages.  
Markup: is to give more functionality by using tags.  
Language:

**HTML file consists of two parts, Head and Body. The Head part contains the title, metadata while the Body everything else.**
![Full HTML Tree](HTML/full-html-tree.png)

### HTML Head Elements

1. Title:  
   The document’s title (the text that shows up in browser tabs): `<title>About Me</title>`.
2. Stylesheet file:  
   Associated CSS files (for style): `<link rel="stylesheet" type="text/css" href="style.css">`.
3. JavaScript file:  
   Associated JavaScript files (multipurpose scripts to change rendering and behavior): `<script src="animations.js"></script>`.
4. Charset:  
   The charset being used (the text's encoding): `<meta charset="utf-8">`.
5. keywords, authors, and descriptions (often useful for SEO): `<meta name="description" content="This is what my website is all about!">`.

### HTML Body Elements

1. `<em></em>`: The em element represents stress _emphasis_ of its contents.
2. `<Strong></strong>`: The **strong** element represents strong **importance**, seriousness, or urgency for its contents.
3. `<br>`: The br element represents a line break.
4. `<mark><\mark>`: highlights <mark>text</mark>
5. `<sub></sub>`: The sub element represents a <sub>subscript</sub>.
6. `<sup></sup>`: The sup element represents a <sup>superscript</sup>.
7. Ordered list

   ```html
   <ol>
     <li>list item</li>
   </ol>
   ```

8. Unordered list

   ```html
   <ul>
     <li>1. list item 1</li>
     <li>2. list item 2</li>
   </ul>
   ```

9. Nested Lists

   ```html
   <ul>
     <li>
       * list item
       <ol>
         <li>1. list item</li>
       </ol>
     </li>
   </ul>
   ```

10. Anchor (Links)  
    `<a href="https://github.com/">GitHub</a>`
    [Github](https://github.com/)
11. Image with URL  
    `<img src="<https://placekitten.com/200/150>" alt="Kitten">`
    ![Kitten](https://placekitten.com/200/150)
12. Image on Disk  
    `<img src="Bear.jpg" alt="Bear">`  
    ![Bear](HTML/Bear.jpg)
13. Image with link  
    `<a href="https://google.com"><img src="glogo.png" alt="Google!"</a>`  
    [![Glogo.png](https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png)](https://google.com)
14. Document language  
    `<html lang="en">`: determines the document lang which is helpful for screen reader.
15. Forms  
    The `<form>` tag will be the parent element that contains all of the code for the form. The form fields, the buttons, etc. need to be enclosed inside these tags.

    ```html
    <form action="" method=""></form>
    ```

    the `action` and `method` attributes tell the form where and how to send the form data, respectively. You will not need them in this course, so we will leave them blank for now

    1. Input field:  
       The `<input>` tag lets you add form fields for the user to enter their information. Each input tag will have an attribute called type to indicate what type of form field to put in the form:

       ```html
       <input type="text" />
       ```

       - [Input types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

    2. Labels:  
       For accessibility reasons, it's important to associate each input element with a label. One way to do this is to use the `<label>` tag. Screen readers and other programs designed for accessibility will help bring focus to an input field and its description when labels are appropriately linked to their input fields using the for and id attributes.

       ```html
       <label for="name">What is your name?</label>
       <input type="text" id="name" />
       <!-- for= and id= are both "name" -->

       <label for="age">How old are you?</label>
       <input type="number" id="age" />
       <!-- for= and id= are both "age" -->
       ```

    3. Buttons:  
       HTML5 has the `<button></button>` element. Buttons also have a type so you can specify whether the button submits data or resets (clears) it. Buttons also have the added benefit of being able to display anything in the button by just adding content inside the button tags.

    - [Button Types](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)

      ```html
      <button>I am just a button.</button>

      <button type="submit">I am a submit button!</button>

      <button type="reset">I am a reset button!</button>

      <button type="button">
        I am a button with an image! <br />
        <img src="rocketship.png" alt="udacity-rocket" />
      </button>
      ```

## Rules

1. **Nesting**: Elements can't overlap each other, they must be one inside the other.
2. Some elements have optional closing tag.
   - `<li&>`
   - `<p>`  
     The browser will presume to start a new item list when it finds a starting item list tag
3. Some elements are auto-closing tag.
   - `<img>`
   - `<br>`
4. **Indentation** can help you see which elements are nested inside other elements.
5. `<!DOCTYPE html>` has to be placed on the very top of the html file, to tell the browser to treat this file as the latest HTML5.

## CSS Notes

CSS stands for Cascading Style Sheet

**Cascading**: refers to the way that style properties "cascade" down the DOM tree, starting at the top. A style applied to the body element will affect the entire document. A style applied to a lower-level element will affect that element and all its descendants.

### Notes

1. **DOM**: "Document Object Model" it has a tree structure of each HTML element and for each piece of text, and image, and other object inside the webpage. Tree rules.
   1. A tree has a root node.
   2. Each node can have branches that lead to other nodes (its children).
   3. Each node has exactly one parent (except the root).
2. **Styling**: there are three ways to apply style to HTML elements.

   1. **Inline styles**: The first way is to use the style attribute to apply style directly to an HTML element.

      ```html
      <p style="color: blue;">I'm blue</p>
      ```

   2. **Style element**: The second way is to use the style element along with a ruleset.

      ```html
      <style>
        p {
          color: blue;
        }
      </style>
      <p>I'm blue!</p>
      ```

   3. **Linking stylesheets**: To link to a stylesheet in your HTML file, add a link element to the head of the HTML file. The syntax for the link element is just like this:

      ```html
      <head>
        <link rel="stylesheet" href="style.css" />
      </head>
      ```

3. Adding the semicolon ; at the end is optional, removing it does not seem to cause a problem. This is true if you only have one style applied to the element. If you want to add more styles, the semicolon must be used to separate them. For example:

   ```html
   <p style="text-align:center; color:blue;">This will be centered and blue.</p>
   ```

4. **CSS syntax:** made of two parts
   1. **Selector**: Which element will the ruleset apply to?
      - There are different types of selectors:
        1. **Type**: It is the name of one type of HTML element such as `p` or `div`.
        2. **Class**: It is used when there could be several elements that need same styling. It starts with a dot such as `.class_name`.
        3. **ID**: It is used when there is only one element to apply it to. It starts with # such as `#ID-name`
        4. **Descendant**: It is one of many ways to combine selectors. For example `li em {color: red;}`, this will select every `em` element that is child of `li` element.
   2. **Declaration Block**: How will these ruleset modify these elements?
   3. An element could have multiple classes by adding beside each other separated by space; such as `<li class="highlight done">Make waffles`
5. **Units**:
   1. Real world (absolute) measures:
      1. px: 1 inch = 96 pixels, 1 centimeter = 37.8 pixels
      2. pt: 1 inch = 72 points, 1 centimeter = 28.35 points
   2. Relative to others:
      1. 1 em: equals to the font size in the element.
      2. Percentages: relative to the box/container its inside. Also, it can be used for scaling.

### Style properties

1. **color**: it changes the font color.

   ```html
   <style>
     .blue {
       color: blue;
     }
     .orange {
       color: rgb(100%, 50%, 0%);
     }
     .green {
       color: #008000;
     }
     .purple {
       color: rgb(128, 0, 128);
     }
   </style>
   ```

2. **text-align**: Changes the text alignment.

   ```html
   <p style="text-align: left;">left Aligned</p>
   <p style="text-align: center;">center Aligned</p>
   <p style="text-align: right;">right Aligned</p>
   ```

3. **text-decoration**: Changes font emphasis

   ```html
   <style>
     .done {
       text-decoration: line-through;
     }
   </style>
   ```

4. **font-size**

   ```html
   <style>
     li {
       font-size: 1.5em;
     }
   </style>
   ```

5. **font-weight**

   ```html
   <style>
     li {
       font-weight: bold;
     }
   </style>
   ```

6. **float**: one of many ways to change the position

   ```html
   <style>
     li {
       float: right;
     }
   </style>
   ```

7. **border**
8. **padding**
9. **margin**
10. **width**
11. **height**

    ```html
    <style>
      div {
        border: 10px solid blue;
        padding: 0.5em;
        margin: 5px;
        width: 150px;
        height: 100px;
      }
    </style>
    ```

12. **Fonts**:

    - There are font families that is the font type
    - There are generic font families, this tells the browser "get me this general kind of font". They are five:
      1. serif
      2. sans-serif
      3. cursive
      4. fantasy
      5. monospace
    - If the page is viewed on a computer that doesn't have that specific font, the page will look different. So, either a font-stack like `font-family: Constantia, Georgia, serif` or online fonts like Google Web Fonts.
    - style fonts using a bunch of separate declarations, like this:

      ```html
      <style>
        div {
          font-weight: bold;
          font-style: italic;
          font-size: 14pt;
          text-decoration: underline;
          text-transform: uppercase;
          font-variant: small-caps;
        }
      </style>
      ```

      Or combine all of this styling info into one declaration, by using the short-hand font property. But the font property have to be in a certain specific order or they won't work.  
       [handy page from the CSS-Tricks website](https://css-tricks.com/almanac/properties/f/font/)

    - There are seven font sub-properties, including:
      1. font-stretch: this property sets the font width, such as condensed or expanded.
         - normal
         - ultra-condensed
         - extra-condensed
         - condensed
         - semi-condensed
         - semi-expanded
         - expanded
         - extra-expanded
         - ultra-expanded
      2. font-style: makes the text appear italicised or oblique.
         - normal
         - italic
         - oblique
         - inherit
      3. font-variant: changes target text to small caps.
         - normal
         - small-caps
         - inherit
      4. font-weight: sets the weight or the thickness of the font.
         - normal
         - bold
         - bolder
         - lighter
         - 100, 200, 300, 400, 500, 600, 700, 800, 900
         - inherit
      5. font-size: sets the height of the font.
         - xx-small
         - x-small
         - small
         - medium
         - large
         - x-large
         - xx-large
         - smaller, larger
         - percentage
         - inherit
      6. line-height: defines the amount of space above and below inline elements.
         - normal
         - number (font-size multiplier)
         - percentage
      7. font-family: defines the font that is applied to the element.
         - sans-serif
         - serif
         - monospace
         - cursive
         - fantasy
         - caption
         - icon
         - menu
         - message-box
         - small-caption
         - status-bar
         - "string"

13. **Flexbox**: was designed as a one-dimensional layout model, and as a method that could offer space distribution between items in an interface and powerful alignment capabilities.

    **The two axes of flexbox:**
    When working with flexbox you need to think in terms of two axes — the main axis and the cross axis. The main axis is defined by the `flex-direction` property, and the cross axis runs perpendicular to it. Everything we do with flexbox refers back to these axes, so it is worth understanding how they work from the outset.  
    **The main axis is defined by flex-direction, which has four possible values:**

    - row
    - row-reverse
    - column
    - column-reverse

14. **Positioning**:

    1. inline-block: `display: inline-block` elements can be sized like block elements but are laid out like inline elements.

       ```html
       <style>
         .inline-block {
           display: inline-block;
         }
         .random {
           border: 2px solid #2e3d49;
           background-color: #ecc81a;
           width: 20em;
           height: 40px;
         }
       </style>
       <body>
         <div class="container 1">
           <span>...</span>
           <span class="random inline-block">This is a random span.</span>
           <span>...</span>
         </div>
         <div class="container 2">
           <span>...</span>
           <div class="random inline-block">This is a random div.</div>
           <div class="random inline-block">This is a second random div.</div>
           <span>...</span>
         </div>
       </body>
       ```

       ![Inline-Block Example](<Images/Inline-Block Example.jpg>)
       ![Inline-Block Example 2](<Images/Inline-Block Example 2.jpg>)

       Regardless of the tag, any element with `display: inline-block` takes on the layout behaviors of an inline element with the sizing behaviors of a block element.

    2. Anonymous Boxes:
       - **Whitespace**, the **newline** and the **tab**, between the elements is turned into an anonymous box.
       - Anonymous boxes arise in situations where there is a mix of block and inline elements inside a container.
       - The good news is that you won’t need to think about anonymous boxes for 99.9% of the HTML you write, but it’s worth knowing about them when something weird like this happens.
       - Check out the [official spec](https://www.w3.org/TR/CSS2/visuren.html#anonymous-block-level) on anonymous boxes and [this great explanation](http://book.mixu.net/css/1-positioning.html#anonymous-box-generation) for more information.
    3. Relative Flow:

       - The relative flow allows you to shift the position of elements after they've been laid out in the normal flow.

       ```css
       .shift {
         position: relative;
         top: 10px;
         left: 10px;
       }
       ```

       ![Relative flow example](<Images/Relative flow example.jpg>)

    4. Fixed Flow
       - `position: fixed` elements are in the simplest flow. For them, `top`, `bottom`, `left` and `right` indicate a position within the [viewport](#tips-and-notes). As the user scrolls the page, fixed elements never move. The most common use cases include headers and side navigation menus.
    5. Absolute Flow
       - `position: absolute`, the element is positioned relative to its parent before the rest of the normal flow occurs. Its siblings in the normal flow ignore it and are laid out as if it were not there.
       - _When Would You Actually Use position: absolute?_  
         Frankly, `position: absolute` is best thought of as a last resort. If all the other flows fail, then maybe absolute is your best option. Off the top of my head, I can't actually think of an instance where I wanted to use `position: absolute`. There are, in fact, other CSS techniques for achieving the same kind of shift, of which my favorite is `transform: translate`. ([Transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform) is a more advanced CSS property and it's incredibly powerful. I recommend checking it out).  
         It's good to know what `position: absolute` does, but it's rarely your best positioning option.
    6. Inline Formatting
       ![Inline formatting](<Images/Inline formatting.png>)
       - There are two properties that you can use to align text: `text-align` for horizontal alignment and `vertical-align` for vertical alignment.
       - _Horizontal Alignment_  
         Horizontal alignment starts with another property, `direction`, which has two options: `ltr` and `rtl`. `ltr` is the default value and it stands for "left to right". `rtl` stands for "right to left". You'll need to set direction: `rtl` when working with text in languages like Hebrew (עִברִית) and Arabic (العربية), which are read from `right` to left.  
         `text-align` takes on the default value of `start`. In the case of `ltr`, `start` is the same as `left`. With `rtl`, `start` is equivalent to `right`. This is normal text alignment, where the text pushes against the `start` of the container. `justify` is another option. Newspapers (in real life) tend to use `justify` to keep the `left` and `right` edges of text nicely aligned with the edges of the column, but it's not used as much online. Besides that, `left`, `right`, and center do exactly what you think they do - align text to the `left`, `right` or `center` of the line box.
       - _Vertical Alignment_  
         By default, text sits on the baseline inside its container. More specifically, the baseline of the text will match the baseline of the parent.

15. **Floats**:

    - They are not a positioning value. They are a wholly different flow on the page created by a new property, `float`. Floats are commonly used to create grid-based layouts.
    - Developers realized that something interesting happens with multiple floats on the page. While floats ignore block elements, they respect the boundaries of other float elements.
    - Float example

      ```html
      <style>
      .left {
        float: left;
      }
      .right {
        float: right;
      }
      .green {
        background-color: #89D698;
      }
      .blue {
        background-color: #89D0E5;
      }
      </style>
      </head>
      <body>
        <div class="left 1 green">.left.1</div>
        <div class="right 2 blue">.right.2</div>
        <div class="left 3 green">.left.3</div>
        <div class="right 4 blue">.right.4</div>
      </body>
      ```

      Notice how the floats stack on one another in the order that they appear in HTML. This animation gives you an idea of how the elements end up where they do.
      ![Lefts stack on the left, rights stack on the right.](<Images/Floating example.png>)

    - Regardless of `float: left` or `float: right`, all floats respect each other's space. Widening the floats in the (bump up the `width` of `div`) and floats will push against each other, they wrap to the next line.
    - Float flow and normal flow

      - Floated elements stay within their containers width, but not their height.
      - Float children are not involved in the box-size calculation of normal flow parents.
      - If a container only contains a float child, the container will not have a height by default - the height has to be set some other way, such as with normal flow content or the `height` property. There are a few ways to work around it and force elements in the normal flow to respect the boundaries of floats.

      1. **Block Formatting Contexts**:
         - This strategy forces normal flow siblings to respect the boundaries of floats.
         - This rule originally protected elements like `<table>`, which create their own block formatting context, from being invaded by floats. The reasoning behind this is that you wouldn't want a random image to push aside all the text inside a carefully built table.
         - The `overflow` property, set a block formatting context (any value other than visible, including auto, forces an element to take on a block formatting context).
      2. **Clearing**:
         - By default, line boxes clear out space for float elements. "Clear," in this case, means that they move out of the way for floats. You can control how siblings interact with floats with `clear`.
         - `clear: left` indicates that the top of the element must be below any left floated elements that appear before this one in the document.
         - `clear: right` acts the same, but with right floated elements.
         - `clear: none` means that there are no restrictions; this is the default value.
         - `clear: both` is interesting - it indicates that the element must be below any floated elements that appear earlier in the document.
      3. **Clearfix**:

         1. Pseudo-elements is an element that is actually created with CSS and then rendered like a normal element. The pseudo-element is created with `:after` inside the CSS on the element that I want to mutate. Another option would be `:before`. In effect, the `pseudo-element` is extra content that is added to the element. Without the `content` property, the `pseudo-element` disappears. It can be styled with whatever CSS properties you'd like.
         2. The third technique to clear floats,

         - clearfix, combines aspects of the first two. The goal of the clearfix is to make a normal flow parent resize its box model to fit all of the floats inside it. There are two general techniques to do so.
           1. Add an element with `clear: both` to the end of a parent. This ensures that the last element is a normal flow element that has been pushed below all the floats.
           2. Turn the parent into a block formatting context with an `overflow` property other than `visible`. The block formatting context respects the boundaries of floats and ensures the parent's box model encompasses float children.
         - The first technique by itself, adding an HTML element with `clear: both`, violates the commandment of code clarity; HTML should be restricted to rendered content. However, applying the same technique with a pseudo-element works nicely.

           ```css
           .clearfix:after {
             content: "";
             clear: both;
             display: table;
           }
           ```

         - This clearfix actually uses both technqiues - the pseudo-element has a block formatting context, forcing it to stay outside the bounds of the floats, and it clears both left and right floats.

           ```css
           .clearfix {
             overflow: auto;
           }
           ```

         - If you were to decide which technique is better just based on the complexity of the two CSS classes, `overflow: auto` would win. It's much simpler. However, `overflow: auto` has a side effect.Shrinking the height of the parent.

      4. Overflow:

      - There are technically three different overflow properties: `overflow`, `overflow-x` and `overflow-y`. These three properties determine what happens to content if its box model is larger than its parent's box model.
      - The default option is `visible`, which means that the content is always rendered and may extend outside of its parent. Other options include `hidden`, `scroll` and `auto`. `hidden` does exactly what you think - it clips off any content that extends outside the parent's box model. `scroll` adds scroll bars to the parent, allowing the user to scroll around the parent element to access all the content. The behavior of `auto` depends on the browser.

## Tips and notes

1. Border Box:  
   [Border-Box](https://css-tricks.com/international-box-sizing-awareness-day/)
2. Semantic Elements:  
   Semantic elements can really help improve your website's search engine optimization. If you want to learn more about SEO, I recommend checking out [Moz's Beginners Guide to SEO](https://moz.com/beginners-guide-to-seo).
3. Types of Elements:  
   You have many different kinds of elements at your disposal. Almost all of them are either block or inline with the major differences being their default CSS styles. Check it out, [here’s a list](https://developer.mozilla.org/en-US/docs/Web/HTML/Element).
   - The elements for [content sectioning](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Content_sectioning) are good for laying out things on the page. Notice that a lot of these have requirements for what should be inside the element, for example, an `<article>` typically includes a heading as a child element.
   - [Text content](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Text_content) is good for text. There are a few from here that you’ve seen before, but there are some new ones as well.
   - There are also [inline text semantics](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Inline_text_semantics). You’ll see familiar elements like `<em>` and `<span>`, but you’ve got others like `<code>`, which displays code in a monospace font. Also `<data>`, `<progress>`, `<time>`, and others.
4. Elements Layering/Stacking or 3rd dimension (z-axis):
   - x and y run along the computer screen's surface, z is the dimension that extends in to and out of the screen. By adding a third dimension, you can think of elements as appearing on different layers.
   - In CSS you can often use the `z-index` property to control the stacking order of overlapping elements on different layers.
   - Elements on layers that are higher in the z-axis appear on top of elements beneath them. I'm going to add a user to the last diagram to show you why.  
     ![Stacking 0](Images/stacking1.jpg)
     ![Stacking 1](<Images/stacking 2.jpg>)
     ![Stacking 2](Images/stacking.jpg)
5. Document, DOM and Viewport:
   1. The "document" is another name for the entire DOM.  
      The document is a reference to the DOM - the big tree you’ve been building with HTML elements. The document is the entire page, from top to bottom, header to footer, as far as you can scroll.
   2. The "window" is the visible portion of the DOM.
      The viewport is the portion of the DOM that is currently visible inside the browser window. The viewport’s size depends on the browser dimensions, and as such will change depending on factors like screen resolution, window size, device orientation (landscape vs. portrait views on phones and tablets) and device pixel ratio.

## Resources

- [CSS-Tricks](https://css-tricks.com)
- [MDN web docs](https://developer.mozilla.org/en-US/)

### Validators

- [W3C HTML Validator](https://validator.w3.org/)
