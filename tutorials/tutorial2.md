---
title: TD2 &ndash; HTML / CSS avancé 1/2
subtitle: structuration et stylisation, block & inline, combinaison de sélecteurs
layout: tutorial
---


La spécification HTML5 propose différentes manières de classer les
balises/éléments selon leurs caractéristiques
([Liste des balises par catégorie](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)). Nous
allons ici nous intéresser à deux types spécifiques :

* les balises de structure : elles permettent de délimiter l'articulation
  logique de la page web en la découpant en différentes sections. Par défaut,
  ces balises découpent la page web en sections horizontales qu'elles occupent
  en entier (du bord gauche au bord droit de la section). Deux balises de flux
  ne peuvent pas partager une même section horizontale aussi les espaces
  qu'elles délimitent dans la page s'enchaînent-ils verticalement.

* les balises au niveau du texte : elles apportent une précision sur la
  sémantique d'une partie du texte (mise en avant d'une partie de texte importante, ajout d'un type exposant, time,...).

Quelques exemples :

* balises de structure :

   * `<header>` : section contenant l'en-tête affichée de la page
   * `<nav>` : section contenant une série de liens hypertextes pour la navigation
     sur le site
   * `<main>` : section principale de la page, celle qui contient le contenu
     spécifique à cette page. Cette balise ne peut être présente dans une autre
     balise présentée ici à l'exception de « div ».
     <!-- Elle n'est pas supportée par Internet Explorer <= 10 mais le support peut -->
     <!-- en être ajouté grâce à Javascript et en utilisant la règle css « main -->
     <!-- {display : block} ». -->
   * `<article>` : section contenant un document « auto-suffisant », i.e. qui peut
     être séparé du reste de la page et gardera cependant tout son sens. Une
     page peut contenir plusieurs articles, dans le cas d'un blog par exemple,
     de commentaires, d'une page listant les publications récentes ...
   * `<aside>` : section contenant du matériel périphérique au contenu
     principal. Cela peut-être par ex. une série de liens spécifiques au document
     principal, un bandeau de publicités …
   * `<footer>` : section contenant le pied de page.
   * `<section>` : une section non spécifique, ou une sous-section d'un article,
     d'un menu... Doit typiquement commencer par un titre hX.
   * `<figure>` : une illustration (au sens large) « auto-suffisante » illustrant le
     document principal ou un article, et qui doit pouvoir être placée librement
     dans la page sans en altérer le déroulement (par ex. dans le texte, dans un
     appendice...)
   * `<h1>`- `<h6>` : titres de section
   * `<blockquote>` : une citation
   * `<p>` : paragraphes du texte
   * `<address>` : coordonnées de contact de l'auteur. Il ne peut y avoir qu'un bloc
     « address » par article et un pour le restant de la page

* balises au niveau du texte :
   * `<sup>` : un exposant
   * `<time>` : mise en valeur d'une date
   * `<em>` : emphase sur du texte
   * `<strong>` : mise en gras du texte
   * `<br>` : saut de ligne


Ces balises au niveau du texte sont souvent naturelement liées à un style
associé (les `<em>` seront stylisées par une mise en italique, les `<sup>` en exposants,...).
Les navigateurs se chargent d'ajouter pour nous ce style ad-hoc.

Il existe encore beaucoup d'autres balises HTML. Cela dit, il arrive qu'aucune ne
corresponde à ce que l'on veut exprimer (lors d'une construction de layout par exemple). Deux balises neutres ont été ajoutées
pour ces constructions :

   * `<span>` : cette balise est neutre, sans signification particulière. Son utilisation permet
     entre autres de créer des règles de formatage spécifiques du contenu
     textuel (par exemple lorsque nous avons ajouter la class `skill`).
   * `<div>` : cette balise est « neutre », son utilisation permet de
distinguer une section qui ne revêt aucune signification
particulière. Contrairement au `span` elle provoque un saut de ligne.

## Structuration de la page

Vous allez d'abord structurer logiquement le contenu du site. Voici un *template* HTML d'une structuration classique de
page Web.


