---
title: TD2 &ndash; HTML / CSS Advanced 1/2
subtitle: structuring and stylisation, Block &amp; inline, combination of selectors
layout: tutorial
lang: en
---

The HTML5 specification provides several ways to classify tags (or elements)
according to their characteristics
([list of tags per category](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)).
Let's focus on two specific types of tags:

* the tags that give structure: they allow you to define the logical
articulation of the web page by cutting it in different sections.


* The tags at the level of the text: they bring a precision on the semantics of
  a part of the text (highlight an important part of text, write an exponent,
  time,...).

  Here are a few examples of text-level tags :

   * `<sup>`: an exponent
   * `<time>`: a date
   * `<em>`: emphasize text
   * `<strong>`:  add importance to text
   * `<br>`: new line (**br**eak line)

  These text-level tags are often associated to a style (the `<em>` will be
  stylized by italics, the `<sup>` in superscript, ...). The browsers are
  responsible to add for us some default common styles.

There are still many other HTML tags. That said, it happens that no tag
corresponds to what we want to express (during a layout construction for
example). Two neutral tags have been added for these constructions:

   * At the text-level `<span>`: this tag is neutral, with no special
     meaning. It is used to create specific formatting rules for textual content
     (*e.g.* when we add the class `skill`).
   * Structure tag `<div>`: this tag is neutral, it is used to create a
     **div**ision in the code which no special meaning. Unlike `span` it causes
     a line break.


##  Structuring a Web page

First you'll logically structure the content of the site. Here is a *HTML
Template* (modèle HTML en français) of a classic page structure.


```html
<!DOCTYPE html>
<html>
    <head> ... </head>
    <body>
        <header>
            ...
            <nav> ... </nav>
        </header>
        <main>
            <article> ... </article>
            <article> ... </article>
            <aside> ... </aside>
        </main>
        <footer>
            ...
        </footer>
    </body>
</html>
```

To clarify, here is an overview of a corresponding layout for the previous
example:

<img src="{{site.baseurl}}/assets/sections.png" alt="Structuration d'une page" style="margin: 0 auto;display: block;">

By default, the structure tags cut the web page in horizontal sections that they
occupy in full (from the left to the right edge). By default, two structure tags
will pile up vertically because they can not share the same horizontal section
(so we will have to add a special layout to `<aside>`).


Let us explain the role of some structure tags:

   * `<header>`: section containing the header of the page (not to be confused
     with `<head>`, which are the meta-informations about the web page)
   * `<nav>`: section containing a series of hyperlinks for navigation
     on the site
   * `<main>`: main section of the page with the specific content to this page.
   * `<article>`: section containing a document "self-sufficient", *i.e.* which
     can be separated from the rest of the page and yet retains all its
     meaning. A page can contain several articles, in the case of a blog, of
     comments, of a list of recent publications ...
   * `<aside>`: section containing content which could be considered separate
     from the rest of the page. This may be a series of specific links to the
     principal document, an advertising banner ...
   * `<footer>`: section containing the footer.
   * `<section>`: non-specific section or subsection of an article,
     a menu ... Must typically begin with a title `<h*>`.
   * `<figure>`: an "self-sufficient" illustration (at large) illustrating the
     main document or article, and which must be placed freely in the page
     without changing its course (eg. in the text, in an appendix ...)
   * `<h1>` - `<h6>`: section titles
   * `<blockquote>`: a quote with in particular `<cite>` for the reference of
     this citation.
   * `<p>`: paragraphs of text
   * `<address>`: Author's contact information. There can be only one
     `<address>` per `<article>` and one for the rest of the page.

<div class="exercise-en">

Let us improve our previous `index.html` Web page of Chuck Norris.

1. Add a `<header>` tag. Its content will be the citation of the TD1 and a
   navigation bar `<nav>` empty for the time being,

2. Add a tag `<main>`, a tag `<article>` and a tag `<aside>` as in the *HTML
   Template*. Put the old content of the page in `<article>` except the last two
   sections ("Les sites amis” and “Le Top 10 des derniers facts proposés”) which
   will go in `<aside>`,

3. Add a tag `<footer>` which contains the link to go back to the beginning of
   the site,

4. Add in the tag `<nav>` a list (do you remember the list tags ?) of two links:
   a link named "Home" that points to the current page `index.html` and a link
   named "Contact" that points to a future page `contact.html`,

5. Validate your HTML pages on the validator
   [https://html5.validator.nu/](https://html5.validator.nu/). (Do it
   systematically without being asked for it :-) ).

