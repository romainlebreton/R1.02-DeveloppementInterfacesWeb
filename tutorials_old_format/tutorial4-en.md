---
title: TD4 - Forms
subtitle: How to send data between webpages
layout: tutorial
lang: en
---

## Introduction

We are going to add a registration form to our site of fans of **Chuck Norris**
using the `<form>` tag. This `<form>` tag will allow us to have answers to
questions from the most open questions ("*What do you want to say to Chuck?*")
to the more closed-ended questions ("*Among these three choices what is your
favorite sport?*", "*What is your gender?*" ... ). For each type of question,
there is a corresponding tag such as `<input>` or `<textarea>` as we will see.

## The tags `<form>` and `<input>`

The heart of the form consists of two types of tags: `<form>` and `<input>`.

The tag `<form>` must englobe all the form related tags. Its attributes also
contain many important information about the form:

* `method`: Forms contain data (mostly typed by the user) that must be sent to
  another page to be processed. The values of the `method` attribute (`post` or
  `get`) tells the form how it will send the data to the processing webpage:

  * `get` sends data through the URL with a syntax like
    `index.html?name=Dupont&login=dupo`. This method limits the size of the data
    sent by the form to about 2000 characters.

  * `post` sends data together with the HTTP request and has no size limitation.

  More information about these methods in next year's PHP course.

* `action`: URL of the webpage to which we will send the data of the form.

The `<input>` tag allows you to define different fields in which the user can
enter data. The `<input>` tag has attributes:

* [`type`](http://www.w3schools.com/tags/att_input_type.asp): defines the
  visual appearance of the field and the nature of the data that can be entered.
* [`name`](http://www.w3schools.com/tags/att_input_name.asp): the variable name
  of the data filled in this `<input>`. In our previous example of
  `method="get"`, the form had two `<input>` of name `name` and `login`.
* [`value`](http://www.w3schools.com/tags/att_input_value.asp) (optional):
  Default value of the `<input>`, that is to say that the `<input>` will be
  prefilled with this value.

Every form must contain a tag `<input type="submit">`: this tag creates the
*Submit* button that will trigger the sending of data when clicked on.

<div class="exercise-en" id="start">

Let us see by ourselves how the value of an `<input>` is sent by a form.

1. Create a new webpage `inscription.html` in the Chuck Norris website. This page
   will contain the inscription form to Chuck Norris' fan-club.

   **Tip:** Do not forget to start every HTML webpage with the html basic
   structure seen in [tutorial 2]({{site.baseurl}}/tutorials/tutorial2-en.html).

1. Add to `inscription.html` the following form:

   ```html
   <form action="sendToMySecondYearInIut.php" method="get">
     <input name="user_name" type="text" >
     <input type="submit" value="Envoyer">
   </form>
   ```
  
1. Click on the *Submit* button and look at the URL in the address bar. Clicking
    on this button should send you to a page finishing by
    `sendToMySecondYearInIut.php?user_name=dupont`.

   **Note**: it's normal that the URL `sendToMySecondYearInIut.php` does not
   exist and that you see the famous **404** error. We will see next year how to
   write server-side scripts (in PHP) to process the form data.

</div>



## The tag `<label>`

It would be nice to tell the user what our `<input>` field refers to. The
[`<label>` tag](http://www.w3schools.com/tags/tag_label.asp) will associate the
question ("*Name ?*") to the `<input>`. The `for` attribute of the `<label>`
must contain the identifier (attribute `id`) of the associated `<input>` (so you
must add this identifier). When the label is correctly filled, a click on the
label will place the keyboard prompt in the corresponding `<input>` (try it!).

<div class="exercise-en" id="exlabel">

1. Replace the first `<input>` by the following code:

   ```html
   <label for="surname">Nom</label>
   <input id="surname" name="user_name" type="text">
   ```

1. Add to this form an input for typing the first name. Verify that clicking on
   the label works.

1. Verify that both fields are in the URL when you click on the *Submit* button
    (the URL must end with
    `sendToMySecondYearInIut.php?user_name=dupont&firstname=super` if the form
    is still in `method="get"`).

1. The inputs appear on the same line. Which tag seen in last tutorial can you
   use to englobe the inputs so that you have a line break between the two
   lines?

</div>

## The main types of `<input>` tags

There are quite a number of types of `<input>`:

 * The `radio` type allows you to select only one of the possible options.
 * The `checkbox` type allows the user to select as many options as he wants.
 * The `password` type automatically hides the characters that are typed in.
 * The types `email`, `URL`, `tel`, `date`, `time` and `number` allow you to
   adapt the virtual keyboard when the page is displayed on a
   smartphone. Depending on the browser, a different layout may be associated.
   Validators are associated with these fields (as we will see later), for
   example, an `email` field value must contain an "@".
 
<div class="exercise-en" id="exinput">
 
 With the help of [w3schools](http://www.w3schools.com/tags/att_input_type.asp),
 add to the form the following `<input>` whose labels are:

 1. "Date de naissance" with the input type `date`.
 1. "Mot de passe" with the input type `password`.
 1. "Email" with the input type ... `email`.
 1. "Sexe" with the two values that you know. Which type should you use
    considering that users only have one gender.
 1. "Niveau en karaté" with the input type `number` ranging from 0 to 5.
 1. "Niveau d'engagement" with a choice among three values labeled "Basique (5
    €)", "Gold (15 €)" and "Tatane in your face (50 €)".
 1. "J'ai bien lu les clauses que je n'ai pas lues" associated to a `checkbox`.
 1. Make sure that every `<input>` is on a separate line.
 1. Fill and submit your form in order to check that all the inputs work ;
    verify that all input names are in the URL.
 
</div>


**Notes:** 

* Some of those input types were introduced with HTML5 and are not fully
  supported by all browsers (especially old versions of Internet Explorer). We
  recommend the website [caniuse.com](http://caniuse.com/) to check the
  compatibility of HTML features. For instance, you can see that the types
  `date` and `time` are
  [more or less compatible](http://caniuse.com/#search=date). The type `number`
  is a [bit more accepted](http://caniuse.com/#search=number). You can notice
  some changes in appearance depending on the browser you are using.

* About the password, you can notice that it is written in plain text the URL if
  you use `method="get"`. For this type of sensitive data, you should use
  `method="post"`, although it is not enough to guarantee the security of the
  data.

## The `<select>` tag

The `<select>` tag is made to display possible values in a drop-down menu. The
`<select>` tag must have a `name` attribute. The possibles options of the
`<select>` are given by `<option value="your_value">` tags, that are put inside
the `<select>`. You can group options together by using an
[`<optgroup>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Optgroup)
tag.


By default, you can only choose one of the possible
options. However, you can enable multiple values by adding the attribute
`multiple` to `<select>`: this attribute is not waiting for a value so we
usually write

```html
<select name="your_name" multiple>...</select>
```

which is equivalent to

```html 
<select name="your_name" multiple="">...</select>
```

Similarly to `<input>`, we can associate a `<label>` to the `<select>`
tag.

<div class="exercise-en" id="exlabel">

With the help of [developer.mozilla.org](https://developer.mozilla.org/fr/docs/Web/HTML/Element/select), add the following `<input>` whose labels are:

1. Add a `<select>` labeled "Pays d'origine" with possible options `U.S.A` ,
   `France`, `Allemagne`, `Chine` and `Viêt Nam` whose associated values must not
   depend on the language of the form (the `value` associated with `France` could
   be `fr` for instance). The user can select only one option. Group the options
   by continent.

1. Add another `<select>` labeled "Arts-martiaux préférés" with values "Kung
   fu", "Karaté" and "Full-contact". The user is allowed to select multiple
   values.

</div>

## The `<textarea>` tag


The
[`<textarea>` tag](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Textarea)
proposes a large textbox so that the users can express themselves.

<div class="exercise-en" id="exlabel">

1. Add a large text box labeled "Message pour Chuck" on which the user can pour
   his heart out.

</div>

## The `<fieldset>` tag

The `<fieldset>` tag is used to regroup different `<input>` together.


<div class="exercise-en" id="exfield">

With the help of
[this page](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Fieldset) and
[this page](https://developer.mozilla.org/fr/docs/Web/Guide/HTML/Formulaires/Comment_structurer_un_formulaire_HTML),
regroup our inputs inside the three following groups:

* "Informations personnelles" (containing "Nom", "Prénom", "Email", etc.),
* "Les sports de combat" (containing "Sport de combat préféré"" and "Niveau en
  karaté"),
* "Inscription" (containing "Message personnel à Chuck", "Mot de passe", the
  checkbox "J'ai bien lu..", "Niveau d'engagement', etc.).

</div>


## Ergonomics and user-friendliness

### Navigation

For advanced users, navigation using the key `Tab` allows browsing very quickly
the form. The attribute `autofocus` allows to specifying what element of the form
must have the focus when the page is loaded. The attribute `tabindex` specifies
the order of elements when pressing the key `Tab`.

<div class="exercise-en" id="extab">

Verify that you can access all the inputs using the key `Tab`. Change the
order with the property `tabindex`.

</div>


### User-friendliness

A few attributes improve the user-friendliness of the fields in your form:

* `placeholder`: display some text in the field that disappears as soon as the
  user types in something. You should use the placeholder to give information
  about the expected content. For instance, if you have specified a pattern (see
  later), you should explain it with the placeholder.

  Example:  `placeholder=“Entrez votre nom ici"`

* `checked` / `selected`: for inputs of type “radio” or “checkbox”, and for
  `<option>` respectively. This attribute is used to select/check an option by
  default. Useful when you know that one of the options will be used much more
  frequently than the others. You then save time for the user.

<div class="exercise-en" >

 1. Add a placeholder of value “yourmail@domain.com” in the input of type `email`.
 1. Add a `placeholder` attribute in the `<textarea>` saying "Un inscrit sera
    tiré au sort, et verra son message transmis à Chuck Norris."
 1. Make sure that the country selected by default in "Pays d'origine" is France
	(regardless of the order of `<option>` tags in HTML).

</div>

### Content validation

The data that the user types in has to be checked by the server (cf. next year
course). However, checks by the server require that the data is sent, that the
server tests, then responds: the operation may be long.

In order to avoid a useless wait to users of your form, you can ask the browser
to directly perform certain validation tests, in order to prevent the common
errors (ex: Bad phone number, Bad date...).

Two attributes allow you to check the content of the form:

* `required`: Specifies that the field must be completed. We commonly indicate
  required inputs to the user with a * in the label.
* `pattern`: attribute specific to open answers, `pattern` let you specify
  [a regular expression](http://www.rexegg.com/). This string obeys
  [a particular syntax](http://www.rexegg.com/regex-quickstart.html#ref) and
  indicates to the browser which entries of the input are valid. The browser will
  refuse to send the form as long as some input is invalid.

  Example: The pattern `0[1-9](\.\d{2}){4}` validates french phone numbers,
  while the pattern `[a-z0-9._-]+@[a-z0-9.-]+\.[a-z]{2,4}` will block the most
  obvious email address mistakes. You can find a large variety of patterns
  examples at [HTML5pattern](http://html5pattern.com/).  
  **Note:** HTML pattern test if the whole input is valid. So there is no need
  to use `^` and `$` as in classic regular expressions.

<div class="exercise-en" id="regulex" >
 1. Make the checkmark "J'ai bien lu les clauses que je n'ai pas lues"
    mandatory. Check if the form is not sent while this box is not checked
 1. Make the inputs "Nom", "Mot de passe" and "Email" mandatory.
 1. By convention, the names of mandatory fields are followed by a `*`. Add it.
 1. Add a pattern to the input of type password so that only characters of the
    Latin alphabet or digits are allowed.
 1. Make sure that the password is at least 8 characters long.

 **Note:** To prevent bugs while writing regular expressions, always use
   [Regulex](https://jex.im/regulex) while developing a regular
   expression. Regulex will help you to visualize the state machine behind the
   regular expression.

</div>


