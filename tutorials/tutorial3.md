---
title: TD3 &ndash; HTML / CSS avancé 2/2
subtitle: display et mise-en-page
layout: tutorial
---

<!--
Remarque des élèves au Jury A1 :
plus d'exemples de comment utiliser Flex
Faire des références (et aller voir) à alsacreation et W3schools (bon tuto sur internet)
Et dire clairement qu'il faut qu'ils aillent lire ces docs
-->

<!--
dans l'exercice position:absolute du sous-menu,
mettre width:100% pour le sous-menu et fixer la largeur des titres de menus
même si position absolute, width se rapporte au père
-->

## Ordre d'application des sélecteurs CSS

Comme vous vous en souvenez, les sélecteurs servent à sélectionner un ensemble
de balises sur lesquels on applique une règle CSS. Nous avons appris lors du
[TD1 les sélecteurs de base](tutorial1_2.html#les-sélecteurs-css-de-base) et lors
du
[TD2 la combinaison de sélecteurs](tutorial2.html#règles-de-compositions-des-css).

Plusieurs règles CSS peuvent porter sur un même élément HTML. Si ces règles
peuvent coexister, elles sont toutes appliquées. Par exemple, si vous avez le
code CSS suivant :

```css
div    { background-color:blue; }
.skill { color:red; }
```

alors un `<div class="skill">` aura les deux propriétés `background-color:blue`
et `color:red`.

Mais il peut aussi arriver que ces dernières soient contradictoires.  Par
exemple, si vous avez le code CSS suivant, **de quelle couleur** sera le texte
d'un `<div>` de classe `skill` ?

```css
.skill { color:red; }
div    { color:blue; }
```

Pour régler ces conflits, le CSS définit une notion de priorité basée sur
l'emplacement des règles CSS puis sur la spécificité des sélecteurs CSS. Dans
l'exemple précédent, c'est la première règle qui prévaut comme nous le verrons
dans la suite.

### Différents emplacements

Il y a plusieurs emplacements possibles pour déclarer du style CSS :

1. **Style externe** : (Conseillé) On peut utiliser un fichier de style externe et le lier au
document HTML avec la balise `<link>`  dans le `<head>` :

   ```html
   <html>
     <head>
       <link rel="stylesheet" type="text/css" href="css/styles.css">
     </head>
     <body> ... </body>
   </html>
   ```

1. **Style interne** : (Déconseillé) On peut inclure des règles CSS directement dans
   le `<head>` à l'aide de la balise `<style>` :

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

1. **Style inline** : (Fortement déconseillé) On peut inclure du style CSS directement
   dans une balise avec l'attribut `style` :
 
   ```html
   <p style="font-size: 12pt; color: fuchsia">
      Aren't style sheets wonderful?
   </p>
   ```

   Attention à ne pas confondre le style inline avec le futur `display:inline`.

Enfin les navigateurs appliquent un style par défaut sur les éléments. Cela
permet de ne pas avoir à définir à chaque fois les styles les plus
classiques. On peut observer le style par défaut dans les outils de
développement de Chrome : ce sont les règles de styles associées à *user agent
stylesheet*.

Pour prendre de bonnes habitudes, on préférera les styles externes comme
`styles.css` qui permet une séparation plus claire entre les rôles du HTML
(contenu avec des balises pour donner du sens) et du CSS (présentation / mise en
page). Comme dit
[à la fin du TD 1 partie 2]({{site.baseurl}}/tutorials/tutorial1_2.html#le-css-et-html--des-rôles-bien-distincts-et-complémentaires),
cette séparation est indispensable et très puissante :

 * Elle permet de réutiliser une présentation d'une page à l'autre. Par exemple
   quand *lemonde.fr* publie un nouvel article, il ne refait pas le style
   expressément pour ce dernier: il s'agit d'un nouveau document HTML partageant
   le même CSS que les articles précédents ;
 * Elle permet de refaire un site Web en se concentrant sur les CSS sans (trop)
   toucher au HTML ;
 * Elle permet de changer la présentation d'un document suivant s'il est destiné
   à l'impression ou à être visualisé avec un navigateur. Dans ce cas, on
   appliquera un style CSS différent selon le média.



### Priorité des sélecteurs


Reprenons l'exemple précédent :

```css
.skill { color:red; }
div    { color:blue; }
```

Afin de savoir la couleur qui sera appliquée sur les éléments `<div
class="skill">`, des priorités sont définies sur les sélecteurs CSS. Dans
l'idée, comme le sélecteur `.skill` est plus spécifique que le sélecteur `div`,
on va appliquer en priorité la règle `color:red;`.

La *priorité d'un sélecteur CSS* est une valeur *(a,b,c,d)* définie comme suit :

* la valeur *a* code la priorité basée sur l'emplacement de la règle. Par ordre
de priorité décroissante, nous avons
   * *a*=2 pour les styles inline,
   * *a*=1 pour les styles externes et internes,
   * *a*=0 pour le style par défaut du navigateur.
 * *b* compte le nombre de sélecteurs d'identifiants (e.g. `#id`),
 * *c* compte le nombre de sélecteurs de classes (e.g. `.skill`) ou pseudo-classes
   (`:hover`,`:visited`,...) <!-- et sélecteur d'attribut -->
 * *d* compte le nombre de sélecteurs de balises (e.g. `div`, `span`) ou de
   pseudo-élements (e.g. `::first-letter`, `::after`)
 * les opérateurs de combinaison et le sélecteur universel `*` ne contribuent
   pas à la priorité.

Pour revenir à l'exemple précédent, les règles ont donc comme priorité (en
supposant qu'elles sont écrites dans un fichier de style externe) :

```css
 div    /* -> (1,0,0,1) (un sélecteur de balise div)   */
 .skill /* -> (1,0,1,0) (un sélecteur de classe skill) */
```

### L'ordre de priorité

Il reste maintenant à expliquer comment on classe les priorités
(*a*,*b*,*c*,*d*). L'ordre sur les priorités est défini comme l'ordre du
dictionnaire (ordre *lexicographique*) :

* on regarde d'abord la "première lettre" *a*. Si *a* est strictement plus grand
alors la règle CSS est plus prioritaire. En cas d'égalité,
* on regarde la "deuxième lettre" *b* pour déterminer la priorité. Si *b* est
strictement plus grand (et donc *a* égal) alors la règle CSS est plus
prioritaire. En cas d'égalité sur *a* et *b*,
* on regarde la "troisième lettre" *c*. En cas d'égalité,
* on regarde la "quatrième lettre" *d*.
* **en cas d'égalité absolue**, la règle écrite en dernier est prioritaire.

Ce mécanisme de priorité s'appelle la cascade et correspond au C de CSS (Cascading Style Sheet).

**Exemple :** `div.skill` (priorité (1,0,1,1)) est plus prioritaire que `div`
(priorité (1,0,0,1)) car on a égalité sur *a* et *b* mais *c* est plus grand
pour `div.skill`.

<div class="exercise">

Dans un fichier texte ou sur papier, écrivez les priorités des sélecteurs
suivants et classez les du plus prioritaire au moins prioritaire. On supppose
que toutes ces règles sont définies dans un fichier externe, donc *a*=1, et les
valeurs recherchées commencent toujours par `(1,...)`.

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
div + a                               (1,0,0,2)
div > a                               (1,0,0,2)
div span                              (1,0,0,2)
-->

<div class="exercise"> Quelle est la couleur du texte "Priorité CSS" dans les
deux cas suivant ? Quelle règle de priorité CSS explique votre réponse ?

1. Le fichier `styles.css` contient `p {color:blue;}`, et le fichier `index.html` contient

   ```html
   <html>
     <head>
       <style type="text/css">
         p {color: pink}
       </style> 
       <link rel="stylesheet" type="text/css" href="css/styles.css">
     </head>
     <body><p style="color:red">Priorité CSS</p></body>
   </html>
   ```

1. Le même fichier `styles.css` et le fichier `index.html` sans la règle inline

   ```html
   <html>
     <head>
       <style type="text/css">
         p {color: pink}
       </style> 
       <link rel="stylesheet" type="text/css" href="css/styles.css">
     </head>
     <body><p>Priorité CSS</p></body>
   </html>
   ```

<!-- Couleur rouge puis couleur bleue -->


</div>

<!-- ### le joker en cas d'impasse !important  -->

<!--  Le style inline ne peut être dépassé par les règles CSS dans notre fichier -->
<!-- styles.css.  De plus nous pourrions utiliser des CSS externes et vouloir écraser -->
<!-- certaines de ces règles pourtant très précises.  Pour cela le CSS propose la -->
<!-- règle !important : -->

<!-- ```css
<!-- div {color: yellow !important;}  -->
<!-- div.skill {color: red;}  -->
<!-- ```

<!-- Elle permet de rendre la règle plus prioritaire que l'ordre (a,b,c,d) de -->
<!-- n'importe quelle règle qui n'a pas le `!important`.  Nous en parlons juste pour -->
<!-- être exhaustif sur les règles de priorité : en pratique, `!important` est très -->
<!-- peu utilisé, c'est le dernier recours, -->



## La propriété `display`

Comme nous l'avons vu au TD précédent, à chaque balise correspond quatre boîtes
(*content*, *padding*, *border* et *margin*,
[voir la section sur le modèle de boîte du TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#le-modèle-de-boite)).

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodel.png" style="margin:0
auto;display: block;">


La façon dont ces boîtes vont occuper l'espace est gérée par l'attribut
`display`.  Nous allons voir dans cette partie les trois valeurs principales de
la propriété `display`.


### `display:block`

Les éléments block sont des éléments :

 * qui par défaut occupent toute la largeur, <!-- (si l'on n'a pas précisé de
   `width`) de son parent, -->
 * qui provoquent un saut de ligne avant et après son affichage (que l'on ait
   diminué sa largeur ou pas)
 * dont on peut définir la taille en CSS via les propriétés `height` et `width`.

<!-- Expliquer ici le containing block et qu'on prend sa largeur ? -->

En pratique, on utilise des éléments de display `block` : 

 * dès que l'on veut expliciter l'agencement (layout) de certains éléments HTML
 d'une page. Par exemple nous voulons que l'en-tête (header) ait une hauteur de
 `200px`, qu'un paragraphe prenne `50%` de la largeur,... .
 * dès qu'il est naturel de prendre toute la place par défaut (exemple un titre
   `<h2>`).

Notez que
[les balises de structure que l'on a présentées au TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#structuration-de-la-page)
ont `display:block` comme style par défaut dans le navigateur, ce qui explique
qu'elles s'empilent verticalement comme on l'avait expliqué.

<!--
Horizontal formatting : Expliquer la content box du containing block, les
largeurs relatives % de la largeur parent, la règle des 7, auto Ne pas parler
des marges négatives

Vertical formatting :
defined height, overflow, auto=0 (pour margin ?),
pourcentage quand parent de hauteur fixée

Collapsing vertical margins : entre pères & fils, entre frères 
-->

### `display:inline`

Les éléments inline sont des éléments :

 * qui prennent leur taille en fonction de leur contenu,
 * qui ne provoquent pas un saut de ligne, ils sont écrits comme du texte les uns
   à la suite des autres
 * dont on ne peut pas définir la taille en css via les propriétés `height` et `width`,


En pratique, on utilise des éléments de display `inline` : 

 1. dans du texte, pour ajouter de la sémantique sans interrompre la lecture du
    lecteur (mettre en exposant un nombre par `<sup>`, préciser l'importance
    d'une partie du texte par `<strong>`, associer un lien avec `<a>`),
 1. lorsque l'on veut positionner des éléments à la suite.


Puisqu'associés au texte (`<strong>`, `<a>`, ...), on trouve en majorité les
éléments `inline` comme feuilles de l'arborescence du HTML.

Notez que
[les balises au niveau du texte que l'on a présentées au TD précédent]({{site.baseurl}}/tutorials/tutorial2.html#top-menu)
ont `display:inline` comme style par défaut dans le navigateur, ce qui explique
qu'elles se comportent comme du texte.

<!--
Lire Meyer
Si on est display:inline, toutes les règles de texte s'appliquent à nous : les espaces s'affichent, line-height, text-align ...
-->

### Exemple

Le code HTML suivant

```html
<p style="display:block;">display:block</p> 
<p style="display:inline;">display:inline</p> 
...
<p style="display:inline;">display:inline</p> 
<p style="display:block;">display:block</p>
<p style="display:block;">display:block</p> 
<p style="display:inline;">display:inline</p> 
```

s'affiche comme suit :

<div class="codeexample" style="padding:0;text-align:initial;"> 
<p style="display:block;background-color:#A4AFFC;border: 1px solid black;margin:0;">
display:block1
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline1
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline2
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline3
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline4
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline5
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline6
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline7
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline8
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline9
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline10
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline11
</p> 
<p style="display:block;background-color:#A4AFFC;border: 1px solid black;margin:0;">
display:block2
</p>
<p style="display:block;background-color:#A4AFFC;border: 1px solid black;margin:0;">
display:block3
</p> 
<p style="display:inline;background-color:#5EFC5E;border: 1px solid black;margin:0;">
display:inline12
</p> 
</div>

On remarque bien que les `display:block` prennent toute la largeur, avec un saut
de ligne avant et après. Tandis que les `display:inline` s'affichent les uns à
la suite des autres comme le texte d'un paragraphe. Faites varier la largeur de
la fenêtre pour voir comment l'affichage s'adapte.

**Note (optionnelle)** -- Règle d'inclusion des éléments `inline` et `block` du
point de vue du HTML et du CSS :

  [^somesamplefootnote]: En fait le HTML5 permet cette inclusion dans [certains cas](http://html5doctor.com/block-level-links-in-html-5/).
  
>   Inclure des éléments `block` dans des éléments `inline` n'est pas conforme
>   en HTML[^somesamplefootnote], mais cela l'est du point de vue du CSS.  En
>   modifiant la propriété `display` d'un élément, nous pouvons donc inclure des
>   éléments `block` dans des éléments `inline`. Mais modifier sempiternellement
>   le `display` naturel du HTML signifie que l'on n'a pas utilisé la bonne
>   méthode (et que le code risque d'être incompréhensible). Nous nous imposons
>   donc de respecter la règle HTML.

### Exercices

Nous allons mettre en page le menu de navigation de notre site en mode `block` puis en mode `inline`.

<div class="exercise">

Dans ce premier exercice, nous allons créer un menu dans un style `block`.



1. Changez le menu de votre site par le suivant

   ```html
   <nav>
   	<div><a href="./index.html">Accueil</a></div>
   	<div><a href="./facts.html">Facts</a></div>
   	<div><a href="./news.html">Actualités</a></div>
   	<div><a href="./contact.html">Contact</a></div>
   </nav>
   ```

1. Puisque `<nav>` est `display:block` par défaut (le vérifier sur Chrome si
   possible), il doit prendre toute la largeur. **Inspectez** donc votre `<nav>` pour
   voir si c'est le cas. Que constatez-vous ?

   **Explication :** En fait, un élément `display:block` ne prend pas toute la
     largeur de `<body>` mais de son plus proche `block` parent. Ici, le père de
     `<nav>` est le bloc `<header>` et donc `<nav>` prend toute la largeur de
     `<header>`.  
     Le plus proche `block` parent s'appelle le *containing block*.

1. Puisque `<nav>` est de type `block`, nous pouvons fixer ses
dimensions. Donnez-lui la largeur `75%`. Que constatez-vous ?

   **Explication :** La largeur d'une balise en `display:block`
     est relative à celle de son *containing block* (`<header>`
     ici). **Inspectez** `<header>` puis `<nav>` pour connaître leur
     largeurs. **Vérifiez** qu'on a bien un rapport de `75%`.

1. Pour centrer le `<nav>` dans son parent `<header>`, on va lui donner des
marges horizontales `auto` (gardez les marges verticales à 0).

   **Rappel :** Nous avons vu dans
   [le dernier TD comment centrer horizontalement]({{site.baseurl}}/tutorials/tutorial2.html#centrer-horizontalement-).
   Pour centrer un `display:block` dont le *containing block* est plus large, il
   faut mettre les marges horizontales en `auto` : elles se règlent alors
   automatiquement pour compléter la largeur manquante entre le `block` courant
   et le *containing block*. Ceci n'est pas valable pour les marges verticales.

1. Rajoutez des règles CSS pour que les fils `<div>` **enfants de** `<nav>`
   aient une couleur de fond `#5BBDBF`,
1. Ajoutez une règle CSS pour que les éléments `<a>` **descendants de** `<nav>`
   aient la couleur de fond `#c0d5c2`.

</div>


<div class="exercise">

Nouvelle mise en page du menu en `display:inline` cette fois-ci.

1. Donnez aux `<div>` enfants de `<nav>` le display `inline`.
1. Vous constatez des espaces entre les entrées du menu, ces derniers sont dû aux
espaces dans le HTML, qui sont affichés lorsque les éléments sont `inline`.  
   **Une solution temporaire (en attendant `display:flex`) :** pour supprimer
   les espaces, changez le code des `<div>` enfant de la balise `<nav>` en
   mettant des commentaires :

   ```html
   <nav>
   	<div><a href="./index.html">Accueil</a></div><!--
 --><div><a href="./facts.html">Facts</a></div><!--
 --><div><a href="./news.html">Actualités</a></div><!--
 --><div><a href="./contact.html">Contact</a></div>
   </nav>
   ```

1. Donnez au `<nav>` une hauteur de `50px` (`<nav>` est `block` donc on peut lui
   donner une hauteur),
1. (Optionnel) Ajoutez du padding horizontal de `10px` sur les éléments `<a>`.
1. (Optionnel) Ajoutez à ces mêmes éléments `<a>` une bordure sur la gauche de `2px` de style `solid` et de couleur noire.
1. (Optionnel) Enlevez la bordure sur le premier de ces éléments.  
   **Astuce :** Il faut utiliser une pseudo-classe vue
     [au TD dernier]({{site.baseurl}}/tutorials/tutorial2.html#pseudo-classes).

</div>

## `display:none`

La valeur `display:none` enlève complètement un élément du rendu, sans laisser
d'espace à l'endroit où il aurait dû être. Nous allons coder en exercice un menu
déroulant.

### Menu déroulant : Partie 1 -- positionnement

Dans un premier temps, nous
allons juste positionner les sous-menus en dessous de leur titre. Cette exercice
met en pratique les `position` que nous avons vu au TD précédent et que nous
vous rappelons.

#### Position

La propriété CSS `position` offre de nouvelles possibilités pour le
positionnement des éléments. Ses valeurs sont :

* `static` : comportement normal (par défaut), l'élément est inséré normalement.
* `relative`: le reste de la page fait comme si l'élément était positionné
  "normalement". De son côté, l'élément est positionné *relativement* à la
  position où il aurait dû être. On voit donc un espace où l'élément aurait dû
  être en `position:static`.
* `absolute` : le reste de la page fait comme si l'élément n'existait
pas. L'élément se positionne relativement à son plus proche ancêtre
**positionné** (voir ci-dessous) ou sinon à `<body>` (si aucun
ancêtre n'est positionné).
* `fixed` : le reste de la page fait comme si l'élément n'existait
pas. L'élément se positionne relativement à la fenêtre d'affichage ; il paraît donc *fixé* lors d'un défilement de la page.

Un élément est dit **positionné** s'il a une position autre que `static` (qui est la valeur par défaut).
Pour indiquer le décalage de position, on utilise les propriétés `top`, `left`,
`right` et `bottom`. Par exemple, les propriétés

```css
position:relative; 
top:20px; 
left:20px; 
```

vont positionner un élément `20px` plus à droite et en bas qu'il n'aurait dû l'être.

Référence : [Mozilla Developer Network (MDN)](https://developer.mozilla.org/fr/docs/Web/CSS/position)

<div class="exercise">

1. Ajoutez les sous-menus suivants aux éléments de la navigation. Ces sous-menus
   doivent être les petits frères des liens `<a>`, *c-à-d* qu'ils se placent
   juste après `<a>` tout en ayant le même père `<div>`.

   * pour l'ancre "Accueil" 

     ```html
     <div class="submenu">
       <div><a href="./one.html">one</a></div>
       <div><a href="./two.html">two</a></div>
       <div><a href="./three.html">three</a></div>
     </div>
     ```

   * pour l'ancre "Contact"

     ```html
     <div class="submenu">
       <div><a href="./other.html">other</a></div>
       <div><a href="./another.html">another</a></div>
     </div>
     ```

1. Positionnons bien ces sous-menus : nous souhaitons que l'affichage du reste de la page
   fasse comme si ces sous-menus n'existaient pas. De plus, nous souhaitons que les
   sous-menus se placent sous leur titre de menu (le `<div>` parent "Accueil" ou
   "Contact"). Nous allons procéder en plusieurs étapes :

   1. Quelle valeur de `position` correspond à ce comportement des sous-menus ?
      <!-- position:absolute -->
   2. Créez la règle CSS qui affecte cette valeur de `position` aux balises de
      classe `submenu` avec un décalage de `50px` par rapport au haut et de
      `0px` par rapport à la gauche.
   3. Les sous-menus ne sont pas encore bien placés car ils se positionnent par
      rapport à la mauvaise balise. **Quelle est cette balise** par rapport à
      laquelle ils se sont positionnés ? Relisez la section sur les éléments
      dits positionnés pour confirmer votre impression.
   4. Nous souhaitons que nos sous-menus se placent par rapport à leur `<div>`
      parent. Il va donc falloir rendre ce `<div>` *positionné*, sans que cela
      ne le déplace ni que le reste de la page ne bouge.  
      **Quelle valeur de `position`** donnée aux `<div>` parent correspond à la
        description précédente ? Créez la règle CSS et le menu doit être enfin
        bien placé.
      <!-- position:relative -->

</div>

### Menu déroulant : Partie 2 -- affichage lors du survol

Nous allons maintenant nous servir de `display:none` pour afficher le sous-menu
juste quand la souris est au dessus du titre correspondant.

<div class="exercise">

1. Donnez aux sous-menus la couleur de fond `#aca`. Puis masquez-les
   par défaut en CSS.

1. Réaffichez le premier sous-menu (resp. le deuxième) avec `display:block`
lorsque la souris passe au-dessus de "accueil" (resp. "contact") en CSS.  

   **Aide :** En pratique, nous allons vérifier si le père `<div>` du sous-menu
     est survolé (`:hover`). Nous souhaitons donc un sélecteur CSS qui
     sélectionne les éléments de classe `submenu` qui sont fils d'un
     `<div>` survolé qui sont fils d'un `<nav>`.

</div>

À ce stade les sous-menus apparaissent bien lorsque l'on survole les éléments
"Accueil" et "Contact". Par contre il n'est pas possible d'entrer dans ces
sous-menus.  Nous consacrons toute la prochaine section au comportement
`display:flex` qui va permettre d'améliorer l'apparence de notre menu et de
remédier à ce problème d'accessibilité.

## `display:flex`

La valeur de display `flex` correspond au layout appellé FlexBox.
Appliquée à un élément, la valeur de display `flex` va permettre de modifier la
disposition **de ses enfants**. C'est donc une différence
fondamentale avec les valeurs `block` et `inline`, qui eux avaient un impact
directement **sur l'élément lui-même**.

Lorsque le display est `flex`, on peut par exemple :

 * fixer le sens de rendu des enfants, 
 * l'espace entre ces derniers, 
 * leurs centrages dans les différentes directions,
 * modifier leurs ordres d'apparition, ...

Nous précisons par la suite quelques-unes de ces contraintes/propriétés.

### La propriété `flex-direction`

La propriété `flex-direction` permet de préciser si les enfants vont se mettre
en ligne ou en colonne et dans quel ordre. Ses valeurs sont :

 * `row` : mise en ligne dans l'ordre classique de gauche à droite ;
 * `row-reverse` : mise en ligne dans l'ordre inversé ;
 * `column` : mise en colonne dans l'ordre classique de haut en bas ;
 * `column-reverse` : mise en colonne dans l'ordre inversé.

L'attribut `flex-direction` s'appliquant aux enfants, il rentre en conflit avec
les valeurs de display `block` ou `inline` de ces derniers.  L'exercice suivant
va nous permettre entre autres de savoir qui surcharge l'autre en cas de
conflit.


<div class="exercise" >
 1. Donnez à l'élément `<nav>` la valeur de display `flex`.
 1. Changez la valeur du display des `<div>` directement enfants de `<nav>` en `block` puis en `inline`. Que cela change-t-il ?
 1. Donnez à l'élément `<nav>` le bloc de déclaration `flex-direction:column`, que cela change-t-il ? 
 1. Remettez la direction dans sa valeur par défaut, `row`.
 1. Donnez une largeur fixe de `100px` à tous les `<div>` **descendants** de
   `<nav>` pour que les menus et les sous-menus soient de la même largeur.

</div>


### La propriété `align-items`


La propriété `align-items` permet de préciser comment les enfants vont venir
occuper l'espace perpendiculairement à la direction donnée par
`flex-direction`. Dans notre cas (`flex-direction:row`), `align-items` va donc
nous permettre de préciser comment occuper l'espace vertical des `<div>`
contenus dans le `<nav>`.


Ses valeurs sont  :

 * `stretch` : étirer pour prendre tout l'espace (valeur par défaut);
 * `center` : centrer sans étirer ;
 * `baseline` : aligne les lignes de base des éléments ;
 * `flex-start` : alignement au début de l'axe perpendiculaire au sens de `flex-direction` ;
 * `flex-end` : alignement à la fin de l'axe perpendiculaire.

Référence : [Mozilla Developper Network](https://developer.mozilla.org/fr/docs/Web/CSS/align-items)


<div class="exercise" >

Dans cet exercice, nous souhaitons que les `<div>` titres des menus soient
centrés verticalement mais qu'ils prennent toute la hauteur.

<!-- Expliquer ce qu'on veut faire :
centrer les titres des sous-menus et qu'ils prennent toutes la hauteur ?
Il faut changer le top:50px pour top:200px ?
Puis revenir en arrière
-->

1. Pour mieux voir le comportement, nous allons donner jusqu'à la fin de cet
   exercice une hauteur de `200px` et la couleur de fond `#FF00FF` à `<nav>` et,
   pour les sous-menus, un décalage de `200px` vers le bas.

1. Centrez les éléments enfants de `<nav>` à l'aide de la propriété
   `align-items` de `<nav>`. Que constatez-vous sur la hauteur des `<div>` et
   l'accessibilité des sous-menus avec la souris ? Est-ce que le `<div>` est
   centré verticalement ?

   <!-- Menu centrés verticalement mais ne prennent pas toute la hauteur et du
   coup on n'arrive pas à accéder aux sous-menus -->

   **Note :** Si rien de ne se passe, utiliser l'inspecteur du navigateur pour
   comprendre ce qui est centré (la marge automatique placée sur le `<nav>` par
   exemple peut expliquer des choses).

1. Utilisez maintenant la valeur `stretch`.  Que constatez-vous sur la hauteur
   des `<div>` et l'accessibilité des sous-menus avec la souris ? Est-ce que le
   `<div>` est centré verticalement ?

   <!-- Menu non centrés verticalement mais prennent toute la hauteur et du
   coup accéde aux sous-menus -->

1. Faites en sorte que les sous-menus restent accessibles et que les textes
   "Accueil" et "Contact" soient centrés verticalement dans la barre de
   navigation. Pour ceci :
   
   1. Faites en sorte que les `<div>` prennent toute la hauteur à l'aide des 2
      question précédentes.
   1. Centrez verticalement les liens `<a>` au sein des `<div>` : il faut pour
      cela que les `<div>` enfants du `<nav>` soient `flex`, ce qui va permettre
      de centrer verticalement ses enfants `<a>` à l'aide de l'un des 2
      comportements vues précédemment.

1. Annulez (commentez) les propriétés temporaires de la question 1.

</div>

### La propriété `justify-content`

Cette propriété permet de préciser la façon dont les enfants vont se disposer dans la direction donnée par `flex-direction`.

Les valeurs possibles sont :

 * `flex-start` : au début de l'axe donné par `flex-direction` ;
 * `flex-end` : à la fin de cet axe ;
 * `center` : centré sur cet axe ;
 * `space-between` : les élements vont du début à la fin de l'axe en rajoutant
   des espaces entre les éléments ;
 * `space-around` : les élements vont du début à la fin de l'axe en rajoutant
   des espaces autour des éléments (donc entre les éléments et avant le premier
   et après le dernier) ;

<div class="exercise" >

 1. Justifiez les blocs de titres de menus non à gauche mais à droite de
    `<nav>`, avec votre display favori. Colorez temporairement le fond de
    `<nav>` pour pouvoir vérifier que les titres se sont bien déplacés sur la
    droite de `<nav>`.

</div>

### Flexbox, une valeur relativement récente

Si ces dernières possibilités offertes par `flex` semblent triviales voire
naturelles pour le néophyte, elles représentent en pratique une avancée majeure
dans le monde du CSS. Avant `flex`, certaines propriétés relevaient d'une
expertise véritable de l'intégrateur (exemple : le centrage vertical), ou
étaient même confinées dans le domaine du fantasme (les justifications, le
comportement des éléments sur l'espace restant, etc.).

Aujourd'hui flexbox est bien implémenté dans
[les différents navigateurs](https://www.caniuse.com/#search=flexbox).
Nous ne vous présenterons donc pas d'autres valeurs de display, car elles sont
devenues inutiles (`display:inline-block`, `display:table`), ni encore moins des
techniques d'alignement avec des `float`, qui ont toujours été techniquement
merdiques.

Il y a d'autres propriétés intéressantes autour de flexbox, la référence suivante
est très instructive :
[https://css-tricks.com/snippets/css/a-guide-to-flexbox/](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

## Mise en page globale

### En-tête

<div class="exercise" >
 1. Placez la citation et le menu de navigation sur la même ligne (la citation
    sera à gauche et le menu à sa droite) toujours avec votre display favori.
 1. Repositionnez le menu pour qu'il soit en bas de la balise `<header>` (oui,
    encore avec flexBox).
 1. Mettez un fond blanc au `<header>`.
 1. Enlevez la couleur de fond des liens dans le menu.

</div>


### Deux colonnes

Il est temps d'avoir un layout (aménagement de l'espace) pour notre site.

<div class="exercise" > 
 1. Donnez au body la `width` de `900px`.
 1. Déplacez dans le HTML la section contenant la `<table>` dans `<aside>` si
    cela n'est pas déjà fait.
    <!-- Vraiment ??? -->

 1. Utilisez la valeur de display `flex` sur la balise `<main>` pour que ses 
    enfants `<article>` et `<aside>` s'affichent comme deux colonnes côte à 
    côte.
 1. Fixez la largeur de `<article>` à `60%`, et celle de `<aside>` à `30%`. Ce
    dernier élément aura une marge gauche de `10%`.
 1. Donnez à `<aside>` et à `<article>` la couleur de fond `#CCC`.


<!--
 1. Dans la page "contact", alignez l'image de Chuck avec l'adresse de contact.
 1. Donnez à l'image la hauteur de `300px`, centrez le texte verticalement.
-->
</div>

<!--
besoin de box-sizing : border-box pour le two column layout ?
Non car pas de bordure et les espaces ne sont pas affichés avec display:flex
-->


## Cacher ou enlever un élément du rendu



Il existe plusieurs façons de faire disparaitre de l'écran un élément HTML avec un bloc de déclaration : 

 * `display:none` 
 * `visibility:hidden`

Nous avons déjà utilisé le bloc de déclaration `display:none` dans le menu pour cacher un sous-menu sans que ce dernier marque la page par son abscence.
Le bloc de déclaration `visibility:hidden` quant à lui laisse l'espace innocupé à la place de l'élément.

Voyons un usage de `visibility:hidden` :

<div class="exercise">

 Nous voulons marquer visuellement le menu sous la souris par une petite puce dans les `<a>` du menu. 

```html
<span class="puce">■</span>
```
Elle se positionne à gauche du texte, elle n'est visible que lorsque la souris
survole le `<div>` contenant. Dans le cas contraire l'espace reste occupé (pour
ne pas faire un effet de flicker/tremblement au survol du menu)


1. Ajoutez cette puce devant le texte des liens `<a>`,
1. Ajoutez `visibility:hidden` à l'élement de classe `puce` et la valeur
   `visible` sur le survole de la souris sur le `<div>` parent.
1. Supprimez la couleur de fond sur les balises `<a>` pour plus de lisibilité.
1. (Optionnel) Styliser les sous-menus.

</div>




## Fini !

Le mot de la fin à propos de flex ? 

<blockquote> 

Moi je stoppe sur mon flex.
Quand je sticks ma vibes le dancefloor se breaks et se fluxe dans la vibes.

<cite>Gad Elmaleh</cite>
</blockquote>


<!--

Rajouter référence MDN ???

Parler aussi des pseudo-éléments type ::first-letter ?
::after
::before
::first-letter
::first-line

MDN : Tout comme les pseudo-classes, les pseudo-éléments sont ajoutés aux
sélecteurs. Mais au lieu de décrire un état spécial, ils permettent de styler
certaines parties du document.

<style type="text/css">
p::first-letter { font-size:1.4em; }
</style>

-->