</div>
<div class="exercise-en">

1. Build a page `contact.html` in the same folder than `index.html`. It must
   contain the same *HTML template* as `index.html`. In particular:

   1. it uses the same `<header>` and `<footer>` as `index.html`,
   1. it calls the same CSS stylesheet,
   1. it defines its own `<title>`.

2. In the `<main>` part of the page, add

   1. a heading `Address` (the required tag is not `<head>` nor `<header>`)
   1. the image [contact.jpg]({{site.baseurl}}/assets/contact.jpg) to illustrate
      that we are listening.
   1. add our address with the tag `<address>` containing:
      IUT de Montpellier Sète <br>
      99 avenue d'Occitanie <br>
      34296 Montpellier Cedex 5 <br>
      Email : chuckn@yopmail.com

3. Validate your HTML page.

</div>


At this point, the job of structuring the Web page does not change the
layout. It is primarily meant to help your browser, or a search engine, to
understand your page. We will see how to change the global layout in the next
tutorials. For the rest of this tutorial, we will add style to some elements in
our page.

## CSS composition rules

[Recall that a CSS rule]({{site.baseurl}}/tutorials/tutorial1_2-en.html#introductory-tutorial)
is composed of a CSS selector and a statement block composed of several pairs
CSS property / value. A CSS selector indicates to which HTML elements the
style applies.

Starting from the basic selectors (of tag, class and id) presented
[in the previous tutorial]({{site.baseurl}}/tutorials/tutorial1_2-en.html#the-basics-of-css-selectors),
it is possible to create
[complex selectors](http://www.w3.org/TR/css3-selectors/#combinators). For
example, we will see how to select the `<div>` tags with class `toto` and who
are sons of an element of identifier `titi`.

We present in this section the most common ways to compose CSS selectors.

### Grouping selectors

The first way to compose selectors is by grouping them. The three following
rules:

```css
h1 {color: red}
h2 {color: red}
h3 {color: red}
```

can be grouped

```css
h1, h2, h3 {color: red}
```


### Combining selectors

To specify an element more precisely, it is sufficient to concatenate (without
spaces between them) several basic selectors (tag, class or id). For example:

```css
div.toto
```

will select tags of type `<div>` which have the class `toto`. Or

```css
.titi.toto
```

will select tags that have both the class `toto` **and**
`titi`.

### Combinators

We want to be able to limit a CSS rule to a sub part of the HTML tree. For this
matter, we will use combinators.

#### Child combinators

We can express that a tag has to be the child of another tag with the combinator
`>`. For example,

```css
#titi > .toto
```

selects the tags of the class `toto` who are **children** of the element of
identifier `titi`.

#### Descendant combinator

One can select a descendant with a spacing. For example,

```css
#titi .toto
```

selects the tags of class `toto` **descendants** of a tag of identifier
`titi`.

Therefore the difference with `>` is that this is no longer limited to the
children since it also incorporates the grandchildren, great-grandchildren ...

<div class="exercise-en">

We are going to make you play a game that allows you to check your understanding
of the selectors. The game is to write the selector which match the
instruction. The right part of the page is there to help you. The tags in the
game (`<plate>`, `<bento>`, ...) are not HTML5 tags but the principle of
selectors remains the same.

**Go on** [http://flukeout.github.io/](http://flukeout.github.io/) and pass
the levels 1 to 11 and the level 14.

**Notes:**

* You can go directly to an exercise by typing the the number of the exercise in
  the selector's place.


</div>

### Pseudo-classes

A pseudo-class is a way to indicate a particular state of an element that we
want to select. Here are a few examples:

```css
/* style of links <a> which have not been visited */
a:link {color: yellow;}
/* style of links <a> which have been visited */
a:visited {color: purple;}
/* style of links <a> when mouse is over them */
a:hover {text-decoration: underline;}

/* a paragraph which is the first child of his parent */
p:first-child {color:red;}
/* a paragraph that is the third child */
p:nth-child(3) {color: green;}
/* first li will be red, then second green, third red, fourth green */
li:nth-child(odd) {color: green;}
li:nth-child(even) {color: red;}
```


<div class="exercise-en">

3. Remove the fact that links are underlined. To do this, go read the
   documentation of
   [the property text-decoration](https://developer.mozilla.org/fr/docs/Web/CSS/text-decoration).
1. Ensure that the links `<a>` visited appear in lighter blue `#0088FF`.
2. When the mouse passes over a link, give him the color `orange`.

</div>

## Tables

The tag `<table>` is used to create tables or more generally to represent a set
of data in the form of columns and rows.

### Common table tags

The tag `<table>` contains the table.  The table is composed of rows (tag `<tr>`
for **t**able **r**ow) containing cells (tag `<td>` for **t**able **d**ata).

A tag `<th>` (**t**able **h**eader) must be a child of `<tr>`. It represents a
header cell (the title of a column or a row). It can be used in place of `<td>`.

Here is a typical table structure:

```html
<table>
   <tr>
      <th> Title1 </th>
      <th> Title2 </th>
      <th> Title3 </th>
      <th> Title4 </th>
   </tr>
   <tr>
      <td> Data1_1 </td>
      <td> Data1_2 </td>
      <td> Data1_3 </td>
      <td> Data1_4 </td>
   </tr>
   <tr>
      <td> Data2_1 </td>
      <td> Data2_2 </td>
      <td> Data2_3 </td>
      <td> Data2_4 </td>
   </tr>
   ...
</table>
```

<div class="exercise-en">

1. Create a table with seven columns labeld: `Acteurs, Karaté, Taekwondo, Judo,
   Chun Kuk Do, Tangsudo, Ju-jitsu`. This table must be at the bottom of the
   page `index.html`, in the additional part `<aside>`.

1. Put the labels corresponding to names of martial arts in tags `<span>`
   with class `skill`.

1. Add the six following rows (the numbers correspond to the value of the actor
   in the corresponding martial art):

   * Chuck Norris, 5, 5, 5, 5, 5, 5
   * Steven Seagal, 3, 5, 3, 2, 3, 5
   * Bruce Lee, 5, 3, 3, 3, 4, 3
   * Jean-Claude Van Damn, 5, 3, 3, 3, 4, 3
   * Bolo Yeung, 2, 4, 4, 2, 5, 3
   * Dolph Lundgren, 2, 4, 4, 2, 5, 3,

1. Test the conformity of your site.

</div>

### Tags `<thead>` and `<tbody>`

The elements `<thead>` and `<tbody>` are used to define more explicitly the
structure of our table:

* `<thead>`: The definition of the columns (`Acteurs, Karaté,`...)
* `<tbody>`: The body of the table, that is to say the rows (our heroes and
   their levels of competence).

<div class="exercise-en">

1. Add these tags to encompass these two parts (do not forget their closing tags
   `</thead>` and `</tbody>`)

1. Test the conformity of your site.

</div>


At this stage the structure of your table reflects the meaning that you wanted
to put. Let us now look at how to stylize it.

<div class="exercise-en">

1. Set a background color `#00AAFF` for the header part `thead` of the table.
1. Give the color purple `#640051` to the text of the skills in the table
   without changing the style of elements with class `skill` outside (see the
   [section on the selectors]({{site.baseurl}}/tutorials/tutorial2-en#css-composition-rules)).
1. Add a rule so that the background of every other row appears in white and
   the other with the color `#CCC` **without** changing in any way the HTML (see
   the
   [section on the selectors]({{site.baseurl}}/tutorials/tutorial2-en#css-composition-rules))
   **Attention:** `<thead>` must remain blue.

</div>

### The attributes `rowspan` and `colspan`

The tags `<th>` and `<td>` can take the attributes `rowspan` and/or `colspan`,
which allow to stretch the current cell to take the place of multiple cells:

* `rowspan` allows to stretch the cell on several rows,
* `colspan` allows to stretch the cell on several columns.

<div class="exercise-en">

It appears that Chuck Norris is always at the top (level 5) in all
martial arts.

1. Make the corresponding cell take the entire width to make it even more
   highlighted.
2. Give some more importance to the 5 of Chuck with a tag `<strong>` to show who
   is the boss.
3. (Optional) If you want to center the 5, go see
   [later in the tutorial](#center-horizontally) how to do it.

</div>

## The box model

As you saw earlier, all the structure tags define a box that takes all the
width. These boxes all have the following CSS properties:

* `margin`: outside margin of the border, between this box and the next, and/or
   between this box and its parent's box. The area covered by the margin is of
   the same color as its parent,
* `border`: border that surrounds the content. This property can take three
   values:

   1. `width`, e.g. `1px`,
   1. `style`, e.g., `solid`, `dotted`, `dashed`, ...  
      **Attention:** a border has no visible default style, therefore giving it
      a width is not enough to see it.
   1. `color`, e.g. `black`.

* `padding`: inner margin to the border, that is to say spacing between the
   content and the edge of the box. The padding is sharing the same background
   color as the box,

* `width`: the width of the content, *i.e.* of the box *content*

* `height`: the height of the content, *i.e.* of the box *content*

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodel.png" style="margin:0
auto;display: block;">

For example the following code

```css
.mybox {
  padding: 20px 50px 20px 50px;
  border: 5px solid green;
  background-color: gold;
}
```

is displayed like this (inspect the element)

<div style="text-align:center">
<div style="display:inline-block;padding:20px 50px;border:5px solid green;background-color:gold;">
the content area
</div>
</div>

<div class="exercise">

Inspect the box above to see the style which is applied on it. Find inside the
"Style" part of the dev tools the box model (see picture below). Inspect the
four boxes *content*, *padding*, *border* and *margin* to see them draw on the
screen.

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodeldevtool.png"
style="margin:0 auto;display:block;width:300px;">

</div>

There are three different syntaxs to give values to the `margin`, `padding` and
the `border`:

* `margin : t r b l;`  
  if we give 4 sizes `t`, `r`, `b` and `l`, then `t` is associated with the
  value on top, `r` for the right, `b` for the bottom and `l` for the left;
* `padding: v h;`  
  if one gives only 2 sizes `v` and `h` then `v` is associated with vertical
  values and `h` with horizontal. It is therefore equivalent to `padding: v h v
  h;`.
* `padding: a;`  
  if one gives a single value, it will be associated with the four sides of the
  box, as if we had written `padding: a a a a;`.

Examples:

```css
#titi {margin: 5px 0 7px 4px;}
/* Vertical margins (high and low) of 10px and horizontal of 5px */
div {margin: 5px 10px;}
/* padding in all directions of 5px */
.toto {padding: 5px}
```

**Note:** One can also specify (painfully) one value at a time with the
  properties `margin-top`, `margin-left`, `margin-bottom`,...

<div class="exercise-en">

1. Add a vertical padding of `10px` to the titles of sections,
1. Add a vertical margin of `30px` to paragraphs,
1. Add a horizontal padding of `5px` to the elements having the class `skill` in
   the table (but not to the elements having the class `skill` elsewhere).
1. Add a border to the titles `<h3>` of `1px`, style `solid` and color
`#CCCCCC`.

</div>


### Center horizontally:

To center the contents of a tag:

* If you want to center text in a tag or a text-level tag: `text-align: center`
* If you want to center a structure tag less wide than its parent tag: `margin:
auto` on the structure tag.


<div class="exercise-en">
1. Center `<body>` horizontally,
1. In the table, center the text of cells.
</div>

## Floating Content

The CSS property `float` makes the text go around an element. It takes values
`left`, `right`, `none` (and `inherit`) depending on where the text will get
round the element.

<div class="exercise-en">

1. Place the image of young Chuck to the left of the text (how to make a
   selector only for this tag?),
1. Place the image `beware_img` to the right of the text.

</div>

<div class="exercise-en">
1. Add a new paragraph which begins with the sentence "Spécialiste en arts
   martiaux, ..." of the section "L'enfance".

   You must then have the following rendering:

   <img src="{{site.baseurl}}/assets/noclear.png" alt="Sans clear"
    style="display:block;margin:0 auto;">

2. Rather, we wish to have this rendering:

   <img src="{{site.baseurl}}/assets/clear.png" alt="Sans clear"
   style="display:block;margin:0 auto;">

   To prohibit our paragraph to have a floating element on its left side, add
   the rule `clear:left`.  
   **Note:** We may also prohibit the right side with `clear:right` and the two
   sides at the same time with `clear:both`.

</div>

## Position

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

<div class="exercise-en">

1. Test your understanding of the above properties `position:
relative;top:20px;left:20px;` by applying them temporarily on the image
`chuck-jeune.jpg`.

2. Add icons of social networks
   [Facebook.png![Facebook]({{site.baseurl}}/assets/facebook.png)]({{site.baseurl}}/assets/facebook.png)
   and
   [Twitter.png![Twitter]({{site.baseurl}}/assets/twitter.png)]({{site.baseurl}}/assets/twitter.png).
   Position them at the bottom right corner of the browser window one above the
   other.

3. Try also temporarily to display them at the bottom right corner of the
   document (`<body>`).

</div>

**Reference:**
  [Mozilla Developer Network (MDN)](https://developer.mozilla.org/fr/docs/Web/CSS/position)
