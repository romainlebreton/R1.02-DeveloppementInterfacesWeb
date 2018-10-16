---
title: TD5 &ndash; Responsive Design
subtitle: Adapting to the media 
layout: tutorial
---

## Introduction

Smartphones, tablets and all mobile devices ask us to rethink the web
today. Designing a Web site or a Web application for all these media is not a
task trivial. Here is an overview of the many existing solutions:

* Coding two sites in HTML / CSS: one for computers and one for smartphones (and
  one for tablets? And one for smartwatches?). Example:
  [lemonde.fr](http://lemonde.fr) and
  [mobile.lemonde.fr](http://mobile.lemonde.fr)
* Native applications for each system (Android, iOS, Windows Phone, ...)
* Use JavaScript to adapt the layout dynamically
* Make the site in Flash (very bad idea because it is no longer supported on
  Android and iOS).
* A solution in pure CSS. Indeed, CSS is the basic language for laying out
  web-pages. It is in constant evolution (CSS3 under development) to adapt to
  new needs.

Let us take two starting hypotheses:

* "There is no need for an application!" : No need to develop native Android or
  IOs applications.
* "There is no need to do two websites for this!" : We do not want to code a
  specific website for each media (computer, tablet, ...).

We will adopt an iterative approach in this tutorial and add constraints one
after another until we arrive at what is done today in terms of responsive
design.

## CSS2

Some properties did not wait for new media or CSS3 to be popular among
developers. Let us start with the properties that were already in CSS2.

### Percentages '%'

We can begin by expressing all the sizes relatively. That is what we have
already done using the dimensions in percentages `%`. Recall that when an
element is in `display:block` or `display:flex`, its width is fixed with respect
to its **containing block** (its closest `block` of `flex` ancestor). For
example, by default `block` or `flex` elements will take the whole width of
their parent. Also, if we set a relative width in percentage when it is relative
to the width of the **containing block**.

<div class="exercise">

1. Set the `width` of `<body>` to `100%`. Put the horizontal margins of `<body>`
   to `auto` (it will center body later).
1. Remove the left margin of `10%` on `<aside>` and change the relative width of
   `<article>` and `<aside>` to respectively `67%` and `33%`.

</div>


**Note :** If adapting the widths in percentage works well, this is not the case
of heights. This is due to the fact that the width of the page is known (it is
the width of the window to display the browser) but its height is not known yet
(since the page is not yet displayed and that the height will depend on the
amount of content).  In other words, the height of the area of the browser where
it displays the page (`viewport height`) is not necessarily the height of the
page [^somesamplefootnote] (and it is linked to the presence of a scrollbar to
the right to go down the page).

[^somesamplefootnote]: The `vh` unit (for `viewport height`) can be used to
    define heights relatively to the viewport.


### `max-width` and `min-width`

the previous rules allow to have a good-looking ratio of width, but not
an optimal rendering:

* on small computer screens, elements may not be displayed correctly (images,
  columns, ...)
* on very large screens, the text becomes illegible (unreadable): the eyes get
  tired because of the lines too long.
 
 To constrain the maximum and minimum dimensions, we will use `max-width`,
 `max-height`, `min-width`and `min-height` which take the same type of values as
 `width` and `height`.

<div class="exercise">
<!-- 1. Set a minimal width of `150px` to the pictures of Chuck Norris. -->
1. Set a maximal width to `<article>` and `<aside>` of respectively `500px` and
   `250px`.
1. Set a minimal width to `<article>` and `<aside>` of respectively `200px` and
   `150px`.

</div>


### Over-constraint dimensions

But what happen if you mix `min-width` with width in percentages ?  Suppose that
you have

```html
<div style="display:flex">
	<div style="width:50%;max-width:400px;">
		Div1
	</div>
	<div style="width:50%;">
		Div2
	</div>
</div>
```

then it displays like this

<div style="display:flex;border:1px solid black;">
<div style="width:50%;max-width:400px;background-color:orange;">
Div1
</div>
<div style="width:50%;background-color: cornflowerblue;">
Div2
</div>
</div>

<br>

<div class="exercise-en">

**Notice** that :

1. the two `<div>` takes the whole width of body when the width of `<body>` is
   less than `800px` (so the first `<div>` width is less than `400px`)
2. but when the width of `<body>` is greater than `800px`, then the two `<div>`
   do not fill the whole width of `<body>`.

**Change the width** of your window to see this change of behavior.

</div>

We will use `display:flex` to get a better mix of relative width (or height) and
`min-width`/`max-width`. We have already seen the rules in the left column of
[this awesome page about FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/):
it is those that apply to the parent. Now we are going to discover the rules in
the right column: those which apply to the elements. **Take a look** in
particularly at the properties `flex-shrink` (default value `1`) and `flex-grow`
(default value `0`). For now, we won't touch at `flex-basis` which will keep its
default value `auto`.


<div class="exercise">

1. Read about `flex-shrink` and `flex-grow` on
   [the guide to FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
   or any other webpage until you understand how they work. Feel free to talk to
   your professor to discuss your comprehension.

1. Let's give an example of use of `flex-grow`. Your job is to see if you
   understand it:

   We can now solve your previous problem by adding `flex-grow:1;`.

   ```html
   <div style="display:flex">
   	<div style="width:50%;max-width:400px;">
   		Div1
   	</div>
   	<div style="width:50%;flex-grow:1;">
   		Div2
   	</div>
   </div>
   ```
   
   displays like this
   
   <div style="display:flex;border:1px solid black;">
   <div style="width:50%;max-width:400px;background-color:orange;">
   Div1
   </div>
   <div style="width:50%;flex-grow:1;background-color: cornflowerblue;">
   Div2
   </div>
   </div>

   Now when the width of `<body>` is greater than `800px`, then the second
   `<div>` increases its width because of `flex-grow:1;`. So now, they do fill
   the whole width of `<body>`.

1. Change the width of `<article>` and `<aside>` so that they are `300px` and
   `200px` by default. Set the values of the properties `flex-shrink` and
   `flex-grow` of those two elements to `0`.  
   **Change** the width of this page. Do the width of `<article>` and `<aside>`
     change?

1. We wish that when the screen is too wide, the remaining horizontal space is
   divided between `<article>` and `<aside>` so that `<article>` grows 3 times
   faster than `<aside>`. 

   **What CSS property**  should you use to get this behavior ?
   **Code** this.

1. In order to verify your comprehension of how the remaining horizontal space
   is divided, resize your browser window so that the width of `<body>` is
   `620px`.  
   What should be according to you the widths of `<article>` and `<aside>` ? Now
   inspect the widths of `<article>` and `<aside>` to check your computations.

1. We wish that when the screen is too small, `<article>` shrinks twice as fast
   as `<aside>`.  
   What CSS property should you use to have this behavior ?  Implement this
   behavior.

</div>


### Radical changes in layout

There comes a time when diminishing the width no longer makes sense. We have to
change the global layout, by passing `<aside>` below `<article>` or completely
delete `<aside>`.

**Responsive design** is the name of the idea of changing the layout depending
on the size of the screen.

The CSS rules already seen in the tutorials do not allow to code this kind of
behavior. We need a way to write CSS that will be valid only in specific
cases. We will see in the next section how this is possible in CSS3.

## Your Chuck Norris website on a smartphone

### Useful tools

Until now, it could be considered that all development tools of Internet
Explorer / Firefox / Chrome were equal. In fact, the Chrome were already a bit
better (auto-completion, drop-down menus of possible values, faster, more
reliable). Anyhow, when we deal with responsive design, Chrome has no match: the
development tools of Chrome/Chromium will become your *"best-friend-ever"*.


### What does my smartphone browser do by default ?

How can we make a website compatible with smartphones mobile at a lower cost ?

Here is the (simplified) algorithm that works by default :

* generate the website on a larger virtual screen, say having a width of `980px` ;
* Zoom out so that the website fits on the smartphone's screen (some elements
  will display really small) ;
* Assume that the user will use the *pinch to zoom* to navigate of the page :
  <img src="{{site.baseurl}}/assets/pinch_zoom.png " alt="Pinch to zoom schema"
  style="margin: 0 auto;height:100px;vertical-align:middle;">


And it works! In fact, that is what is done by smartphone's browsers when we are
on a non-responsive website.

<div class="exercise">

1. Using Chrome/Chromium development tools (`F12`), enable the device mode
   <img src="{{site.baseurl}}/assets/phone-responsive.png" alt="Outil pour mobile"
   style="margin: 0 auto;width:45px;vertical-align:middle;">
   *"Samsumg Galaxy S5"* and reload your webpage. It should display very small.

1. Inspect `<html>` to see the width of the screen. Check that it `980px`.  
   See that the actual width of the display is `360px`.  
   This means that the previous algorithm has been used to display your website.

</div>

Even if it works, it can not be said to be optimal. The mobile user does not
have the same expectation as the computer user : he wants to have rapid access
to essential information. One can imagine that on a smartwatch, for instance, a
weather forecast website would display a lot less information (maybe just a
cloud or sun and the temperature).

Typically we want to remove entire parts of the site depending on the size of
the screen.

Since we are going to the manage the responsiveness ourselves, the first thing
to do is therefore to deactivate the previous algorithm. In the `<head>` tag,
write:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

<div class="exercise">

Add this HTML code to your Chuck Norris website. Check that the display is
different when you use the device mode of Chrome. What is the new width of
`<html>` ?

</div>

You should find that the previous algorithm no longer applies. The browser is no
longer trying to be smart: it lets you be in charge.


## Technical solution using CSS3 : media queries

Media queries are a set of options added to the CSS3 standard that help to
define CSS rules that will apply only under certain specific conditions.

There are two different ways to use a *media query*:

* Either you write many specific CSS file (one for smartphone, one for
  computers, etc.) and you want to say which CSS file apply in what
  condition. Then it is necessary to add a `media` attribute to your declaration
  of CSS file in `<head>`:
  
  ```html
  <link rel="stylesheet" media="condition" href="mon_css_special.css"/>
  ```
  
  The condition in `media="condition"` will tell something like *"apply this CSS
  only when the screen is wider than `920px`"* for example. We will see later
  the syntax of conditions.

  Do not forget that the last loaded CSS takes precedence over the previous
  ones. Remember to always declare your media queries in last position ; if not
  they will be systematically overwritten by your *standard* CSS file.

* Or you just want certain rules to be applied under certain conditions. Then
  you need to englobe your CSS rules with `@media(ma_condition) { ... }`. For
  instance :

  ```css
  @media(ma_condition) {
    div {background-color:white;}
    ...
  }
  ```
  
A media query works in the following way: the condition is
evaluated and returns a value "true" or "false". If the value is True,
the CSS file/ the CSS rule (depending on the method used) is applied.

Each condition is formed from one or several basic conditions. Among
[all the possible conditions](https://developer.mozilla.org/fr/docs/Web/CSS/Media_queries),
let's focus on the following ones.

* `min-width`, `max-width`, `min-height` and `max-height` : Say if some
  dimension should be less/greater than some value. For instance

  ```css
    @media(min-width:100px) {
      div {background-color:white;}
    }
  ```

* `orientation` : its values are `landscape` (horizontal screen) or `portrait`
  (vertical screen)


The basic conditions can be combined together to form complex conditions using
logical operators `and`, `,` (or) and `not`.

**Example :** The media query condition `(min-width: 500px) and (min-height:
800px)` is true if and only if the display width is `≥500px` and its height is
`≥800px`.


<div class="exercise">

* Go to the [Bootstrap website](http://getbootstrap.com/) and find the widths
  for which the layout is changing.
* Use the device mode of chrome to show the media queries (click on the 3 dots
  on the top right corner of the window to do this). Check your previous
  findings.
* What changes in the layout when the width changes around the break-point
  `768px`?

</div>


### Breakpoints

In order to organize our *media queries*, we generally use 3 to 4 screen widths
values, for example:
 
 * `480px` (Smartphone)
 * `768px` (Tablet)
 * `992px` (Standard computer screen)
 * `1200px` (Wide computer screen)

<div class="exercise">
 1. On Chuck's website, remove the table that compares martial arts skills when
    the width is less than `768px`.
 1. Below `480px`, put `<aside>` below `<article>` (the display direction is
    column instead of row).
 1. (Optional) On smartwatch (width `<168px`), display only Chuck Norris' quotes
    contained in `<aside>`.

</div>


### Put me a burger on the menu!

When the size of the screen is limited, a good practice in *responsive design*
is to replace the menu by a burger button:

<img alt="Burger button, three horizontal lines, (two corresponding to the
bread, and the one for the meal) " src="{{site.baseurl}}/assets/burger.png"
style="margin:0 auto;display: block;">

When clicked, the menu will appear. The page is not wasting any space when the
menu is closed. To fix the ideas, we want a menu that appears sideways in the
manner of the following examples (don't look at the JavaScript):

 * [http://codepen.io/gungorbudak/pen/XbazEX](http://codepen.io/gungorbudak/pen/XbazEX)
 * [http://codepen.io/drewr/pen/uxvdt](http://codepen.io/drewr/pen/uxvdt)

(Note by the way that [codepen.io](http://codepen.io/) is a very useful tool to
learn new techniques !)

<div class="exercise">

We will code a second menu, identical to the first one in its content, but with
a different layout. We will display one menu of the other depending on the size
of the screen.

1. Add a `<div>` of class `burger` containing the image of the burger (width
   `50px`) just before the `<nav>`.
1. From the *smartphone break-point*, make disappear the former menu and show
   the `<div class="burger">` to the right of the page (in place of the menu).
3. Implement the second menu with the following characteristics:

   * Its content is

     ```html
     <div class="burger">
       <img src="images/burger.png" alt="burger" width="50px">
       <div id="menu2">
         <div><a href="./index.html">Accueil</a></div>
         <div><a href="./facts.html">Facts</a></div>
         <div><a href="./news.html">Actualités</a></div>
         <div><a href="./contact.html">Contact</a></div>
      </div>
     </div>
     ```

    * It is positioned with respect to the display window, on the upper right
      corner : What value of `position` should you use ?
	* it takes `80%` of the width of the display screen and `100%` of its height
      (look for the units `vh` and `vw` on the Web [^somesamplefootnote])
    * it should display in front of the other elements of the webpage (look for
      `z-index` on the Web)
	* the submenus are arranged vertically (one on the top of the other).

1. Hide by default the `menu2` using CSS. When the mouse is over `<div
   class="burger">`, show it again.
1. (Optional) Change the way to hide `menu2` : In the same way that
   [http://codepen.io/gungorbudak/pen/XbazEX](http://codepen.io/gungorbudak/pen/XbazEX),
   hide the menu by shifting it to its right with the property
   `margin-left`. Add a transition on the margin-left (ohhhh! it's beautiful!)

</div>

**Note :** The `hover` on submenus makes no sense on smartphones since there is
  no mouse. You will have to handle the click using JavaScript and we will see
  it next semester.

### Mobility in general

The constraints related to mobility are not confined to responsive design. To
give you a complete idea, here are other examples of constraints:

 * throughput of the network
 * limited capabilities of the media (processor, RAM,...)
 * offline mode (if you go under a bridge)
 * change in the paradigm of the human-machine interface (mouse over, drop-down
   menu,... )
