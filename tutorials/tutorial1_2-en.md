---
title: TD1 Part 2 &ndash; The basics of CSS
subtitle: A page layout language
layout: tutorial
---

The standards defining the CSS are published by the World Wide Web Consortium
(<a Href="http://www.w3.org/"> </a> W3C) at the address
[http://www.w3.org/Style/CSS/](http://www.w3.org/Style/CSS/).

> Cascading Style Sheets (CSS) is a simple mechanism for adding style
> (e.g. font, color, space) to a Web document.  
> <cite><a href="http://www.w3.org/Style/CSS/"> W3C </a></cite>

The CSS is responsible for rendering the site on your screen,
but also on smartphone and paper printouts (CSS rules sets can be specified for
each of these media).

To know the basics of the CSS is relatively easy and essential for anyone who
wants work in the Web business. But mastering all aspects of CSS is a profession
(the one of Web integrator, which translates into HTML and CSS the work of the
web-designer).

## Introductory Tutorial

Here is a sample CSS rule

```css
h3 {
  font-style: italic;
  color: blue;
}
```

This CSS rule gives to all tags `<h3>` the italic style and color the text in
blue.

A CSS rule consists of two parts:

* A CSS selector that indicates which HTML elements the style applies to. In our
   example, the `h3` selector means that we will apply the style to
   all HTML tags `<h3>`;
*  a block of statements composed of several pairs CSS property /
value. In our example, the block contains two statements:
1. We give the value `italic` to the CSS property `font-style`;
1. We give the value `blue` to the CSS property `color`.

<div class="exercise-en">

Let's set up our CSS rules:

1. We will work mainly in this tutorial on a file `styles.css`. Create an empty
   text file `styles.css` in a new directory `css/`.  We will write our CSS
   rules in this file.

1. Copy in `styles.css` the above style `h3 {...}`.  Open the `index.html` page
   and notice that the style is not applied because we haven't linked yet the
   HTML with the CSS.

2. In the file `index.html`, add the following line in the header of the HTML
   document (in the `<head>` part ):

   ```html
   <link rel="stylesheet" type="text/css" href="css/styles.css">
   ```

   This line loads the CSS stylesheet `styles.css` and applies it to the Web
   page.

3. Reopen the `index.html` page and note that the style is now applied.

</div>


We will present you some [CSS properties](#some-css-properties) and how to
design [selectors](#the-basics-of-css-selectors).

## Development tools are your friends

For the HTML part, the development tools were already good friends; for the CSS,
they are promoted to the rank of "best-friend-forever". Select an HTML element
with the development tools not only allows to see the CSS rules applied to the
latter, it allows also to **change** them. Suffice to say that it is advisable
to abuse this tool during the tutorials for tweaking everything and anything.

<div class="exercise-en">

1. Inspect with the development tools (`F12`) one of the red texts. In the
   column on the right, you see the CSS styles applied to the inspected tag.

2. Disable the statement `color:#d00` and notice the change.

3. Note that your changes disappear when you refresh the page (`F5`). Indeed,
   you must save them in a stylesheet to keep them.

</div>


## Comments

In CSS, only comments with `/*` and `*/` are allowed. If you
use `//` in your file `styles.css` you will have problems
(the following CSS rules will not be applied).
 
<div class="exercise-en">

Comment the CSS rule `h3 {...}` in `styles.css` and notice that the titles
`<h3>` are no longer blue or italic.

</div>

## Some CSS properties

As said previously, the blocks of declarations include several
statements of the form `proprietyCSS:value;`. Here we present a few
examples of CSS properties and associated values.

### Colors

The colors can be used on several attributes of an HTML element:

 * Text color: `color: red;`
 * Background color: `background-color: blue;`
 * Border color: `border-color: yellow;` ...

The following 16 keywords can be used to define a color: `aqua`,` gray`,
`navy`,` Silver`, `black`,` green`, `olive`,` teal`, `blue`, `lime`,` purple`,
`white`,` fuchsia`, `maroon`,` red`, `yellow`. They were chosen to designate 16
well-distributed colors as shown in the following diagram:

<div style="text-align: center">
![Symmetry of 16 colors]({{site.baseurl}}/assets/HSL14colors.png).
</div>

CSS3 has added 147 keywords of colors that you can find at the address
[http://www.w3.org/TR/css3-color/#svg-color](http://www.w3.org/TR/css3-color/#svg-color).

You can be more specific and access to the 16 million colors that a screen can
display by the hexadecimal values `R`,` G` and `B` of respectively the Red,
Green and Blue components of the color. This is written with the format
`#RRGGBB` (or `#RGB` which is a shortcut). For example :

 * `#000000` is black,
 * `#FFFFFF` is white,
 * `#F00`, which is shorthand for` # FF0000`, is red,
 * `#FF00FF` is pink, which can also be accessed with the keyword` pink`.

**Note** You can use the website
  [http://www.colorpicker.com/](http://www.colorpicker.com/) to easily find the
  `# RRVVBB` code of any color.

### Dimensions

Some elements may have a size defined by CSS, other take the minimum space
required for their rendering.

The absolute most used unit of measurement is the "CSS pixel" `px`. This unit
often corresponds with the physical pixels on the screen but with some
subtleties:

1. current browsers allow you to zoom, which has the effect of displaying a "CSS
   pixel" over several pixels.
2. some media as the printer does not have pixels; CSS pixel is then defined as
   a scale allowing a good readability on the media.

Dimensions are used on different parts of an item. For example, CSS properties
and `width` and `height` allow you to force respectively the width and height of
an element (here the tags `<img>`):

```css
img {
    width: 50px;
    height: 100px;
}
```

One can also give relative dimensions in percentages; `width:50%` will
decrease by half the width compared to that which would have been calculated
normally.

**Reference:** For details on available units
[http://www.w3.org/TR/css3-values/#absolute-lengths](http://www.w3.org/TR/css3-values/#absolute-lengths)

### Fonts

We will list here the most used properties on fonts:

1. **`font-size`:** This property allows you to define the size of the
   font. Example:

   ```css
   font-size:12px;
   ```

1. **`font-weight`:** This property allows you to write **bold** text. Example:

   ```css
   font-weight:bold;
   ```

1. **`font-style`:** This property allows you to define the style of the
   font (*i.e.* italics or not). Example:

   ```css
   font-style:italic;
   ```

1. **`font-family`:** This property allows you to choose the font-family (or
   typeface) that you want to use. Example:

   ```css
   font-family: "Lucida Sans Unicode", "Arial", "sans-serif";
   ```

**Important:** The last two fonts specified by the rule are fallback fonts: they
will be used if and only if the previous are not available on the browser. A few
classic fonts are listed on
[http://www.w3schools.com/cssref/css_websafe_fonts.asp](http://www.w3schools.com/cssref/css_websafe_fonts.asp).


**Import new fonts:** You can import new fonts in your web page by using the
   `@font-face` property. Example:

```css
@font-face {
    font-family: myFontName;
    src: URL(path/to/font/font.otf);
}
```

If you want to learn more, go to
[https://developer.mozilla.org/fr/docs/Web/CSS/@font-face](https://developer.mozilla.org/fr/docs/Web/CSS/@font-face).
Here are two practical websites to download new fonts:
[http://www.1001fonts.com](http://www.1001fonts.com) and
[http://www.fontsquirrel.com](http://www.fontsquirrel.com).

**Reference:**
  [http://www.w3.org/TR/CSS21/fonts.html](http://www.w3.org/TR/CSS21/fonts.html)
  and [http://www.w3.org/TR/css-fonts-3/](http://www.w3.org/TR/css-fonts-3/).

### Texts

We will list here the most used properties concerning the display of paragraphs
of text:

1. **`text-align`:** This property affects the alignment of lines of text. Example:

   ```css
   text-align:center; /* or left, right, justify */
   ```
   
   For reminder, a justified paragraph is a paragraph where the lines go all the
   way from the left margin to the right margin.

1. **`line-height`:** This property allows you to space vertically the lines
of text. Example:

   ```css
   line-height:150%;
   ```
   
1. **`text-indent`:** This property will indent the first line of text,
   that is to say, it shifts it horizontally.  Example:

   ```css
   text-indent:12px;
   ```

   If given a percentage, the value of `text-indent` is understood as a
   percentage of the width of the parent element.

### Exercises

<div class="exercise-en">

1. **Colors:** The background of our page is all white by default. We are going to
change this and give `<body>` the color choosen by our web-designer: `#838892`.

2. **Dimensions:** several studies (cf.
   [1](https://viget.com/inspire/the-line-length-misconception) and
   [2](https://en.wikipedia.org/wiki/Line_length)) suggest that lines too long
   or too short seriously impair the readability of a site. To give a first
   treatment of the problem, limit the width of the `<body>` to `600px`.

4. Section titles must have their text centered.

5. The text must be spaced: use a line height of `150%`.

6. Each paragraph should be indented `5px`.

3. Go get a font of your choice on
   [http://www.fontsquirrel.com](http://www.fontsquirrel.com). Link it to your
   document with `@font-face`. Apply it to the section titles `<h2>` and do not forget to give fallback fonts.

   **Warning:** If you use spaces in the name of your font, you will have to
      surround it with quotation marks.

10. The CSS is a standard just like HTML. Test the conformity of your CSS file
    with the validator
    [https://jigsaw.w3.org/css-validator](https://jigsaw.w3.org/css-validator).

</div>

## The basics of CSS selectors

CSS selectors are used to specify which elements will be impacted by a CSS
rule. They are also used on other issues of Web development that we will see
next year. In short you will have a question about them in the exam, that is for
sure.

As you know from the
[tutorial 1]({{site.baseurl}}/tutorials/tutorial1_1-en.html), an HTML tag can
take attributes. Two attributes are very important for the CSS rules: The
identifier attribute `id` and the class attribute `class` of a tag.

For example :

```html
<h2 id="myidentifier" class="skill feature">... </h2>
```

This HTML snippet declares an HTML `<div>` tag with the unique identifier
`myidentifier` and having two classes:  `skill` and `feature`.

**Warning** an identifier must be unique in the HTML document. But an element can
have several classes as in the previous example and these classes are made to be
assigned to multiple page elements.

The classes, identifiers and tags are used to build 90% of CSS selectors.  Let
us take a look at the syntax to use them.

### Tag selectors

You just have to use the name of the tag (`a`, `p`, `img`,...) without further
decorator. If we want to give the purple color for all links `<a>` on a page, you
must write

```css
a {
    color: purple ;
}
```

### Identifier selectors

The decorator associated with identifiers is the character `#`. If one wants to
give a width of `100px` to the unique tag with the identifier `myidentifier`, he
must write

```css
#myidentifier {
    width: 100px;
}
```

### Class selectors

The decorator associated with class selectors is the character `.`. If one wants
to give a height of `200px` to all elements which have the class `skill`, he
must write

```css
.skill {
    height: 200px;
}
```

### Exercises

<div class="exercise-en">

2. In accordance with the model of the designer
   [target.png]({{site.baseurl}}/assets/target.png), the background colors for
   section's titles should alternate between values `#5BBDBF` and `#FF5850`. For
   this, we want you to add alternatively a class "even" or "odd" to elements
   `<h2>`, and separately alternate on elements `<h3>`. Add the appropriate
   style to those classes in `styles.css`.

3. The image `beware.jpg` has style, but it takes a little too much space: limit
   its height to `300px`.  
   **Warning:** The limit of `300px` should only apply to the image
   `beware.jpg` and not to `chuck-jeune.jpg`. How would you do that ?

5. We want to highlight the countless martial arts mastered by Chuck Norris. To
   do this :

   1. we will surround each of these martial arts (Taekwondo, Ju-Jitsu, ...)
      with a `<span>`  with class `skill` in the HTML file.

   2. On the other hand, create the CSS rule that gives to all
      elements with class `skill` the following layout: red text
      and italics (or whatever makes you happy).

10. Test the conformity of your CSS file with the validator
    [https://jigsaw.w3.org/css-validator](https://jigsaw.w3.org/css-validator).

</div>

## Concluding Remarks

### CSS and HTML: very distinct and complementary roles

There is a clear separation between the roles of HTML (content with tags to add
meaning) and CSS (page layout). This choice is not obvious at first: for
example, a Word document does not separate the presentation from content. But
this separation is essential and powerful:

 * It allows you to reuse a presentation from one page to another. For example
   when *lemonde.fr* publishes a new article, it does not rewrite the style
   expressly for it: it is a new HTML document sharing the same CSS as previous
   articles;
 * It allows you to change the layout of your website by focusing on CSS without
   touching the HTML (too much);
 * It allows you to change the presentation of a document depending on whether
   it is intended to be printed or to be viewed inside a browser.