~~~
<!DOCTYPE html>
<html>
    <head>...</head>
    <body>
        <header>
            ...
            <nav>...</nav>
        </header>
        <main>
            <article>...</article>
            <article>...</article>
            <aside>...</aside>
        </main>
        <footer>
            ...
        </footer>
    </body>
</html>
~~~
{:.html}

Pour fixer les idées, voici un aperçu d'une mise en page correspondante à
l'exemple précédent :

<img src="{{site.baseurl}}/assets/sections.png" alt="Structuration d'une page" style="margin: 0 auto;display: block;">

<div class="exercise">

1. Ajouter une balise `<header>`. Son contenu sera la citation du TD1 et une
   barre de navigation `<nav>` vide pour l'instant,
2. Ajouter une balise `<main>`, une balise `<article>` et une balise `<aside>`
   comme dans le *template* précédent. Mettez l'ancien contenu de la page dans
   `<article>` sauf les deux dernières sections ("Les sites amis" et
   "Le Top 10 des derniers facts proposés") qui vont dans `<aside>`,
3. Ajouter une balise `<footer>` qui contient le lien vers le retour au début du site,
4. Ajouter dans la balise `<nav>` deux liens dans une structure de liste
   contenant : Un lien nommé "Accueil" qui pointe sur la page courante `index.html`
   et un nommé "Contact" qui pointe vers une page `contact.html`,
5. Construire cette page `contact.html` au même niveau que `index.html`. Elle
   doit contenir l'image [contact.jpg]({{site.baseurl}}/assets/contact.jpg) pour
   illustrer que nous sommes bien à l'écoute. Ajouter l'adresse avec la balise
   `<adress>` contenant :
 * Email : chuckn@yopmail.com
 * IUT de Montpellier Sète <br>
   99 avenue d'Occitanie <br>
   34296 Montpellier Cedex 5
 
</div>

À ce point, le travail de division du site n'a pas encore de résultat visuel
marquant. C'est avant tout un travail de structuration logique qui permet au
navigateur, à un moteur de recherche de mieux comprendre votre page web.  Nous
verrons comment structurer la page dans les TDs suivants. Pour la suite du TD,
nous allons ajouter du style aux éléments de la page courante.


## Règles de compositions des CSS

