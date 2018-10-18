---
title: TD3 &ndash; HTML / CSS advanced 2/2
subtitle: display and layout
layout: tutorial
lang: en
---


## Priority of CSS selectors

As you recall, selectors are used to select a set of tags on which we apply a
CSS rule. We learned in
[tutorial 1 the basic selectors](tutorial1_2-en.html#the-basics-of-css-selectors)
and in
[tutorial 2 the CSS composition rules](tutorial2-en.html#css-composition-rules).

Several CSS rules may apply to a single HTML element. If these rules
can coexist, they are all applied. For example, if you have the
following CSS code:

```css
div    { background-color:blue; }
.skill { color:red; }
```

then a `<div class="skill">` will have both properties `background-color:blue`
and `color:red`.

But it can also happen that rules are contradictory. By example, if you have the
following CSS code, **what color** will the text of a `<div class="skill">` be ?

```css
.skill { color:red; }
div    { color:blue; }
```

To resolve these conflicts, the CSS defines a notion of priority based on
the location of the CSS rules and the specificity of CSS selectors. In
the previous example, this is the first rule that prevails as we shall see
in the following.

###  Various locations

There are several possible locations for declaring CSS:

1. **External Style** : (Recommended) You can use an external style file and
   link it to HTML document with the `<link>` tag inside the `<head>`:

   ```html
   <html>
     <head>
       <link rel="stylesheet" type="text/css" href="css/styles.css">
     </head>
     <body> ... </body>
   </html>
   ```

1. **Internal Style** : (Not recommended) You can include directly the CSS rules
   into the `<head>` using the `<style>` tag:

   ```html
   <html>
     <head>
       <style type="text/css">
         p {font-size: 12pt; color: pink}
       </style>
     </head>
     <body> ... </body>
   </html>
   ```

1. **Style inline** : (Strongly discouraged) You can include CSS rules directly
   into any tag using its `style` attribute:
 
   ```html
   <p style="font-size: 12pt; color: fuchsia">
      Aren't style sheets wonderful?
   </p>
   ```

   Be careful not to get confused between the inline style with the future
   `display: inline`.

Finally browsers apply a default style on the elements, so you don't have to set
the most classic styles everytime. One can observe the default style in
development tools of Chrome: it is the style rules associated with *user agent
stylesheet*.

Take good habits and use external stylesheets such as `styles.css` which allows
a clearer separation between the roles of HTML (content with tags to add sense)
and CSS (presentation / page layout).  As told at
[the end of part 1 of tutorial 2]({{site.baseurl}}/tutorials/tutorial1_2-en.html#css-and-html-very-distinct-and-complementary-roles)
this separation is essential and powerful:

 * It allows you to reuse a presentation from one page to another. For instance
   when *lemonde.fr* publishes a new article, it does not remake the style for
   it: it is a new HTML document sharing the same CSS as previous articles;
 * It allows you to change the layout of your website by focusing on CSS without
   touching the HTML (too much);
 * It allows you to change the presentation of a document depending on whether
   it is intended to be printed or to be viewed inside a browser.


### Priority of selectors

Using the previous example:

```css
.skill { color:red; }
div    { color:blue; }
```

To determine the color that will be applied to the `<div class="skill">`
elements, priorities are set to CSS selectors. To get an idea, since `.skill`
class selector is more specific than `div` tag selector, `color:red;` will have
a higher priority and we be applied.

The *priority of a CSS selector* is a value *(a, b, c, d)* defined as follows:

* the value *a* encodes the priority based on the location of the rule. By
  decreasing priorities, we have
   * *a*=2 for inline styles,
   * *a*=1 for external and internal styles,
   * *a*=0 for default browser style.
 * *b* counts the number of identifier selectors (e.g. `#id`),
 * *c* counts the number of class selectors (e.g. `.skill`) or pseudo-class
   selectors (`:hover`, `:visited`,...)
 * *d* counts the number of tag selectors (e.g. `div`, `span`) or pseudo-element
   selectors (e.g. `::first-letter`, `::after`)
 * combinators and the universal selector `*` have no impact on the priority.

Returning to the previous example, we get these priorities for our rules
(assuming they are written in an external style file) :

```css
 div    /* -> (1,0,0,1) (one div tag selector)   */
 .skill /* -> (1,0,1,0) (one skill class selector) */
```

###  The order of priority

It remains to explain how priorities (*a*,*b*,*c*,*d*) are sorted. The order of
priority is the order of dictionary (*lexicographical ordering*):

* First we look at the "first letter" *a*. If *a* is strictly greater
then the CSS rule has a higher priority. In case of equality,
* we look at the "second letter" *b*: If *b* is strictly greater (and therefore
  *a* is equal) then the CSS rule has a higher priority. In case of equality of
  both *a* and *b*
* we look at the "third letter" *c*. In case of equality,
* we look at the "fourth letter" *d*.
* **In case of equalities everywhere**, the last written rule has priority.

**Example :** the selector `div.skill` (priority (1,0,1,1)) has higher priority
than the selector `div` (priority (1,0,0,1)) because we have equality on *a* and
*b* but *c* is greater for `div.skill`.

This priority mechanism is called the cascade and corresponds to the C of CSS
(Cascading Style Sheet).

<div class="exercise-en">

In a text file or on paper, write the priorities of the following selectors
and sort them from the highest priority to lowest priority. Assume
that all these rules are defined in an external file, so *a*=1.

```css
 .titi span
 div span
 nav.titi .tata div div div div div
 ul li div.skill
 #id
 div > a
 div + a
```

</div>

<!--
#id                                   (1,1,0,0)
nav.titi .tata div div div div div    (1,0,2,6)
ul li div.skill                       (1,0,1,3)
.titi span                            (1,0,1,1)
div span                              (1,0,0,2)
div > a                               (1,0,0,2)
div + a                               (1,0,0,2)
-->

<div class="exercise-en">

What is the color of the text "CSS priority" in following two cases? Say which
rule on CSS priorities explain your answer.

1. The file `styles.css` contains the rule `p {color:blue;}`, and the file
   `index.html` contains

   ```html
   <html>
     <head>
       <style type="text/css">
         p {color: pink}
       </style> 
       <link rel="stylesheet" type="text/css" href="css/styles.css">
     </head>
     <body><p style="color:red">CSS priority</p></body>
   </html>
   ```

1. Given the same file `styles.css` and the new file `index.html` without the
   inline style

   ```html
   <html>
     <head>
       <style type="text/css">
         p {color: pink}
       </style> 
       <link rel="stylesheet" type="text/css" href="css/styles.css">
     </head>
     <body><p>CSS priority</p></body>
   </html>
   ```

</div>


## The `display` property

As we have seen in the previous tutorial, each tag is associated with four boxes
(*content*, *padding*, *border* and *margin*,
[see the section about the box model in tutorial 2]({{site.baseurl}}/tutorials/tutorial2-en.html#the-box-model)).

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodel.png" style="margin:0
auto;display: block;">

How these boxes will occupy the space is managed by the attribute `display`. We
will see in this section the three main values of the `display` property.

### `display:block`

The block elements are elements:

 * that occupy the entire width by default,
 * that cause a line break before and after,
 * whose sizes can be set via the CSS properties `height` and `width`.

In practice, `display:block` elements are used:

 * when one wants to specify the layout of certain HTML elements. For example we
   want the header to have height `200px`, or a paragraph to take `50%` of the
   width ....
 * as soon as it is natural to take all the width (such as a title `<h2>`).


Note that
[structure tags that were introduced in the previous tutorial]({{site.baseurl}}/tutorials/tutorial2-en.html#structuring-a-web-page)
all have the default style `display:block` in the browser, which explains that
they stack vertically as explained before.

### `display:inline`

The inline elements are elements:

 * whose sizes are solely based on their content; the size can not be set using
   the properties `height` and `width`,
 * that do not cause a line break; they are written one after another the same
   way that text is written.

In practice, `display:inline` elements are used:

 * in the text, to add meaning to some part of the text without interrupting the
   normal flow of text (write an exponent with `<sup>`, specify the importance
   of a portion of text with `<strong>`...)
 * when one wants to position elements one after another.

Since they only contain text most of the time, inline elements such as
`<strong>`, `<a>`, ... are generally leaves of the HTML tree.

Note that
[text-level tags that were presented in the previous tutorial]({{site.baseurl}}/tutorials/tutorial2.html#top-menu)
all have the default style `display:inline` in the browser, which explains that
they behave as text.

### Example

The following HTML code

```html
<p style="display:block;">display:block</p> 
<p style="display:inline;">display:inline</p> 
...
<p style="display:inline;">display:inline</p> 
<p style="display:block;">display:block</p>
<p style="display:block;">display:block</p> 
<p style="display:inline;">display:inline</p> 
```

is displayed like this:

<div class="codeexample" style="padding:0;text-align:initial;"> 
<p style="display:block;background-color:#A4AFFC;border: 1px solid black;margin:0;">
display:block
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
<p style="display:block;background-color:#A4AFFC;border: 1px solid black;margin:0;">
display:block
</p>
<p style="display:block;background-color:#A4AFFC;border: 1px solid black;margin:0;">
display:block
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline
</p> 
</div>

Note that the `display:block` take the whole width, and have a line break before
and after them. The `display:inline` elements appear one after the other as the
text of a paragraph.

### Exercises

We will successively layout the navigation menu of our website with
`display:block` then `display:inline`.

<div class="exercise-en">

In this first exercise we will create a menu with the `display:block` style.

1. Change the navigation menu of your Chuck Norris website to the following one

   ```html
   <nav>
   	<div><a href="./index.html">Accueil</a></div>
   	<div><a href="./facts.html">Facts</a></div>
   	<div><a href="./news.html">Actualités</a></div>
   	<div><a href="./contact.html">Contact</a></div>
   </nav>
   ```

1. Since `<nav>` is `display:block` by default (check it with the dev tools in
   Chrome), it must take the whole width. **Inspect** your `<nav>` to see if it
   is the case. What do you notice?

   **Explanation:** In fact, a `display:block` element do not take the whole
   width of `<body>` but the whole width of its closest `block` parent. Here,
   the parent of `<nav>` is the `block` `<header>` and so `<nav>` takes the width
   of `<header>`.  
   The closest `block` parent is called the *containing block*.

1. Since `<nav>` is `block`, we can fix its dimensions. Fix its width to
   `75%`. What do you notice?

   **Explanation :** The width of a `block` element is relative to its
   containing block (`<header>` here).

1. **Inspect** `<header>` then `<nav>` to know their width. **Verify** that they
   have a ratio of `75%` as expected.

1. Center `<nav>` with respect to its parent `<header>`: to do so, set the
   horizontal margins to `auto` (and keep the vertical margins at `0`).

   **Reminder:** We saw
   [in the previous tutorial how to center horizontally]({{site.baseurl}}/tutorials/tutorial2-en.html#center-horizontally).
   To center a `display:block` element whose *containing block* is wider, one
   must set the horizontal margins to `auto`: the margins will adjust
   automatically to fill up the width difference between the element and its
   containing block. This does not work for vertical margins.

1. Add a CSS rule so that all the `<div>` **children of** `<nav>` have a
   background color of `#5BBDBF`,
1. Add a CSS rule so that all the `<a>` **descendant of** `<nav>` have a
   background color of `#c0d5c2`.

</div>


<div class="exercise-en">

Let's now apply `display:inline` to the navigation menu.

1. Apply `display:inline` to the `<div>` children of `<nav>`.
1. You can see spaces between the menu items. These spaces are due to spaces in
   the HTML, which are displayed when we are in `display:inline`.  
   **A temporary solution (until we learn about `display:flex`):** Change the
   HTML to put comments instead of spaces like this:

   ```html
   <nav>
   	<div><a href="./index.html">Accueil</a></div><!--
 --><div><a href="./facts.html">Facts</a></div><!--
 --><div><a href="./news.html">Actualités</a></div><!--
 --><div><a href="./contact.html">Contact</a></div>
   </nav>
   ```

1. Set the height of `<nav>` to `50px` (`<nav>` is a `block` element so you can
   fix its height),
1. (Optional) Add a horizontal padding of `10px` to all `<a>` elements in the
   navigation menu.
1. (Optional) Add to those same `<a>` a left border of `2px` of style `solid`
   and color black.
1. (Optional) Remove the left border of the `<a>` that are first children of
   their parent.  
   **Hint:** You need to use a pseudo-class seen
   [in the last tutorial]({{site.baseurl}}/tutorials/tutorial2-en.html#pseudo-classes).

</div>

## `display:none`

The value `display:none` completely removes an element from the rendering,
without leaving space to where it should have been. We will use this in our
following exercise about a pull-down menu to hide the sub-menus by default.

### Pull-down menu : Part 1 -- positioning

First, let's just position the sub-menus below their menu title. This exercise
puts into practice the `position` property that we saw in the previous TD. Here
is a reminder about `position`.

#### Position

The CSS property `position` offers new opportunities for the positioning of the
elements. Its values are:

* `static`: normal behavior (default), the item is normally inserted.

* `relative`: the rest of the page behaves as if the element was positioned
  normally. But the element is positioned *relatively* to the position where it
  should have been. So you can see an empty space where the element would have
  been in `position:static`.

* `absolute`: the rest of the page acts as if the element does not exist. The
  element is positioned relatively to its closest **positioned** ancestor or
  otherwise to `<body>` (if no ancestor is positioned).
  
* `fixed`: the rest of the page acts as if the element does not exist. The
   element is positioned with respect to the browser window; it therefore seems
   *fixed* while scrolling the Web page.

An element is said **positioned** if it has a position other than `static`
(which is the default value).

To indicate the position offset, use the properties `top`, `left`, `right`
and `bottom`. For example, the properties

```css
position:relative;
top:20px;
left:20px;
```

will position an element `20px` to the bottom right of where it ought to be.

Reference : [Mozilla Developer Network (MDN)](https://developer.mozilla.org/fr/docs/Web/CSS/position)

<div class="exercise-en">

1. Add the following sub-menus for the navigation menu. These sub-menus have the
   same father `<div>` than the `<a>` links (Accueil, Facts, ...), but are
   placed right after these links.

   * Sub-menu for "Accueil" 

     ```html
     <div class="submenu">
       <div><a href="./one.html">one</a></div>
       <div><a href="./two.html">two</a></div>
       <div><a href="./three.html">three</a></div>
     </div>
     ```

   * Sub-menu for "Contact"

     ```html
     <div class="submenu">
       <div><a href="./other.html">other</a></div>
       <div><a href="./another.html">another</a></div>
     </div>
     ```

1. Let us position properly these sub-menus: we wish that the rendering of the
   webpage behaves as if these sub-menus did not exist. Moreover, we wish that
   these sub-menus are positioned below their menu title (the parent `<div>`
   "Accueil" or "Contact"). Let's proceed in several steps:

   1. What is the value of `position` that corresponds to this behavior for the
      sub-menus ?
   2. Create CSS rules that sets this value for the `position` of tags of class
      `submenu`, and indicate that the position should be offset by `50px` from the
      top, and `0px` from the left with respect to the menu title.
   3. The sub-menus are not well placed yet since they position themselves with
      respect to the wrong tag. **With respect to which tag** are the sub-menus
      positioned ?  Re-read the previous explanation about positioned elements
      to check your understanding.
   4. We wish that our sub-menus would be positioned with respect to their
	  `<div>` parent. Therefore, we need to make these `<div>` *positioned*,
	  without affecting the rendering of the rest of the page.  
      **What value of `position`** should we apply to those `<div>` to do this ?
	  Create this CSS rule and the sub-menus should finally be positioned `50px`
	  below their title.

</div>

### Pull-down menu : Part 2 -- display when mouse is over

We will now use `display:none` to display the sub-menus only when the mouse is
over their corresponding title.

<div class="exercise-en">

1. Set the background color of those sub-menus to `#aca`. Then hide them using
   CSS.

1. Reveal the first sub-menu (resp. the second) with `display:block` when the
   mouse flies over its menu title "Accueil" (resp. "Contact") using CSS.  

   **Help:** In practice, we will check if the parent `<div>` is flown over
   (`:hover`). We wish to have a selector that selects elements of class
   `submenu` which are children of a `<div>` flown over which are a children of
   `<nav>`.

</div>

At this point the sub-menus appear only when the mouse flies over "Accueil" or
"Contact". However, it is not possible to click on those sub-menus. We spend the
entire next section on the behavior `display:flex` which will improve the
appearance of our menu and address the problem of accessibility.

## `display:flex`

The value `flex` for the property `display` corresponds to a layout mechanism
called FlexBox. Applied to an element, the value `flex` will help change the
layout **of the children**. It is therefore a fundamental difference with values
`inline` ​​and `block` that had an impact directly **on the item itself**.


When the display is `flex`, we can for example:

 * fix the rendering direction of the children,
 * set the spacing between the children,
 * center them horizontally and vertically,
 * change their appearance orders, ...
 
We detail thereafter some of these constraints / properties. We recommend that
you also look at
[this complete guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
while learning new `flex` properties to help understand them.
 

### The property `flex-direction`

The `flex-direction` property specifies whether the children will place themselves
in a row or column and in which order. Its values ​​are:

 * `row` : children are placed in a row from left to right;
 * `row-reverse` : children are placed in a row from right to left;
 * `column` : children are placed in a column from top to bottom;
 * `column-reverse` : children are placed in a column from bottom to top.

Because the `flex-direction` attribute applies to children, it may conflict with
display values `block` or `inline` of those children. The following exercise
will enable us, among other things, to know what overloads the other in case of
conflict.

<div class="exercise-en" >
 1. Read the section corresponding to `flex-direction` in
    [the complete guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
    to check your understanding.
 1. Set `display:flex` on the `<nav>`.
 1. Change the display value of `<nav>`'s children `<div>` to `block` then
    `inline`. Does it change anything ?
 1. Set `flex-direction:column` on the `<nav>`. What does it change ?
 1. Put back the default value `flex-direction:row`.
 1. Give a fixed width of `100px` to all `<div>` **descendants** of `<nav>` so
    that menus and sub-menus have the same width.

</div>


### The property `align-items`

The `align-items` property is used to specify how the children will occupy the
space **perpendicular** to the direction given by `flex-direction`. In our case
(`flex-direction:row`), `align-items` will therefore allow us to specify how to
occupy the vertical space of the `<div>` elements contained in the `<nav>`.

Its possible values are:

 * `stretch` : stretch to take the entire space (default);
 * `center` : center without stretching;
 * `baseline` : aligns the baselines (line on top of which text is written) of
    the children;
 * `flex-start` : alignment at the beginning of the axis perpendicular to the
    direction of` flex-direction`;
 * `flex-end` : alignment at the end of the perpendicular axis.

Reference:
[Mozilla Developer Network](https://developer.mozilla.org/fr/docs/Web/CSS/align-items)


<div class="exercise-en" >

In this exercise, we want the `<div>` menu titles to be centered vertically
**and** to take the whole height.

1. Read the section corresponding to `align-items` in
   [the complete guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
   to check your understanding.

1. To see the behaviors more clearly, we will set until the end of this exercise
   a height of `200px` and a background color of `#FF00FF` to `<nav>` and change
   the top offset of sub-menus from `50px` to `200px`.

1. Center vertically the children of `<nav>` using `align-items` on `<nav>`.
   What do you notice about the height of the `<div>` and the accessibility of
   the sub-menus ? Is `<div>` vertically centered ?

1. Now use the value `stretch`.  What do you notice about the height of the
   `<div>` and the accessibility of the sub-menus ? Is `<div>` vertically
   centered ?

1. Now let's make the sub-menus accessible and make "Accueil" and "Contact"
   centered vertically. For this matter:
   
   1. Make the `<div>` take the whole height using one of the two previous questions.
   1. Now center vertically the links `<a>` inside their `<div>`: you need to
      set `display:flex` for the `<div>` children of `<nav>`, which will allow
      you to center vertically the links using the other of the two previous
      questions.

1. Cancel (comment) the CSS rules written in question 2.

</div>

### The property `justify-content`

This property allows you to specify how the children will behave with respect to
the direction given by `flex-direction`.

The possible values are:

 * `flex-start`: at the beginning of the axis given by` flex-direction`;
 * `flex-end`: at the end of this axis;
 * `center`: centered on this axis;
 * `space-between`: the elements start from the beginning to the end of the axis
   by adding spaces between the elements;
 * `space-around`: the elements are from the beginning to the end of the axis by
   adding spaces around the elements (so between the elements **and** before the
   first **and** after the last).

<div class="exercise-en" >

 1. Justify the menu titles to the right of `<nav>`, with your favorite display
    `flex`. Put temporary a background color to `<nav>` to check that the menu
    titles moved to the right of `<nav>`.

</div>


### Flexbox, a relatively recent value

If the `flex` possibilities seem trivial or even natural for the neophyte, they
represent a major practical advance in the world of CSS. Before `flex`, some
properties were part of a real expertise of the integrator (e.g. vertical
centering), or were even confined to the realm of fantasy (the justifications,
the behavior of elements on the remaining space, etc.).

Today flexbox is implemented in [many different
browsers](https://www.caniuse.com/#search=flexbox). Therefore we will not
present some other display values that have become unnecessary
(`display:inline-block`, `display:table`) or even alignment techniques based on
`float` which have always been technically crappy.

## Global layout

### Header part

<div class="exercise-en" >
 1. Place the quote and the navigation menu on the same row (the quote will be
    on the left and the menu to the right), using your favorite display value.
 1. Replace the menu to the bottom of the `<header>` tag (yes, still using
    `flex`).
 1. Put a white background color to `<header>`.
 1. Remove the background color of the links in the menu.
</div>


### Two column layout

It's time to have a better layout for our website.

<div class="exercise-en" > 

1. Set the `width` of `<body>` to `900px`.
 1. Set `display:flex` on the `<main>` tag so that its children `<article>` and
    `<aside>` would display as two columns side by side.
 1. Fix the width of `<article>` to `60%`, and the width of `<aside>` to
    `30%`. This last element will have a left margin of `10%`.
 1. Give a background color of `#CCC` to `<aside>` and `<article>`.

</div>

##  Hide or remove an element from the rendering

There are many ways to make an HTML element disappear from the screen:

 * `display:none` 
 * `visibility:hidden`

We have already used the `display:none` to hide a sub-menu without impacting
the rest of the webpage.  The `visibility:hidden` acts differently and leave an
unoccupied space in place of the element.

Let's use `visibility:hidden`:

<div class="exercise-en">

We want to visually mark the menu under the mouse by a small bullet in the `<a>`
of the menu title.

```html
<span class="puce">■</span>
```

It is positioned to the left of the text, it is visible only when the mouse is
over the `<div>` tag. If the mouse is not over, the space of the bullet remains
occupied by an empty space: this way we don't have any flickering on the menu's
title.

1. Add this bullet in the HTML before the links `<a>`,
1. Add `visibility:hidden` to elements of class `puce` and add the value
   `visible` when the mouse flies over the parent `<div>`.
1. (Optional) Improve the style of the sub-menus.

</div>
