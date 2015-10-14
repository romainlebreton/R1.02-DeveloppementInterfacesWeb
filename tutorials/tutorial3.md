---
title: TD3 &ndash; HTML / CSS avancé 2/2
subtitle: display property and Layout
layout: tutorial
---

## Display 

À chaque élément HTML d'un page lui correspond une boîte ([voir la section sur le modèle de boîte du TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#le-modle-de-boite)).
La façon dont cette boîte va occuper l'espace est gérée par l'attribut display.
Nous allons voir dans cette partie les trois valeurs principales de la propriété display.


### block

Les éléments block sont des éléments :

 * dont on peut définir la taille en css via les propriétés `height` et `width`.
 * qui par défaut occupe toute la largeur (si l'on n'a pas précisé de `height`) de son parent,
 * provoque un saut de ligne avant et après son affichage (que l'on est diminué sa largeur ou pas)


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

 1. dans du texte, pour ajouter de la sémantique sans couper la lecture du lecteur (mettre en exposant un nombre par `<sup>`, préciser l'importance d'une partie du texte par `<strong>`,associer un lien avec `<a>`),
 1. lorsque l'on veut positionner des éléments à la suite.


Puisque associé au texte (`<strong>`, `<a>`, ...), on trouve en majorité les éléments `inline` comme feuilles de l'arborescence du HTML.

### règle d'inclusion des éléments `inline` et `block` du point de vue du HTML et du CSS 

[^somesamplefootnote]: En fait le HTML5 permet cette inclusion dans [certains cas](http://html5doctor.com/block-level-links-in-html-5/).

Inclure des éléments `block` dans des éléments `inline` n'est pas conforme en HTML [^somesamplefootnote], mais cela l'est du point du vue du CSS.
En modifiant la propriété `display` d'un élément, nous pouvons donc inclure des éléments `block` dans des éléments `inline`. Mais modifier sempiternellement le `display` naturel du HTML signifie que l'on n'a pas utilisé la bonne méthode (et que le code risque d'être incompréhensible). Nous nous imposons donc de respecter la règle HTML.


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

 1. puisque `<nav>` est de type `block`, nous pouvons fixer ses dimensions. Donnez-lui la hauteur `50px`,

 1. Encapsuler vos liens `<a>` par des `<div>`, que constatez-vous ?

 1. Utiliser la propriété `display` sur ces `<div>` de manière à remettre la navigation en ligne.


Conserver ces `<div>` dans la navigation avec la propriété `display` pour les mettre en ligne.
Même s'ils ne semblent pas servir à grand-chose pour l'instant.

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


La valeur `none` enlève complètement du rendu. L'élément en le sortant du flux, il ne laisse donc pas d'espace manquant à son emplacement.


<div class="exercise">

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



1. positionner ces menus en dessous des éléments qui leur correspondent (vous aurez besoin d'utiliser l'attribut `position` vu [dans le TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#position))

1. masquer ces menus par défaut en css.
1. rendez le premier menu (repsectivement le deuxième) `inline` lorsque la souris passe au-dessus de accueil (resp contact) en css.

</div>

À ce stade les sous menus apparaissent bien lorsque l'on survole les éléments "accueil" et "contact". Par contre il n'est pas possible d'entrer dans ces sous menus. 
Nous consacrons toute la prochaine section à une autre valeur de display : `flex`. L'utilisation de cette dernière va permettre d'améliorer notre menu et remédier à ce problème d'accessibilité.

## flex

La valeur de display `flex` appliquée à un élément influence plus le comportement de ses enfants que l'élément lui-même. Lorsque le display est `flex`, on peut utiliser un ensemble de propriétés spécifiques pour par exemple fixer le sens de rendu des enfants, l'espace entre ces derniers, etc... 
Nous précisons par la suite quelque-unes de ces contraintes/propriétés.

### flex-direction

La propriété `flex-direction` permet de préciser si les enfants vont se mettre en ligne ou en colonne et dans quel sens. Ses valeurs sont  :

 * `row`
 * `row-reverse`
 * `column`
 * `column-reverse`

L'attribut `flex-direction` s'appliquant aux enfants, il rentre en conflit avec les valeurs de display `block` ou `inline` de ces derniers.
L'exercice suivant va nous permettre entre autre de savoir qui surcharge l'autre en cas de conflit.


<div class="exercise" >
 1. Donner à l'élément `<nav>` la valeur de display `flex`.
 1. Changer la valeur du display des `<div>` directement enfant de `<nav>` en `block` puis en `inline`. Que cela change-t-il ?
 1. donner à l'élément `<nav>` la valeur de flex-direction:column, que cela change-t-il ? (sachant que la valeur de flex-direction est `row` supprimer cette propriété, et supprimer le display aux div enfants puisqu'ils ne servent plus à grand chose)
</div>


### align-items

La propriété `align-items` permet de préciser comment les enfants vont venir occuper l'espace perpendiculaire à la direction donnée par `flex-direction`.
Dans notre cas (`flex-direction:row`), `align-items` va donc nous permettre de préciser comment occuper l'espace vertical des `<div>` contenus dans le `<nav>`.

<div class="exercise" >

1. Centrer les éléments enfants à l'aide de la propriété align-items. Que constatez-vous ?
Si rien de ne se passe utiliser l'inspecteur du navigateur pour comprendre ce qui est centré.

1. utilisez maintenant la valeur `stretch`. Que constatez-vous à propos de l'accessibilité des sous menus avec la souris ?

1. Comment faire pour que les sous-menus restent accessibles et que les textes "Accueil" et "Contact" soient centrés dans la barre de navigation ? (les enfants n'héritent pas de la propriété flex de leur parent par défaut...)
</div>

### justify-content

Elle permet de préciser la façon dont les enfants vont se disposer dans la direction donnée par `flex-direction`.

Les valeurs possibles sont :

 * `flex_start`
 * `flex_end`
 * `center`
 * `space-between`
 * `space-around`

<div class="exercise" >

Placer les éléments de navigation non pas en début de ligne (valeur par défaut) mais en fin.

</div>


### flex, une valeur relativement rescente

Si ces dernières possibilités offertes par `flex` semblent triviales voire naturelles pour le néophyte, elles représentent en pratique une avancée majeure dans le monde du CSS. Avant flex, certains propriétés relevés jusque-là d'une expertise véritable reposant sur l'intégrateur (exemple : le centrage vertical), ou été même confiné dans le domaine du fantasme (les justifications, le comportement des éléments sur l'espace restant,...'). 


Aujourd'hui flex est bien implémenté dans [les différents navigateurs](http://caniuse.com/#search=flexbox). 
Il le sera encore plus lorsque vous entrerez dans le monde professionel (et si vous êtes amenés à faire du HTML).
Nous ne vous présenterons donc pas d'autres valeurs de display, car elles sont devenues inutiles (`display:inline-block`) ou ont toujours été merdiques (`display:table`).


Il y a d'autres valeurs intéressantes autour de flex, la référence suivante est très instructive :
https://css-tricks.com/snippets/css/a-guide-to-flexbox/



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


## Ordre d'application des sélecteurs CSS.

Il a plusieurs emplacements possible pour déclarer du style CSS.
Nous commençons par préciser ces dernières et donner leur ordre de priorité.

### priorité du style par emplacement.
Nous avons utilisé un ficher de style externe styles.css pour ajouter des règles CSS.
Il est aussi possible d'ajouter du CSS directement dans le HTML via l'attribut `style` (on parle de style "inline" à ne pas confondre avec un élément de valeur de display `inline`) :

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

Afin de savoir la couleur qui sera appliquée sur les éléments `<div>` ayant la classe toto, des priorités sont définies sur les sélecteurs CSS.

Cette valeur (a,b,c,d) de priorité est définie comme suit :

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
Vérifier bien que les ordres suivants vous semblent normaux :

~~~
 cssprior(.titi span ) >= cssprior(div span)
 cssprior( nav.titi .tata div div div div div  > ul li div.toto) 
    <= cssprior(#truc)
 cssprior(div > a) == cssprior(div + a)
~~~
{:.html}



Si deux règles ont la même priorité, alors c'est l'emplacement de leurs déclarations (inline, ficher externe, style interne, style par défaut) qui prévaut 
et si les deux règles sont dans le même emplacement, alors c'est la dernière déclaration qui l'emporte.


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


## Cacher ou Enlever un élément du rendu

Il existe plusieurs façons de faire disparaitre de l'écran un élément HTML : 

 * display:none 
 * visibility:hidden

Nous avons déjà utiliser la propriété display:none dans le menu pour cacher un menu qui ne venait pas s'intercaler dans le flow. 
Voyons un usage de visibility:hidden :

<div class="exercise">

1. Nous voulons marquer visuellement le menu sous la souris par une petite puce sur le `<div>` fils de `<nav>`. Elle se positionne à gauche de l'intitulé "accueil" ou "contact".
nous ne voulons pas que son apparition déplace le texte contenu dans accueil ni dans contact et perturbe l'utilisateur.

</div>
