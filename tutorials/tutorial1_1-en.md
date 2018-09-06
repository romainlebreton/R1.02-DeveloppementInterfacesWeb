---
title: TD1 Part 1 &ndash; HTML - a markup language for structuring documents
subtitle: Doctype and first tags
layout: tutorial
---

<!-- Make a note more complete on the encoding of the characters -->

The purpose of this TD is to understand how are written basic Web pages,
also called static pages (Web 1.0). Such Web pages contains two
parts:

1. **HTML**: The HTML file contains the structure of the page and its content;
in addition to plain text, it gives meaning to the text by indicating what is in
fact a paragraph, a title, *etc*, using **tags** (for example `<p>`,
`<title>`,...);

2. **CSS**: The CSS file is responsible for the layout of these elements on the
page (put this paragraph in pink, use the font "Sans serif" for this title,... )

The browser (Firefox, Chrome, Safari, IE/Edge, ...) is the software that allows
us to view the Web pages. The purpose of this TD is to demystify the way that
these two types of files are interpreted by the browser.  For this matter, we
will produce a website whose rendering corresponds to the file
[target.png]({{site.baseurl}}/assets/target.png), starting from the file
[index.txt]({{site.baseurl}}/assets/index.txt) which contains the raw content of
the website to achieve.

We start by clarifying the structure (the HTML) that we can add to our raw
content. Then we will see in the [second part of TD](tutorial1_2-en.html) how to
obtain the rendering proposed by [target.png]({{site.baseurl}}/assets/target.png)
by means of a CSS file.


## From a raw text to an HTML document

### What does a browser do ?

As said previously, the role of the browser (Firefox, Chrome, Safari, IE/Edge,
...) is to render the Web pages. So the browser transforms a raw text file
containing HTML/CSS to a display with proper layout, with images ...


<div class="exercise-en">

1. This tutorial is a Web page. Open the sources of this page to see the HTML
source code that is used to display this page (right-click and then source code
or `Ctrl+U`).

</div>

<div class="exercise-en">

To create a Web page, it is enough to create a text file and to give him the
extension `.html` so that the browser understands that it must interpret it as
an HTML document.

1. Save the file [index.txt]({{site.baseurl}}/assets/index.txt) locally in a
folder `HTMLCSS/TD1/`.  
   Save the same file [index.txt]({{site.baseurl}}/assets/index.txt) locally in
   the folder `HTMLCSS/TD1/` **and rename it** `index.html`.

1. Open both files [index.txt]({{site.baseurl}}/assets/index.txt) and
   `index.html` in the browser.  
   What differences do you observe in the rendring? Why?  
   How are displayed line breaks in an HTML document?  
   How is displayed a HTML text surrounded by `<!--` and `-->`?
   <!-- saut de ligne mangés, mauvais accents, commentaire coupés : interprétation du HTML -->

</div>

### The standard of the HTML language

Our document `index.html` is well interpreted as a HTML document by the
browser.

HTML, which means *HyperText Markup Language*, is a markup language containing
links, called *hypertext links*, to other documents. Markup is a synonym of
annotate. A markup language annotates its content to give it structure. 

