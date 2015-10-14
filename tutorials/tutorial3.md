---
title: TD3 &ndash; HTML / CSS avancé 2/2
subtitle: display et mise-en-page
layout: tutorial
---


## Ordre d'application des sélecteurs CSS.

Comme vous vous en souvenez, les sélecteurs servent à sélectionner un ensemble de
balises sur lesquels on applique une règle CSS. Nous avons appris lors du
[TD1 les sélecteurs de base](tutorial1_2.html#les-slecteurs-css-de-base) et lors
du
[TD2 la combinaison de sélecteurs](tutorial2.html#rgles-de-compositions-des-css).
Plusieurs règles CSS peuvent porter sur un même élément HTML. Si ces règles peuvent coexister, elles sont toutes appliquées.
Mais il peut aussi arriver que ces dernières soient contradictoires. 

Par exemple, si vous avez dans votre fichier CSS le code suivant : 

~~~
div    { color:blue; }
.skill { color:red; }
~~~
{:.css}

de quelle sera la couleur du texte d'un `<div>` de classe `skill` ?

Pour régler ces conflits, le CSS définit une notion de priorité basée sur
l'emplacement des règles CSS puis sur la spécificité des sélecteurs CSS.

### Différents emplacements

En fait, il y a plusieurs emplacements possibles pour déclarer du style CSS :

1. **Style externe** : (Conseillé) On peut utiliser un fichier de style externe et le lier au
document HTML avec la balise suivante dans le `<head>` :

   ~~~
   <link rel="stylesheet" type="text/css" href="css/styles.css">
   ~~~
   {:.html}

1. **Style interne** : (Déconseillé) On peut inclure des règles CSS directement dans
   le `<head>` à l'aide de la balise `<style>` :

   ~~~
   <html>
     <head>
       <style type="text/css">
         p {font-size: 12pt; color: pink}
       </style>
     </head>
     <body> ... </body>
   </html>
   ~~~
   {:.html}

1. **Style inline** : (Déconseillé) On peut inclure du style CSS directement
   dans une balise avec l'attribut `style` :
 
   ~~~
   <p style="font-size: 12pt; color: fuchsia">
      Aren't style sheets wonderful?
   </p>
   ~~~
   {:.html}

   Attention à ne pas confondre le style "inline" avec le futur
   `display:inline`.

Enfin les navigateurs appliquent un style par défaut sur les éléments. Cela
permet de ne pas avoir à définir pour chaque balise tout le style qui doit lui
être associé. On peut observer ce style par défaut dans les outils de
développement de Chrome.

Pour prendre de bonnes habitudes, on préférera les styles externes comme
"styles.css", qui respectent mieux la distinction entre la structure HTML et le
style CSS.


### Priorité des sélecteurs


Des règles CSS rentrent inévitablement en conflit sur certains éléments :

~~~
div {color: yellow;}
div.toto {color: red;}
~~~
{:.css}

Afin de savoir la couleur qui sera appliquée sur les éléments `<div
class="toto">`, des priorités sont définies sur les sélecteurs CSS.  Comme le
sélecteur `div.toto` est plus spécifique que le sélecteur `div`, on va appliquer
en priorité la règle `color:red;`.

Cette valeur *(a,b,c,d)* de priorité d'un sélecteur CSS est définie comme suit :

* la valeur *a* code la priorité basée sur l'emplacement de la règle. Par ordre
de priorité décroissante, nous avons
   * *a*=2, les styles inline,
   * *a*=1, les styles externes et internes,
   * *a*=0, le style par défaut du navigateur.
 * soit *b* est le nombre de sélecteur d'identifiant (`#`),
 * soit *c* est le nombre de classes (`.`) ou pseudo-classes
   (`:over`,`:visited`,...) <!-- et sélecteur d'attribut -->
 * soit *d* est le nombre d'élément contenu dans le sélecteur (`div` , `span`,
   `p`, ...) <!-- et pseudo-éléments -->
   * les opérateurs de combinaison ne contribuent pas à la priorité <!-- ni le sélecteur universel -->

Pour revenir à l'exemple précédent, les règles ont donc comme priorité  :

~~~
 div -> (0,0,0,1) (un élément div)
 div.toto -> (0,0,1,1) (une classe toto et un élément div)
~~~
{:.html}

### L'ordre de priorité

L'ordre de priorité est défini comme l'ordre du dictionnaire (ordre *lexicographique*) :

* on regarde d'abord la "première lettre" *a*. Si *a* est strictement plus grand
alors la règle CSS est plus prioritaire. En cas d'égalité,
* on regarde la "deuxième lettre" *b* pour déterminer la priorité. Si *b* est
strictement plus grand (et donc *a* égal) alors la règle CSS est plus
prioritaire. En cas d'égalité sur *a* et *b*,
* on regarde la "troisième lettre" *c*. En cas d'égalité,
* on regarde la "quatrième lettre" *d*.
* **en cas d'égalité absolue**, la règle écrite en dernier est prioritaire.

Ce mécanisme de priorité s'appelle la cascade et correspond au C de CSS (Cascading Style Sheet).

**Exemple :** `div.toto` (priorité (0,0,1,1)) est plus prioritaire que `div`
(priorité (0,0,0,1)) car on a égalité sur *a* et *b* mais *c* est plus grand
pour `div.toto`.

<div class="exercise">

Dans un fichier texte ou sur papier, écrivez-les
priorités des sélecteurs suivants et classez-les du plus prioritaire au moins
prioritaire. 

~~~
 .titi span
 div span
 nav.titi .tata div div div div div
 ul li div.toto
 #id
 div > a
 div + a
~~~
{:.css}


</div>


<!-- ### le joker en cas d'impasse !important  -->

<!--  Le style inline ne peut être dépassé par les règles CSS dans notre fichier -->
<!-- styles.css.  De plus nous pourrions utiliser des CSS externes et vouloir écraser -->
<!-- certaines de ces règles pourtant très précises.  Pour cela le CSS propose la -->
<!-- règle !important : -->

<!-- ~~~  -->
<!-- div {color: yellow !important;}  -->
<!-- div.toto {color: red;}  -->
<!-- ~~~  -->
<!--  {:.css}  -->

<!-- Elle permet de rendre la règle plus prioritaire que l'ordre (a,b,c,d) de -->
<!-- n'importe quelle règle qui n'a pas le `!important`.  Nous en parlons juste pour -->
<!-- être exhaustif sur les règles de priorité : en pratique, `!important` est très -->
<!-- peu utilisé, c'est le dernier recours, -->

<!--

#id                                   (0,1,0,0)
nav.titi .tata div div div div div    (0,0,2,6)
ul li div.toto                        (0,0,1,3)
.titi span                            (0,0,1,1)
div span                              (0,0,0,2)
div > a                               (0,0,0,2)
div + a                               (0,0,0,2)

-->

## Display 

À chaque élément HTML d'un page lui correspond une boîte ([voir la section sur le modèle de boîte du TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#le-modle-de-boite)).
La façon dont cette boîte va occuper l'espace est gérée par l'attribut display.
Nous allons voir dans cette partie les trois valeurs principales de la propriété display.


### block

Les éléments block sont des éléments :

 * dont on peut définir la taille en css via les propriétés `height` et `width`.
 * qui par défaut occupe toute la largeur (si l'on n'a pas précisé de `height`) de son parent,
 * qui provoque un saut de ligne avant et après son affichage (que l'on est diminué sa largeur ou pas)


On utilise à l'usage des éléments de display `block` : 

 * dès que l'on veut expliciter l'agencement (layout) de certains éléments HTML d'une page. (exemple nous voulons que l'en-tête (header) ait une hauteur de `200px`, nous voulons 
 qu'un paragraphe prenne `50%` de la largeur,...).
 * dès qu'il est naturel de prendre toute la place par défaut (exemple un titre `<h2>`).
 

### inline

Les éléments inline sont des éléments :

 * dont on ne peut pas définir la taille en css via les propriétés `height` et `width`,
 * qui prennent leur taille en fonction de leur contenu,
 * qui ne provoquent pas un saut de ligne.


On utilise à l'usage des éléments de display `inline` : 

 1. dans du texte, pour ajouter de la sémantique sans interrompre la lecture du lecteur (mettre en exposant un nombre par `<sup>`, préciser l'importance d'une partie du texte par `<strong>`,associer un lien avec `<a>`),
 1. lorsque l'on veut positionner des éléments à la suite.


Puisque associé au texte (`<strong>`, `<a>`, ...), on trouve en majorité les éléments `inline` comme feuilles de l'arborescence du HTML.

### règle d'inclusion des éléments `inline` et `block` du point de vue du HTML et du CSS 

[^somesamplefootnote]: En fait le HTML5 permet cette inclusion dans [certains cas](http://html5doctor.com/block-level-links-in-html-5/).

Inclure des éléments `block` dans des éléments `inline` n'est pas conforme en
HTML [^somesamplefootnote], mais cela l'est du point du vue du CSS.  En
modifiant la propriété `display` d'un élément, nous pouvons donc inclure des
éléments `block` dans des éléments `inline`. Mais modifier sempiternellement le
`display` naturel du HTML signifie que l'on n'a pas utilisé la bonne méthode (et
que le code risque d'être incompréhensible). Nous nous imposons donc de
respecter la règle HTML.

Nous allons mettre en page le menu de navigation de notre site de plusieurs façons différentes.


<div class="exercise">

Dans ce premier exercice, nous allons créer un menu dans un style "block".



1. Changer le menu de votre site par le suivant

   ~~~
   <nav>
   	<div><a href="./index.html">Accueil</a></div>
   	<div><a href="./facts.html">Facts</a></div>
   	<div><a href="./news.html">Actualités</a></div>
   	<div><a href="./contact.html">Contact</a></div>
   </nav>
   ~~~
   {:.html}

1. puisque `<nav>` est de type `block`, nous pouvons fixer ses
dimensions. Donnez-lui la largeur `50%`. Que constatez-vous ? Explication : la largeur en pourcentage est relative à la taille de la boîte de
 contenu du parent (du 1er parent en display:block). Quelle est cette boîte ?
 quel est sa largeur ? vérifiez que la largeur est bien de 50%.
1. Rajoutez des règles CSS pour que les fils `<div>` aient une couleur de fond `#5BBDBF`,
1. Ajouter une règle CSS pour que les éléments `<a>` aient la couleur de fond `#7F8C8D`.
1. Pour centrer le nav dans son parent header, on va lui donner des marges horizontales `auto` (garder marges verticales 0)
</div>


<div class="exercise">

Nouvelle mise en page en `inline` cette fois-ci.

1. Donner au nav la hauteurn `50px`,
1. Donnez aux `<div>` enfants de `<nav>` le display `inline`.
1. Vous constatez des espaces entre les entrées du menu, ces derniers sont du au espaces dans le HTML, conservé lorsque les éléments sont `inline`.
Solution : pour supprimer les espaces changer le code des `<div>` enfant de la balise `<nav>` en mettant des commentaires :

   ~~~
   <nav>
   	<div><a href="./index.html">Accueil</a></div><!--
   	--><div><a href="./facts.html">Facts</a></div><!--
   	.....
   	--><div><a href="./contact.html">Contact</a></div>
   </nav>
   ~~~
   {:.html}

1. (Optionnel) Ajouter du padding horizontal de `10px` sur les éléments `<a>`.
1. (Optionnel) Ajoutez à ces mêmes éléments `<a>` une bordure sur la gauche de `2px` de style `solid` et de couleur noire.
1. (Optionnel) Enlevez la bordure sur le premier de ces éléments.

</div>



### none

La valeur `display:none` enlève complètement du rendu. L'élément en le sortant
du flux, il ne laisse donc pas d'espace manquant à son emplacement.


<div class="exercise">

1. ajouter des sous-menus aux éléments de la navigation (frères des liens `<a>`) dont le contenu est :

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



1. Positionnez ces menus en dessous des éléments qui leur correspondent (vous
   aurez besoin d'utiliser l'attribut `position` vu
   [dans le TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#position))

1. Donnez leurs la couleur de fond `#aca, puis masquer ces menus par défaut en css. 
1. Réaffichez le premier sous-menu (resp. le deuxième) avec `display:block`
   lorsque la souris passe au-dessus de "accueil" (resp. "contact") en css.

</div>

À ce stade les sous-menus apparaissent bien lorsque l'on survole les éléments
"accueil" et "contact". Par contre il n'est pas possible d'entrer dans ces sous-menus.  Nous consacrons toute la prochaine section à une autre valeur de
display : `flex`. L'utilisation de cette dernière va permettre d'améliorer notre
menu et remédier à ce problème d'accessibilité.

## La valeur de display flex

Appliquée à un élément, la valeur de display `flex` va permettre de modifier la disposition <strong>de ses enfants</strong>. C'est donc une différence fondamentale avec les valeurs `block` et `inline`, qui eux avaient un impact directement <strong>sur l'élément lui-même</strong>. 

Lorsque le display est `flex`, on peut par exemple :

 * fixer le sens de rendu des enfants, 
 * l'espace entre ces derniers, 
 * leurs centrages dans les différentes directions,
 * modifier leurs ordres d'apparition,
 * etc. 

Nous précisons par la suite quelques-unes de ces contraintes/propriétés.

### flex-direction

La propriété `flex-direction` permet de préciser si les enfants vont se mettre en ligne ou en colonne et dans quel sens. Ses valeurs sont  :

 * `row`
 * `row-reverse`
 * `column`
 * `column-reverse`

L'attribut `flex-direction` s'appliquant aux enfants, il rentre en conflit avec les valeurs de display `block` ou `inline` de ces derniers.
L'exercice suivant va nous permettre entre autres de savoir qui surcharge l'autre en cas de conflit.


<div class="exercise" >
 1. Donnez à l'élément `<nav>` la valeur de display `flex`.
 1. Changez la valeur du display des `<div>` directement enfants de `<nav>` en `block` puis en `inline`. Que cela change-t-il ?
 1. Donnez à l'élément `<nav>` le bloc de déclaration `flex-direction:column`, que cela change-t-il ? 
 1. Remettez la direction dans sa valeur par défaut, `row`.
</div>


### align-items


La propriété `align-items` permet de préciser comment les enfants vont venir occuper l'espace perpendiculairement à la direction donnée par `flex-direction`. Dans notre cas (`flex-direction:row`), `align-items` va donc nous permettre de préciser comment occuper l'espace vertical des `<div>` contenus dans le `<nav>`.


Ses valeurs sont  :

 * `stretch`
 * `center`
 * `baseline`
 * `flex-start`
 * `flex-end`


<div class="exercise" >

1. Centrez les éléments enfants à l'aide de la propriété align-items. Que constatez-vous ?
Si rien de ne se passe utiliser l'inspecteur du navigateur pour comprendre ce qui est centré.

1. Utilisez maintenant la valeur `stretch`. Que constatez-vous à propos de l'accessibilité des sous-menus avec la souris ?

1. Comment faire pour que les sous-menus restent accessibles et que les textes "Accueil" et "Contact" soient centrés dans la barre de navigation ? (les enfants n'héritent pas de la propriété flex de leur parent par défaut, il faudra donc peut-être donner cette valeur de display à d'autres éléments...)
</div>

### justify-content

Cette propriété permet de préciser la façon dont les enfants vont se disposer dans la direction donnée par `flex-direction`.

Les valeurs possibles sont :

 * `flex_start`
 * `flex_end`
 * `center`
 * `space-between`
 * `space-around`

<div class="exercise" >

 1. Placez les éléments de navigation non pas en début de ligne (valeur par défaut) mais en fin.
 1. Placez la citation et la navigation sur le même plan (toujours avec votre display favoris)
 1. Repositionnez le menu pour qu'il soit en bas de la balise `<header>`.
</div>

### flex, une valeur relativement récente

Si ces dernières possibilités offertes par `flex` semblent triviales voire naturelles pour le néophyte, elles représentent en pratique une avancée majeure dans le monde du CSS. Avant flex, certaines propriétés relevés jusque-là d'une expertise véritable de l'intégrateur (exemple : le centrage vertical), ou été même confiné dans le domaine du fantasme (les justifications, le comportement des éléments sur l'espace restant, etc.). 

Aujourd'hui flex est bien implémenté dans [les différents navigateurs](http://caniuse.com/#search=flexbox). 
Nous ne vous présenterons donc pas d'autres valeurs de display, car elles sont devenues inutiles (`display:inline-block`) ou ont toujours été techniquement merdiques (`display:table`).

Il y a d'autres propriétés intéressantes autour de flex, la référence suivante est très instructive :
https://css-tricks.com/snippets/css/a-guide-to-flexbox/

## Two columns layout

Il est temps d'avoir un layout (aménagement de l'espace) pour notre site.

<div class="exercise" > 
 1. Donnez au body la `width` de `900px`.
 1. Déplacez dans le HTML la table comparative de `<aside>` vers `<article>` 
 1. Utilisez la valeur de display `flex` sur la balise `<main>`, et comme pour la navigation mettez ses enfants `<article>` et `<aside>` en colonne.
 1. Fixez la largeur de `<article>` à `60%`, et celle de `<aside>` à `30%`. Ce dernier élément aura une marge gauche de `10%`.
 1. Donnez à `<aside>` la couleur de fond `#CCC` et à `<article>` la couleur de fond `#731373`.

 <!--
 1. Dans la page "contact", alignez l'image de Chuck avec l'adresse de contact.
 1. Donnez à l'image la hauteur de `300px`, centrez le texte verticalement.
-->
</div>


## Fini !

Le mot de la fin à propos de flex ? 

<blockquote> 

Moi je stoppe sur mon flex.
Quand je sticks ma vibes le dancefloor se breaks et se fluxe dans la vibes

<cite>Gad Elmaleh</cite>
</blockquote>



<!--
## Cacher ou Enlever un élément du rendu

<span class="puce">■</span>

Il existe plusieurs façons de faire disparaitre de l'écran un élément HTML : 

 * display:none 
 * visibility:hidden

Nous avons déjà utiliser la propriété display:none dans le menu pour cacher un menu qui ne venait pas s'intercaler dans le flow. 
Voyons un usage de visibility:hidden :

<div class="exercise">

1. Nous voulons marquer visuellement le menu sous la souris par une petite puce sur le `<div>` fils de `<nav>`. Elle se positionne à gauche de l'intitulé "accueil" ou "contact".
nous ne voulons pas que son apparition déplace le texte contenu dans accueil ni dans contact et perturbe l'utilisateur.

</div>

-->
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