À partir des sélecteurs de bases présentés
[dans le TD précédent]({{site.baseurl}}/tutorials/tutorial1_2.html#les-slecteurs-css-de-base), il est
possible de créer des
[sélecteurs complexes](http://www.w3.org/TR/css3-selectors/#combinators).
Par exemple, nous allons voir comment sélectionner les `<div>` ayant la classe `toto` et
qui sont fils d'un élément d'identifiant `titi`.


Nous exposons dans cette section les principaux moyens de composer un sélecteur
CSS complexe.


### Regroupement 

La première façon de composer des sélecteurs est le regroupement.
Les trois règles suivantes :

~~~
h1 {color: red}
h2 {color: red}
h3 {color: red}
~~~
{:.css}

peuvent s'écrire :

~~~
h1,h2,h3 {color: red}
~~~
{:.css}


### Combinaison

Pour préciser un élément, il suffit d'apposer plusieurs sélecteurs de base
(balise, classe ou identifiant). Par exemple :

~~~
div.toto
~~~
{:.css}

correspond au sélecteur des `<div>` qui ont la classe 'toto'. Ou encore 

~~~
.titi.toto
~~~
{:.css}

correspond aux éléments qui ont la classe `toto` <strong>ET</strong> `titi`.

### Descendance


On veut pouvoir limiter une règle css à une sous partie de l'arborescence HTML, pour cela on utilise la relation de descendance.


#### Directe (enfant)

La relation de descendance directe est signifiée par le caractère `>`. Par exemple,

~~~
#titi>.toto
~~~
{:.css}

sélectionne les éléments de la classe `toto` qui sont  <strong>enfant</strong> (direct) de l'élément
d'identifiant `titi`.

#### Indirecte


La relation de descendance indirecte est signifiée par le caractère d'espacement. Par exemple, 

~~~
#titi .toto
~~~
{:.css}

signifie les éléments qui ont la classe `toto` qui sont <strong>descendants</strong> (direct ou indirect) de
l'élément d'identifiant 'titi'. Donc la différence avec `>` est qu'on n'est plus
limité aux fils puisqu'on intègre aussi les petits-fils, arrières-petits-fils
...

<div class="exercise">

Aller sur [http://flukeout.github.io/](http://flukeout.github.io/) et passez
les niveaux de 1 à 11 et le niveau 14.

**Notes :**

* Vous pouvez passer directement à l'exercice que vous voulez en rentrant le
   numéro de l'exercice à la place du sélecteur ;
* La partie de droite de la page est là pour vous aider.


</div>

### Pseudo Classes

Une pseudo-classe est un moyen d'indiquer un état particulier de l'élément qui
doit être sélectionné. Voici quelques exemples :

~~~
/* Style des liens <a> n'ayant pas été visités */
a:link {color: yellow;}
/* Style des liens <a> ayant été visités */
a:visited {color: purple;}
/* Style des liens <a> si la souris les survole */
a:hover {text-decoration: underline;} 

/* le premier caractère d'un texte */
p:first-child {color:red;}
/* le troisième paragraphe */
p:nth-child(3) {color: green;}
/* les textes des éléments li impairs seront verts et les pairs rouges */
li:nth-child(odd) {color: green;}
li:nth-child(even) {color: red;}
~~~
{:.css}


<div class="exercise">

1. Dans la page de Chuck Norris de la semaine dernière, faites en sorte que les
liens `<a>` visités apparaissent en gris.
2. Lorsque la souris passe sur un lien, lui donner la couleur orange.

</div>

<!-- Les règles hover et visited peuvent être en conflit en cas de lien visité
sur lequel on passe la souris. Comme les deux règles ont la priorité, c'est
l'ordre qui va importer.  -->

## Table

L'élément `<table>` correspond à une structuration récurrente, qui sert à représenter un ensemble de données sous forme de colonnes et de lignes.

### Les éléments `<table>`, `<tr>`, et `<td>`

L'élément `<table>` contient la table.
La table est composée de ligne (l'élément `<tr>`) contenant des cellules (élément `<td>`).


### L'élément `<th>`

Dans l'arborescence du document, un élément `<th>` doit être le fils d'un élément
`<tr>`. Il représente une cellule en-tête (le titre d'une colonne ou le titre d'une
ligne du tableau). Il peut être utilisé à la place d'un élément `<td>`.

Voici un squelette de table :

~~~
<table>
   <tr>
      <th>Caract1</th>
      <th>Caract2</th>
      <th>Caract3</th>
      <th>Caract4</th>
   </tr>
   <tr>
      <td>Val1_1</td>
      <td>Val1_2</td>
      <td>Val1_3</td>
      <td>Val1_4</td>
   </tr>
   <tr>
      <td>Val2_1</td>
      <td>Val2_2</td>
      <td>Val2_3</td>
      <td>Val2_4</td>
   </tr>
   ...
</table>
~~~
{:.html}

<div class="exercise">

1. Créer une table avec les sept noms de colonnes suivants : ```Acteurs, Karaté,
Taekwondo, Judo, Chun Kuk Do, Tangsudo, Ju-jitsu```. Les noms doivent être
contenus dans des balises ```<span>```
1. Ajouter la classe  "skill" aux ```<span>``` contenant les noms des arts martiaux.
1. Ajouter les six lignes suivantes (les nombres correspondent à la valeur de
   l'acteur dans l'art martial correspondant) :

     * Chuck Norris, 5, 5, 5, 5, 5, 5
     * Steven Seagal, 3, 5, 3, 2, 3, 5
     * Bruce Lee, 5, 3, 3, 3, 4, 3
     * Jean-Claude Van Damne, 5, 3, 3, 3, 4, 3
     * Bolo Yeung, 2, 4, 4, 2, 5, 3
     * Dolph Lundgren, 2, 4, 4, 2, 5, 3

</div>

### Les éléments `<thead>` et `<tbody>`

Les éléments `<thead>` et `<tbody>` servent à définir plus explicitement la structure de notre table:

 * la définition des colonnes (```Acteurs, Karaté,```...) 
 *  les lignes (nos héros et leurs niveaux de compétence).

<div class="exercise">

Ajouter ces balises pour englober ces deux parties (en oubliant pas pour se
faire leurs balises fermantes ```</thead>``` et ```</tbody>```)

</div>

### Les attributs ```rowspan``` et ```colspan``` 

Les attributs ```rowspan``` et ```colspan``` permettent de fusionner les cellules adjacentes :

 * ```rowspan``` permet de fusionner les cellules sur plusieurs lignes (i.e rows),
 * ```colspan``` permet de fusionner les cellules sur plusieurs colonnes.

<div class="exercise">

Il apparaît que Chuck Norris est toujours au top (niveau 5) dans tous les
martiaux. Fusionner les cellules représentant ses valeurs de manières à mettre
cela encore plus en exergue. Et puis mettez le 5 de Chuck en avant avec une
balise `<strong>` pour bien montrer qui est le patron.

<!-- Faire en sorte que les noms des acteurs soient maintenant des liens vers leurs pages Wikipedia. -->

</div>

À ce stade la structure de votre table reflète le sens que vous vouliez y mettre.
Voyons maintenant comment la styliser.

<div class="exercise">
<!--
 1. Ajouter une règle pour que les textes dans les colonnes ne soient pas sur plusieurs lignes (notamment 'Chun Kuk Do') en utilisant la bonne valeur pour la propriété `white-space`,
 -->
 1. Définissez une couleur de fond #00AAFF pour la partie en-tête `thead` du tableau.
 1. donner la couleur noire aux skill sans modifier le style des éléments ayant la classe `skill` dans les paragraphes,
 (voir la [section sur les sélecteurs]({{site.baseurl}}/tutorials/tutorial2.html#rgles-de-compositions-des-css))
 1. ajouter une règle pour qu'une ligne (*row*) de la table sur deux apparaisse
 en blanc et l'autre avec la couleur `#CCC` <strong>SANS</strong> modifier de quelque façon le
 HTML (voir la
 [section sur les sélecteurs]({{site.baseurl}}/tutorials/tutorial2.html#rgles-de-compositions-des-css))

</div>

## Le modèle de boite

Comme vous l'avez vu précédemment, les balises de type structure définissent des
boîtes. Ces boîtes disposent toutes des propriétés suivantes en CSS :

* padding : espacement entre le contenu est la bordure de la boîte. Le padding est de
  la couleur de la boîte, donc il a le même arrière plan (background-color) que la boîte,
* border : bordure qui entoure le contenu, un border correspond à une width, un style et une couleur.
* margin : marge à l’extérieur de la bordure, entre cette boîte et la
  suivante, et/ou entre cette boite et son parent. La zone couverte par la marge est de la même couleur que sont parent,
* width : la largeur du contenu,
* height : la hauteur du contenu

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodel.png" style="margin:0
auto;display: block;">


À noter que la taille réelle d'une boîte est égale à la taille du contenu `content` 
(width, height) additionnée de l'épaisseur du padding, du bord et de la marge.
Un border n'a pas de style par défaut, donc lui donner une width ne suffit pas pour le voir.

Le margin et le padding peuvent accepter trois arités : 

 * margin : t r b l (t est associé à la valeur du haut (top), r est la valeur droite (right), ...)
 * padding : v h (v est associé aux valeurs verticales, h horizontales)
 * padding : a (la valeur de a est associé aux quatre coté de la boite)

Exemples : 

~~~
 div {margin: 10px 5px;}
.toto {padding : 5px}
#titi {margin : 5px 0 4px 7px;}

~~~
{:.css}

on peut aussi préciser (péniblement) les valeurs unitaires des propriétés `margin-top`, `margin-left`, `padding-bottom`,...

<div class="exercise">
 1. Ajouter du padding vertical de `10px` aux titres de sections,
 1. Ajouter du margin vertical de `30px` aux paragraphes,
 1. Ajouter du padding horizontal de `5px` aux élements ayant la class `skill` dans la table (mais pas aux élements ayant la class `skill` dans les paragraphes).
 1. ajouter une bordure aux titres `<H3>` de `1px`, de style `solid` et de couleur `#CCCCCC`. 
</div>


### Centrer horizontalement :

Pour centrer le contenu d'une balise :

* si l'on veut centrer du texte dans une balise : `text-align: center`
* si le contenu est lui-même dans une balise moins large que la balise parent :
  `margin : auto` sur la balise du contenu.


<div class="exercise">
 1. Centrer le body horizontalement,
 1. Dans la table, centrer le texte des cellules, (le 5 de Chuck notamment est encore trop discret)
</div>

## Les contenus flottant

La propriété `float` associée à un élément permet de faire flotter ce dernier complètement à gauche ou à droite de la ligne où il se trouve. 
Les valeurs de la propriété float sont  ```left```, ```right```, ```none``` et ```inherit```.

<div class="exercise">

 1. Placer l'image de Chuck jeune de class ```young_chuck``` à gauche du texte, 
 1. Placer l'image beware ```beware_img``` à droite du texte.

</div>

<div class="exercise">
1. Rajoutez un nouveau paragraphe qui commence à la phrase "Spécialiste en arts
martiaux, ..." de la section "L'enfance".

   Vous devez alors avoir le rendu suivant :
   
   <img src="{{site.baseurl}}/assets/noclear.png" alt="Sans clear"
   style="display:block;margin:0 auto;">
   
2. Nous souhaitons plutôt ce rendu :
   
   <img src="{{site.baseurl}}/assets/clear.png" alt="Sans clear"
   style="display:block;margin:0 auto;">

   Pour interdire à notre paragraphe d'avoir un élément flottant sur son côté gauche,
rajoutez-lui la règle `clear:left`.  
**Note :** On peut aussi interdire le côté droit avec `clear:right` et les deux
  en même temps avec `clear:both`.

</div>

## Position

La propriété CSS `position` offre de nouvelles possibilités pour le
positionnement des éléments. Ses valeurs sont :

* `static` : comportement normal (par défaut), l'élément est inséré normalement.
* `relative`: le reste de la page fait comme si l'élément était positionné
  "normalement". De son côté, l'élément est positionné *relativement* à la
  position où il aurait dû être. On voit donc un espace où l'élément aurait dû
  être en `position:static`.
* `absolute` : le reste de la page fait comme si l'élément n'existait
pas. L'élément se positionne relativement à `<body>` (ou plus généralement à son
plus proche ancêtre positionné).
* `fixed` : le reste de la page fait comme si l'élément n'existait
pas. L'élément se positionne relativement à la fenêtre d'affichage ; il paraît donc *fixé* lors d'un défilement de la page.

Pour indiquer le décalage de position, on utilise les propriétés `top`, `left`,
`right` et `bottom`. Par exemple, les propriétés

~~~
position:relative; 
top:20px; 
left:20px; 
~~~

vont positionner un élément `20px` plus à droite et en bas qu'il n'aurait dû l'être.

Référence : [Mozilla Developer Network (MDN)](https://developer.mozilla.org/fr/docs/Web/CSS/position)

<div class="exercise">

1. Testez votre compréhension des propriétés `position:
   relative;top:20px;left:20px;` précédente en les appliquant temporairement sur
   l'image `chuck-jeune.jpg`.

2. Ajouter les icônes de réseaux sociaux
[facebook.png ![Facebook]({{site.baseurl}}/assets/facebook.png)]({{site.baseurl}}/assets/facebook.png)
et
[twitter.png ![Twitter]({{site.baseurl}}/assets/twitter.png)]({{site.baseurl}}/assets/twitter.png)
toujours positionnées en bas à droite de la fenêtre d'affichage l'une au-dessus
de l'autre. Essayez aussi temporairement de les afficher tout en bas à droite du
document.

</div>
