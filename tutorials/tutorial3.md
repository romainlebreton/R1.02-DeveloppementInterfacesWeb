---
title: TD3 &ndash; HTML / CSS avancé 2/2
subtitle: display property and Layout
layout: tutorial
---

## Display 

A chaque élément HTML d'un page lui correspond une boite [dans le TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#le-modle-de-boite).
La façon dont cette boite va occuper l'espace est gérée par l'attribut display.
Nous allons voir dans cette partie les trois valeurs principales de la propriété display.


### block

Les éléments block sont des élements :

 * dont on peut définir la taille en css via les propriétés `height` et `width`.
 * qui par défaut occupe toute la largeur (si l'on a pas précisé de `height`) de son parent,
 * provoque un saut de ligne avant et après son affichage (que l'on est diminué sa largeur ou pas)


On utilise à l'usage des éléments de display `block` : 

 * dès que l'on veut exliciter l'agencement (layout) de certains éléments HTML d'une page. (exemple nous voulons que l'en-tête (header) ait une hauteur de `200px`, nous voulons 
 qu'un paragraphe prenne 50% de la largeur,...).
 * dès qu'il est naturel de prendre toute la place par défaut (un titre `<h2>`).
 

### inline

Les éléments inline sont des élements :

 * dont on ne peut pas définir la taille en css via les propriétés `height` et `width`,
 * qui prenent leur taille en fonction de leur contenu,
 * qui ne provoque pas un saut de ligne.


On utilise à l'usage des éléments de display `inline` : 

 1. dans du texte, pour ajouter de la sémantique sans couper la lecture du lecteur (mettre en exposant `<sup>`, mettre de l'importance `<strong>`,associer un lien `<a>`),
 1. lorsque l'on veut positionner à la suite des éléments.


Puisque associé au texte (`<strong>`, `<a>`, ...), on trouve en majorité les éléments `inline` comme feuilles de l'arboresence du HTML.

### à propos de HTML et CSS 

[^somesamplefootnote]: En fait le HTML5 permet cette inclusion dans [certains cas](http://html5doctor.com/block-level-links-in-html-5/).

Inclure des éléments `block` dans des éléments `inline` n'est pas conforme en HTML [^somesamplefootnote]. Cela dit du point du vue du CSS, cela est conforme.
En modifiant la propriétée `display` d'un élément, nous pouvons donc inclure des éléments `block` dans des éléments `inline`. Mais modifier sempiternellement le `display` naturel du HTML signifie que l'on a pas utiliser la bonne méthode (et que le code risque d'être incompréhensible, immentenable). Nous nous imposons donc de respecter la règle HTML.


<div class="exercise">

Nous allons créer un menu de navigation pour notre site.
Pour l'instant le menu que vous devez avoir pour votre site est le suivant 


~~~
<nav>
	<a href="./index.html">Accueil</a>
	<a href="./contact.html">Contact</a>
</nav>
~~~
{:.html}

(Si ce n'est pas le cas remplacer le contenu de votre menu par celui-ci).

 1. puisque `<nav>` est de type `block`, nous pouvons fixer ces diemsnsions. Donnez lui la hauteur `50px`,

 1. Encapsuler vos liens `<a>` par des `<div>`, que constatez vous ?

 1. Utiliser la propriété `display` sur ces `<div>` de manière à remettre la navigation en ligne.


Conserver ces `<div>` dans la navigation avec la propriété `display` pour les mettre en ligne.
Même s'ils ne semblent pas servir à grand chose pour l'instant.

</div>




<!--

### inline-block

signifie que l'élément bénéficie du mode hybride suivant :
 
  * on peut fixer la `width` et la `height` de l'élément (hérité de `block`),
  * par défaut la taille de l'élément est définie par son contenu (hérité de `inline`),
  * l'élement reste en ligne, il n'y a pas de saut de ligne avant lui et après lui (hérité de `inline`)


Au niveau de la composition l'élément se comporte comme `block` : 

 * Un élément `inline-block` peut contenir des éléments `block` ou `inline`.
 * Un élément `inline` ne peut contenir d'élement `inline-block`.


-->


### none


La valeur `none` enlève complètment du rendu l'élément en le sortant du flux. Il ne laisse donc pas d'espace marquant sa disparition.


<div class="exercise">

1. combiner avec li:hover img, visibility:default pour liker un lien (ou un site)
1. ajouter des sous menu aux éléments de la navigation (frères des liens `<a>`) dont le contenu est :

 * pour l'ancre "Accueil" 

~~~
<div class="submenu">
	<div>one</div>
	<div>two</div>
	<div>tree</div>
</div>
~~~
{:.html}

 * pour l'ancre "Contact".

~~~
<div class="submenu">
	<div>other</div>
	<div>another</div>
</div>
~~~
{:.html}



1. positionner ces menus juste en dessous des éléments qui leurs correspondent (vous aurez besoin d'utiliser l'attribut `position` vu [dans le TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#position))

1. masquer ces menus par défaut
1. rendez le premier menu (repsectivement le deuxième) `inline` lorsque la souris passe au dessus de accueil (resp contact).

</div>

A ce stade les sous-menus apparaissent bien lorsque l'on passe sur les éléments censés les ouvrir.
Par contre il n'est pas possible d'entrer dans ces sous-menus. Nous verrons avec la propriété suivante améliorer notre menu et remédier à ce problème.

## flex

La propriété flex porte à la fois sur l'élement et ses enfants.

La propriété flex placée sur l'élement permet de positionner différentes valeurs sur ce dernier ou sur ces enfants comme autant de contraintes.
Nous précisons par la suite quelque unes de ces contraintes en se concentrant sur celles définies sur l'élément parent.



### align-items


<div class="exercise" >

1. Donner à l'élement `<nav>` la valeur de display `flex`.

1. Centrer les éléments enfants à l'aide de la propriété align-items. Que constatez vous ?
 Si rien de ne se passe utiliser l'inspecteur du navigateur pour comprendre ce qui est centré.

1. utilisez maintenant la valeur `stretch`. Que constatez vous à propos de l'accessibilité des sous menus avec la souris ?

1. Comment faire pour que le menu reste accessible et que le texte "Accueil" et "Contact" soient centrés dans la barre de navigation ? (les enfants n'héritent pas de la propriété flex de leur parent par défaut...)
</div>


### flex-direction


Elle permet de préciser si les enfants vont se mettre en ligne ou en colonne. Ses valeurs sont  :

 * `row`
 * `row-reverse`
 * `column`
 * `column-reverse`

 
 L'attribut `flex-direction` d'un élément prend le pas sur les propriétés `block` ou `inline` de ses enfants.


<div class="exercise" >
 1. Changer la valeur du display des `<div>` diretement enfant de `<nav>` en `block` puis en `inline`. Que cela change t il ?
 1. donner à l'élement `<nav>` la valeur de flex-direction:column, que cela change t'il ? (sachant que la valeur de flex-direction est `row` supprimer cette propriété)
</div>


### justify-content


La propriété `justify-content` s'applique sur l'élement. Elle permet de préciser la façon dont les enfants vont se disposer dans l'espace de leur parent.


Les valeurs possibles sont :

 * `flex_start`
 * `flex_end`
 * `center`
 * `space-between`
 * `space-around`

<div class="exercise" >

Placer les éléments de navigation non pas en début de ligne comme flex le posiotnne par défaut mais en fin.

</div>



### Les autres propriétés 

Il y a d'autres valeurs interessantes autour de flex, la référence suivante est très instructive :
https://css-tricks.com/snippets/css/a-guide-to-flexbox/


 * le comportement des boites des enfants lorsqu'il n'y a pas assez d'espace,
 * le comportement des boites des enfants lorsque la parent dispose de trop d'espace,
 * comment les éléments vont être justifier (à droite, à gauche, centrer,...),
 * de centrer les enfants horizontalement <strong>et/ou</strong> verticalement,
 * etc.

Si ces dernières possibilités offertes par `flex` semblent triviales voire naturelles, elles représentent en fait une avancée majeure dans le monde du CSS, ou ces différents aspects relevés jusque là d'une véritable expertise de la part de l'integrateur (le centrage vertical), ou même de l'ordre du fantasme (les justifications et le centrage en une simple valeur css, le comportement des éléments sur l'espace restant,...').



### une valeur relativement rescente, 

Citer can i use
Quand seriez vous sur le marché ?

Toutes ces contraintes n'ont soit pas d'équivalent dans les autres modes de display (`display:inline` ou `display:block`) , soit artificiellement absconses (`display:table`) soit entachées de cas particuliers (`display:inline-block`).



### suite des positions

menu avec position:absolute pour ne pas décaler le corps de la page

## Ordre d'application des sélecteurs CSS.


<!-- On peut aussi parler des sélecteurs de base sur les attributs -->

<!--

Rajouter référence MDN ???

Parler aussi des pseudo-éléments type ::first-letter ?
::after
::before
::first-letter
::first-line

MDN : Tout comme les pseudo-classes, les pseudo-éléments sont ajoutés aux
sélecteurs. Mais au lieu de décrire un état spécial, ils permettent de styler
certaines parties du document.

<style type="text/css">
p::first-letter { font-size:1.4em; }
</style>

-->

Il a plusieurs emplacements pour déclarer du style CSS.
Nous commençons par préciser ces dernières et donner leurs ordre de priorité.

### priorité du style par emplacement.
Nous avons utilisé un ficher de style externe styles.css pour ajouter des règles CSS.
Il est aussi possible d'ajouter du CSS directement dans le HTML via l'attribut `style` (on parle de style "inline") :

~~~
<p style="font-size: 12pt; color: fuchsia">
   Aren't style sheets wonderful?
</p>
~~~
{:.html}

Ou d'inclure des règles CSS dans une balise `<style>` (on parle de "internal style"):


~~~
<style type="text/css">
   p {font-size: 12pt; color: pink}
</style>
~~~
{:.html}

Enfin les navigateurs appliquent un style par défaut sur les éléments.
Cela permet de ne pas avoir à définir pour chaque balise tout le style qui doit lui être associé.

L'ordre de priorité d'application des règles CSS est la suivante :

1. styles 'inline' par l'attribut `style` à même le HTML,
1. styles contenu dans les fichiers CSS (external style),
1. styles définis dans une balise `<style>` dans le fichier HTML (internal style),
1. style par défaut des navigateurs.


En pratique on préférera les styles externes comme "styles.css", cela respecte mieux la césure entre la structure HTML et le style CSS. 


### Priorité des règles par leurs sélecteurs.

Des règles CSS rentrent inévitablement en conflit sur certains éléments :

~~~
div {color: yellow;}
div.toto {color: red;}
~~~
{:.css}

Afin de savoir la couleur qui sera appliquée sur les éléments `<div>` ayant la classe toto, des priorités sont définis sur les sélecteurs CSS.

Cette priorité est une valeur (a,b,c,d) définie comme suit :

 * soit a la règle est dans un style inline (voir plus haut), (a=1 si le style est inline, 0 sinon)
 * soit b est le nombre de sélecteur d'identifiant (`#`),
 * soit c est le nombre de classe (`.`) ou pseudo classe (`:over`,`:visited`,...)
 * soit d est le nombre d'élément contenu dans le sélecteur (`div` , `span`, `p`, ...)

l'ordre de priorité est défini comme lexicographique (la valeur de a est plus discriminante que b qui lui même est plus discriminant que c). 

Pour revenir à l'exemple précédent, les règles ont donc comme priorité  :

~~~
 div -> (0,0,0,1) (un élément div)
 div.toto -> (0,0,1,1) (une classe toto et un élément div)
~~~
{:.html}


Soit la fonction `cssprior` qui à un sélecteur CSS donne sa priorité `(a,b,c,d)`, 
voici quelques exemples d'ordre.
Vérifier bien que les ordres suivants vous semblent normal :

~~~
 cssprior(.titi span ) >= cssprior(div span)
 cssprior( nav.titi .tata + div div div div div  > ul li div.toto) 
    <= cssprior(#truc)
 cssprior(div > a) == cssprior(div + a)
~~~
{:.html}



C'est donc la deuxième qui sera appliquée (sur les div ayant la classe toto bien sûr).


Remarque si deux règles ont la même priorité, alors c'est l'emplacement de leurs déclaration (inline, ficher externe, style interne, style par défaut) qui prévaut 
et si les deux règles sont dans le même emplacement, alors c'est le dernier qui l'emporte.


### le joker en cas d'impasse !important 

 Le style inline ne peut être dépassé par les règles CSS dans notre fichier styles.css. 
De plus nous pourrions utiliser des CSS externes et vouloir écraser certaines de ces règles pourtant très précises. 
 Pour cela le CSS propose la règle !important : 

~~~ 
div {color: yellow !important;} 
div.toto {color: red;} 
~~~ 
 {:.css} 

Elle permet de rendre la règle plus prioritaire que l'ordre (a,b,c,d) de n'importe quelle règle qui n'a pas le `!important`. 
Nous en parlons juste pour être exhaustif sur les règles de priorité : en pratique, `!important` est très peu utilisé, c'est le dernier recours,  


## Display avancés

### inline-block

### Flexbox

https://css-tricks.com/snippets/css/a-guide-to-flexbox/


## Layout

### Column layout


### holly grail layout

Nous sommes en 2015, et jusquà peu il n'est toujours pas évident de faire ce layout (d'où son nom).

https://philipwalton.github.io/solved-by-flexbox/

## Media Object


## vertical centering


## box-model


## le model par défaut

## le border-layout



## Cacher ou Enlever un élément du rendu

Il existe plusieurs façons de faire disparaitre de l'écran un élément HTML.

### cacher display:none 

### enlever visibility:hidden