HTML is a standard, that is to say a language described completely (do not
hesitate to throw a quick glance
[to its specification](http://www.w3.org/TR/html5/), a highly technical document
but very complete).

<div class="exercise-en">

1. Test the conformity of `index.html` to the HTML5 standard using the validator
   [https://html5.validator.nu/](https://html5.validator.nu/). What are the
   errors indicated?

2. Let us start by the error

   ```text
   Error: Non-space characters found without seeing a doctype first. Expected <!DOCTYPE html>.
   ```

   The validator is telling us that he expected to see `<!DOCTYPE html>` at the
   beginning of our document. This tag is used to declare that the document is
   written in HTML5. Indeed, there are several standards of "HTML": HTML4,
   XHTML, HTML5, ... Today, people mainly use HTML5 and we will do the same.

   For the document to be valid and recognized as an HTML5 document, **add** the
   tag `<!DOCTYPE html>` at the very beginning of the file.  
   **Retest** the conformity of your document.

3. The validator now indicates **The character encoding was not declared**.

   The encoding indicates in which way the file is saved (UTF-8, ANSI,
   `ISO-8859-15`, ...). If most of the characters are saved only one way, the
   special characters (french accents, œ, ...) can be saved in many different
   manners.

   When the encoding is not specified, the browser may display **Ã©** instead of
   **é** because of a wrong detection of encoding. Indeed, the character **é**
   is recorded in UTF-8 in the same way that **Ã©** is recorded in `ISO-8859-15`
   (encoding still very used in Windows).

   Specifying the encoding of the characters is therefore necessary to make sure
   that the special characters in your Web pages are correctly interpreted. We
   will always use the encoding UTF-8 (and ideally everyone should also use it).

   1. **Add** therefore the following line that declares the encoding in the header of the
      document just after the DOCTYPE.

      ```html
      <meta charset="utf-8">
      ```
   
   1. Reopen `index.html` in the browser and verify that all accents are
      displayed properly.
   
      **Note:** If the accents still do not work, it is because **it is not
      enough** to say that your file is in UTF-8. You must also **save your file
      in UTF-8** for real. For example in Notepad++, the encoding is marked at
      the bottom on the right. You can convert your file in UTF-8 by looking in
      the menus.
   
   1. **Retest** the conformity of your document.

4. The last error is about an element `head` which is lacking a `title`.
   Correct your Web page by inserting a title after the `<meta>`.
   
   ```html
   <title>The non official website of Chuck Norris </title>
   ```

</div>

At this stage, the validator indicates that the file `index.html` is a valid
HTML5 document.

## The usual structure of an HTML document

### HTML Tags

We have seen in the previous exercise our first tags `<meta>` and `<title>`. The
tags allow you to structure the document. They annotate the text they contain
and therefore allow to add meaning to it. There are two types of tags:

1. Most of the tags **include content**: they begin with a *opening tag*
`<mytag>`, then the *content* that it wants to annotate and end by a *closing
tag* `</mytag>`. For example, the tag `<title>` is used to say that the text
inside will be the title of the document.

2. [Some tags](http://www.w3.org/TR/html5/syntax.html#void-elements) **do not
accept any content**: they just consist of an opening tag.  For example, we
have seen the tag `<meta>` and we will soon see `<img>`, `<br>` ...

**Example:**

```html
<p>This is an HTML paragraph since it is surrounded by 'p' tags </p>
The 'br' tag means a line break and accepts no content <br>
```

### The basic structure

Let us tags to create a well structured HTML document:

```html
<!DOCTYPE html>
<html>
    <head>
        <!-- The header must include at least a title -->
        <meta charset="utf-8">
        <title>A title that is displayed in the tab of the browser</title>
    </head>
    <body>
	   <!-- The body of the document -->
	</body>
</html>
```

After the statement of the language `<!DOCTYPE html>` , the document is included
in the tag `<html>` and is composed of two parts:

* The header `<head>` contains information on the HTML document itself, as for instance
   * a `<title>` (mandatory tag)
   * a `<meta>` tag to set the encoding

* The body `<body>` contains the actual visible content. We will see examples of
tags in the section *Common Tags*.

### An HTML document is like a tree

HTML tags provide a tree structure to the document. In our example
`index.html`

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>The non official website of Chuck Norris</title>
    </head>
    <body>
	   ...
	</body>
</html>
```

<div style="float:right">
<p style="margin:0">
<img alt="Tree structure" src="{{site.baseurl}}/assets/arbre.svg">
</p>
</div>

The tree is the following:

* `<html>` is the root node
* `<head>` and `<body>` are the two children of the node `<html>`
* `<title>` and `<meta>` are two children of the node `<head>`
* "The non official website of Chuck Norris" is a child of the node `<title>`.

<div style="clear:both" class="exercise-en">

1. Update your page `index.html` so that it respects the HTML structure
   above.  
   (You must add the tags `<html>`, `<head>` and `<body>`)
2. **Retest** the conformity of your document.
</div>

<!-- Explication orale sur l'importance de la validation : standard, uniformité -->

## Web development tools

In the rest of this tutorial, we will use our browser to "inspect" our Web
page. For this we recommend Chrome/Chromium or Firefox. Press the `F12` key to
enable development tools. The development tools are split in two distinct parts,
one dedicated to the HTML and the other to the CSS. The dev tools are fabulous
to learn how Web pages are built.

There are three ways to inspect a particular item:

* Right click on the Web page then "inspect/review the element" : this allows
you to see the corresponding HTML code in the development tool panel.
* Click ![Inspector]({{site.baseurl}}/assets/magnifying.png) in the development
tool : this allows you to go out and inspect an area of interest in the page (by
overview with the mouse).
* When you pass the mouse over an item in the development tool panel, this
element gets highlighted on the Web page.

<div class="exercise-en">

Familiarize yourself with these three techniques by inspecting the page of the
tutorial.  For instance, make a right click on the element "There are three
ways..." then "inspect element". The development tool will focus on the HTML
code and position you directly on `<p>There is ...`.

</div>

<!-- Hey ! this is an HTML comment, you are not supposed to see this, unless you
know how to use the dev tools ? -->

## Common HTML Tags

### Comments

It is possible to add comments in the HTML source code. These comments are not
interpreted by the browser, and are therefore not displayed (but they remain
present in the source code). Therefore it is a piece of information left by
developers for developers. Comments are placed between the special tags `<!--`
et `-->`:


```html
<!-- This is a comment in an HTML document -->
```

Since we speak about comments, the file `index.html` is full of them. They are
instructions for future exercises.

### Titles

Let us begin to add some structure to our page. To do this we will use the tags
`<h1>` to `<h6>` to identify the different sections:

* `<h1>` is used for big headlines of the document
* `<h2>` is used for the sections of the document
* `<h3>` is used for the sub-sections of the document and so on.

For example, the above title is obtained with the following code:

```html
<h2>Titles</h2>
```

<div class="exercise-en">

1. Check that the title **Titles** just above is an `<h3>` tag using the dev
   tools by right-clicking on it.
1. Add the Tag `<h2>` to the elements of `index.html` marked by the comments:
   `<!-- section -->`.
2. Add the Tag `<h3>` to the elements of `index.html` marked by the comments:
   `<!-- sous section -->`.
3. **Retest** The conformity of your document.

</div>

### Grouping content

#### Paragraphs

<div class="exercise-en">

Use the tags `<p>` and `</p>` around the paragraphs in the document. The
paragraphs are indicated by the comments `<!--début paragraphe -->` and `<!--fin
paragraphe -->`.

**Note:** If you right-click then "inspect the element" on this paragraph, you
will see precisely that this text is in a paragraph.

</div>

#### Lists

In HTML we can obtain ordered (numbered) lists or unordered lists:

```html
<ul> <!-- ul stands for unordered list -->
  <li>First unordered item</li> <!-- li stands for list item -->
  <li>Second item </li>
</ul>
<ol> <!-- ol stands for ordered list -->
  <li>First ordered item</li>
  <li>Second item </li>
</ol>
```

Once interpreted by the rendering engine of the browser, it gives:

<div class="codeexample" style="margin:1em 0px;">
<ul>
<li>First unordered item </li>
<li>Second item </li>
</ul>
<ol>
<li>First ordered item </li>
<li>Second item </li>
</ol>
</div>

<div class="exercise-en">

1. Use the tags `<ul>` and `<li>` to structure the bullet list `<!--liste -->`
in `index.html`.  (Do not worry yet about comments `<!-- lien externe -->`)
2. Use the tags `<ol>` and `<li>` to structure the numbered list `<!--liste
numérotée -->` in `index.html`.
3. **Retest** the conformity of your document. (In fact you should regularly
test it by yourself, but we will hold your hand during this first tutorial)

</div>

### Image: An example of embedded element

To insert an image, you can use the tag `<img>`

```html
<img src="image_location" alt="alternative text (not optional)">
```

This tag has no closing tag because it can not have content
(cf. [the beginning of the tutorial](#html-tags)). We note that it has two
fields `src` and `alt` that are called the **attributes** of the tag. The
attributes are **always** located in the opening tag.

<div class="exercise-en">
Previously, we had seen another tag with an attribute: What was this tag?
<!-- `<meta>` avec l'attribut `charset`. -->
</div>

The attribute `src` must contain the location of the image. The attribute `alt`
allows you to add an alternative text for browsers that cannot display images
(e.g. textual browser <a href="http://lynx.browser.org/">Lynx</a>) or for the
persons who can not see images clearly (blind or people with visual
deficits). **Careful**, the `alt` attribute is mandatory.


<div class="exercise-en">

1. Save the image [chuck-jeune.jpg]({{site.baseurl}}/assets/chuck-jeune.jpg) in
a directory `images` located where `index.html` is.

2. Replace the comment `<!--l'image de Chuck Young doit être positionnée ici
-->` by the following tag `<img>`

   ```html
   <img src="./images/chuck-jeune.jpg" alt="Une photo de Chuck Jeune, la légende est en marche.">
   ```

   **Note:** The address `./images/chuck-jeune.jpg` is a relative address. The
   point means "the folder of the current web page". Therefore we will go and
   get the image in the folder `images` of the directory containing the
   web page `index.html`.

3. Do the same and position the image
  [beware.jpg]({{site.baseurl}}/assets/beware.jpg) in place of the comment
  `<!--l'image de Chuck Beware ici -->`.

4. Guess what? You must **retest** the conformity of your document.

</div>

### Semantic elements

#### External links

One of the most emblematic tag of HTML is without doubt `<a>`. It allows you to
make hypertext links (the HT in HTML).

A link is composed mainly of a target URL and a label (the clickable text often
underlined in blue):

```html
<a href="http://target_url">The label</a>
```

You can specify the complete URL of the target (absolute path), for example:

```html
<a href="http://lynx.browser.org/">Lynx</a>
```

or give a relative address to the current page (relative path), for example:

```html
<a href="./images/chuck-jeune.png">Image</a>
```

<div class="exercise-en">

1. Replace the comments `<!-- lien externe ...` by tags `<a>` with the correct
   address.
2. **Retest** the conformity ...
   
</div>

#### Internal links

We can add to these *external links* an *internal* part based on anchors
`#myanchor`. All tags can take an `id` attribute as in the following
example. **Attention**, the value of this attribute must be **unique** in the
document.

```html
<h2 id="an_identifier">
```

One can make a link to this tag by adding `#myanchor` at the end of the URL. For
example, here is a internal link to the tag whose `id` is `an_identifier` inside
the current web page `index.html`:

```html
<a href="index.html#an_identifier">Example of internal link</a>
```

You can shorten the URL as follows. If you do not indicate the document, it
points to the current document by default :

```html
<a href="#an_identifier">Example of internal link</a>
```

<div class="exercise-en">

1. Replace the comment `<!-- lien interne ...-->` of `index.html` by a tag `<a>`
   which will point to one of the first tags. Therefore you will need to add an
   identifier to this target tag.
2. Test the functionality of your link by clicking on it. They must take you to
   the tag with the matching identifier.
3. **Test** the conformity ...

</div>

#### Emphasis

The tag `<em>` allows you to highlight important parts in a text.

<div class="exercise-en">

Precisely, it is necessary to underline the fact that Chuck Norris is very strong in
different martial arts. For this it is necessary to put in emphasis the sentence which
follows the comment: `<!-- mettre en emphase cette phrase -->` in the file
`index.html`.

</div>

**Note:** There is another type of emphasis which is obtained with the tag `<strong>`.

#### Quote

Here is a magnificent example of citation:

<blockquote> 
Un biscuit ça n'a pas de 'spirit', c'est juste un biscuit. 
Mais avant c'était du lait, des oeufs. Et dans les oeufs, il 
y a la vie potentielle.  
<cite>Jean-Claude Van Damme</cite>
</blockquote>

The quotes are used to identify a short text on which one wants to attract the
attention. This is used in particular to show that one has some `spirit`.

<div class="exercise-en">

1. Go see the source code of our quote using the dev tools. What are the two
   **new** tags used?
   <!-- `<blockquote>` et `<cite>` -->

   The first tag (which starts with a `b`) surrounds the full citation while the
   second (which starts with a `c`) contains only the reference (the author, the
   book, ...).

1. Use these two tags to put more attention on the quotation at the beginning of
   document (search for `<!-- utiliser blockquote ici -->`).

2. Have you checked throughout the tutorial that your HTML page remains valid?

</div>

## Finished!

We are done for now with regard to the content and the structure of our site. We
have learned how to add structure to an HTML page with specific tags.

In the [2nd part of this tutorial](tutorial1_2-en.html), we will see how to
improve the appearance of the site.

**Note:** Why would the appearance of the title change when we add the tag
`<h1>` to it ? Should not this change only the structure and not the layout of
the page (which is CSS job)?  
In fact, browsers apply default CSS styles to some HTML tags. For example, links
`<a>` are underlined and blue without doing anything. This avoids to have to
redo everything every time in CSS: the browser offers a default style.

<!-- Dans le devtools, elles s'appelent user agent rules -->

<!-- Pour afficher les extensions de fichier Dans l'explorateur : alt pour
afficher les menus, outils, options des dossiers, affichage, décocher cacher les
extentions dont le type est connu -->
