---
title: Les bases du HTML / CSS
subtitle: Le CSS, responsable du rendu.
layout: tutorial
---

# CSS: un langage pour définir la mise en forme


Les standards définissant le CSS sont publiés par le World Wide Web Consortium
(<a href="http://www.w3.org/">W3C</a>).

<!-- lien pour HTML et compléter le lien pour CSS -->


> <i>Cascading Style Sheets (CSS) est un mécanisme simple pour ajouter du style
> (exemple fonte, couleurs, espace) à un document web.</i>  
> <cite><a href="http://www.w3.org/Style/CSS/">W3C</a></cite>

Le CSS est responsable du rendu du site sur votre écran, mais aussi sur un smartphone et des impressions papier (des ensembles de règles CSS peuvent être spécifiés pour chacun de ces média).


Bien que l'acronyme signifie donc <b>des</b> feuilles de style, on parlera <b>du</b> CSS (le langage utilisé ou le mécanisme), mais on fera pas les pédants tant les deux sont confondus à l'usage (l'usage fait très souvent loi lorsque l'on fait du CSS !).

Savoir les bases du CSS est relativement facile et indispensable pour qui veut travailler dans les métiers du Web. En maîtriser tous les aspects est un métier (celui d'intégrateur Web, qui traduit en HTML et CSS le travail du Web-designer).

## Tutoriel d'introduction

Nous allons travailler principalement sur ce TD sur un fichier `styles.css`.
Créer ce fichier à partir du fichier index.html dans le répertoire `css/`.

Dans le fichier index.html, il faut ajouter la ligne suivante dans l'en-tête du
document HTML (dans la partie `head`) :

~~~
<link rel=‘stylesheet’ type=‘text/css’ href=‘css/styles.css’>
~~~
{:.html}


Nous déclarerons dans ce fichier des règles CSS.

Une règle CSS est composée de deux parties: 

 * un sélecteur CSS,
 * un bloc de déclaration.

Par exemple la règle CSS suivante donne à tous les div la hauteur de 200 pixels et définie comme couleur de fond le bleu : 

~~~
div { height:200px;background-color:blue;}
~~~
{:.css}

 * le sélecteur est `div`,
 * le bloc de déclaration est `height:200px;background-color:blue;`.


 Nous allons plus amplement présenter quelques bloc de <a href="#declarations">déclarations</a> et la façon de concevoir des <a href="#selectors" >sélecteurs</a>.
 Nous passerons ensuite à la mise en pratique dans la section <a href="#exercice">Exercices</a> .


## Les outils de développement sont votre ami.

Pour la partie HTML, l'outil de développeurs c'était votre ami ; pour le CSS, il
est promu au grade de "best-friend-ever".  Sélectionner un élément HTML avec
l'outil des développeurs ne permet pas seulement de voir les règles CSS
appliquées à ce dernier, il permet aussi de les CHANGER. Autant dire qu'il est
conseiller d'abuser de cet outil pendant le TD pour bidouiller tout et n'importe
quoi.

## Commentaires

En CSS, seul les commentaires avec `/*` et `*/` sont autorisés.
Si vous utilisez `//` dans votre fichier `styles.css` vous allez avoir des problèmes (les règles CSS suivantes ne seront pas appliquées).


## Bloc de déclaration


Les blocs de déclarations porte sur des ensemble "`attributs:valeur`" séparés par des "`;`" (exemple `height:200px;background-color:blue;`).
Nous présentons ici quelques exemples valides de  valeurs et des attributs associés.

### Couleurs

Les mots `aqua`, `black`, `blue`, `fuchsia`, `gray`, `green` ...  peuvent être utilisés pour définir une couleur.
Vous pouvez être plus précis et définir une couleur avec le format #RRVVBB ou #RVB. R, V et B sont les valeurs en hexadécimal de la composante respectivement Rouge, Vert et Bleue.

 * `#000000` est noir,
 * `#FFFFFF` est blanc,
 * `#F00` ou `#FF0000` est rouge,
 * `#FF00FF` est rose (c'est beau le rose).

Les couleurs peuvent s'utiliser sur plusieurs attributs d'un élément HTML :

 * la couleur du texte : color:red;
 * la couleur du fond : background-color:#FF00FF;
 * ...


### Dimensions

Certains éléments peuvent avoir une taille définie par CSS, d'autres épousent la place minimale nécessaire à leur rendu.
Cela caractérise entre autres chose des éléments inline et block. Nous préciserons ces notions dans le TD suivant, en attendant on s'en tiendra à 
expliciter les unités de dimensions applicables.

L'unité la plus utilisée est le pixel "px" pour pixel CSS. Cette unité ne compte pas le nombre de pixels physique à l'écran mais est plutôt basée sur une échelle de bonne lisibilité pour le média de rendu (i.e. il est donc relativement adapté pour un écran d'ordinateur, un smartphone, une tablette,...).

Pour plus de détails sur ce qu'est cette unité : http://www.w3.org/TR/css3-values/#absolute-lengths

On peut aussi donner des dimensions relatives en pourcentages (`width:50%`).

D'autres unités de mesures sont possibles (`pt`, `cm`, ...), mais nous nous en tiendrons aux `px`.



Les dimensions sont utilisées sur différentes parties d'un élément.
Exemple :

~~~ 
 .ma_class {
 			height:150px;
 			width:50px;
 			padding:15px;
 			border-width:1px;
 			}
~~~
{:.css}



### Fontes

référence : http://www.w3.org/TR/CSS21/fonts.html




<b> La propriété font-family</b>

Rajouter maintenant la règle suivante :

~~~
p { font-family: "lucida calligraphy", "Arial", "sans-serif"; }
~~~
{:.css}

Les deux dernières fontes précisées par la règle sont des "fall-back" : elles seront utilisées si et seulement si les précédentes ne sont pas disponibles sur le navigateur.

<b> La propriété font-size</b>

Utiliser la propriété font-size pour changer la taille de la citation.

### Textes

Tester les règles ci-dessous :

~~~
p {
  text-align: justify ;
}
~~~
{:.css}

## Les Sélecteurs CSS

Les sélecteurs CSS permettent de préciser les éléments qui vont être impactés
par la règle CSS.  Les sélecteurs CSS sont aussi utilisés sur d'autres
problématiques du développement Web que nous verrons l'année prochaine.  Bref
vous en aurez au partiel, c'est sûr.

On peut construire un sélecteurs CSS complexe à partir de sélecteurs de bases et
de règles de compositions.

### Sélecteurs de bases 

Il nous faut compléter nos connaissance sur le HTML.  Toutes les balises peuvent
se voir adjoindre différents attributs.  Suivant le type (i.e. `<span>`,
`<div>`, `<a>`,....) des balises, ces attributs auront des sens différents.
Deux attributs sont très important pour les règles CSS : l'id et la class d'un
élément.

Par exemple :

~~~
<div id="monidentifiant" class="skill feature" ></div>
~~~
{:.css}


Ce code HTML déclare un élément de type `div` avec comme identifiant unique `monidentifiant` et ayant deux classes : `skill` et `feature`.
Un identifiant est unique pour toute la page HTML. Un élément peut avoir plusieurs classes comme dans l'exemple précédent et ces classes ont du sens si elles sont attribuées à de multiples élément de la page.

Les classes, id et type permettent de construire 95 % des règles CSS.
Voyons la syntaxe pour les utiliser.

#### type

Il s'agit juste d'utiliser le type (`a`, `p`, `img`,...) sans autre décorateur.
si l'on veut donner la couleur rose à tous les liens d'une page, il faut écrire

~~~
a {
  color: pink ;
}
~~~
{:.css}


#### id

Le décorateur associé à l'id est le caractère `'#'`.
si l'on veut donner une width de 100px à notre div déclaré plus haut il faut écrire

~~~
#monidentifiant {
  width: 100px;
}
~~~
{:.css}

#### Classes


Le décorateur associé aux classes est le caractère `'.'`.
si l'on veut donner une height de 200px à tous les éléments qui ont la classe `skill`,  il faut écrire

~~~
.skill {
  height: 200px;
}
~~~
{:.css}


### Règles de compositions, Sélecteurs complexes.

Un sélecteur CSS peut être plus ou moins compliqué. Sa sémantique peut aller de :

* je vais appliquer la règle à tous les div de la page
* je vais appliquer la règle à tous :
	* les div ayant la class "toto" et qui sont fils d'un élément d'id #titi mais aussi fils directs d'un élément de type span.
	* <b>ou</b> l'élément qui a pour id "my_id".

### Pseudo Classes

Pseudo Classes des liens 

~~~
.skill {
a:link {color: yellow;}
a:visited {color: pink;}
~~~
{:.css}

Pseudo Classes d'interaction


~~~
.skill {
a:hover {text-decoration: underline;}
~~~
{:.css}

#### Les combinaisons (Combinators) 

http://www.w3.org/TR/css3-selectors/#combinators

A partir des sélecteurs de bases précédents, il est possible de créer des sélecteurs complexes.
Nous présentons dans la suite les sélecteurs qui sont utilisés en moyenne 95 % du temps.


#### Regroupement 

La première façon de "composer" des sélecteurs et juste le regroupement :

~~~
h1 {color: red}
h2 {color: red}
h3 {color: red}
~~~
{:.css}

peut s'écrire :

~~~
h1,h2,h3 {color: red}
~~~
{:.css}

Il ne s'agit pas vraiment de combinaison, mais plutôt d'une factorisation de règles CSS.


#### Combinaison

On veut parfois préciser un élément au travers de plusieurs sélecteurs de bases sur ce dernier, il suffit pour cela de coller les sélecteurs de base.

Par exemple :

~~~
div.toto
~~~
{:.css}

Signifie le div qui a la classe toto

Ou encore 

~~~
.titi.toto
~~~
{:.css}

L'élément qui a la classe toto ET titi.


#### Descendance

Pour discriminer certains éléments sur lequel on veut que porte un sélecteur il est très courant de préciser de quoi il est descendant dans le code HTML.
Pour expliciter ce chemin on ajoute un espace entre les sélecteurs de base.

##### Directe (enfant)

Par exemple 

~~~
#titi>.toto
~~~
{:.css}

##### Indirecte

Par exemple 

~~~
#titi .toto
~~~
{:.css}

Signifie les éléments qui ont la classe toto ET qui sont descendants d'un
élément d'id titi.


##### Fréres/adjacents

Les deux éléments sont tous deux fils directs d'un même élément.

Par exemple 

~~~
#titi + .toto
~~~
{:.css}

Signifie que l'élément ayant la classe toto et qui est frère de l'élément d'id
titi doit avoir son texte en rouge.

## Comment se décline les CSS applicables sur un site.

Il est possible d'ajouter plusieurs fichiers CSS dans une page et même si l'on
n'a qu'un seul fichier, plusieurs règles peuvent être contradictoires.  Pour
complexifier le tout, nous verrons que l'on peut ajouter du CSS dit "inline"
directement dans le HTML...  et que les navigateurs appliquent des styles par
défaut.  Enfin on peut finir une règle CSS avec le code `important!` ce qu'il
lui

### Style par défaut des navigateurs 


(reset CSS),

### Style inline,

### Styles dans un fichier css,

### Ordre de priorité de tout cela ?

9. Calculating a selector's specificity

A selector's specificity is calculated as follows:

count the number of ID selectors in the selector (= a)
count the number of class selectors, attributes selectors, and pseudo-classes in the selector (= b)
count the number of type selectors and pseudo-elements in the selector (= c)
ignore the universal selector



<ul>
<li>Style inline,</li>
<li>Style marqué important!,</li>
<li>Style avec le sélecteur le plus précis
(si plusieurs fois le même sélecteur pour des déclarations non compatibles, la dernière gagne),</li>
<li>Style du navigateur.</li>
</ul>


## Exercices : 

Tout va principalement se passer dans styles.css.



### Couleurs :

Le fond de notre page est tout blanc par défaut.
Nous allons changer cela en donner au body la couleur qu'à choisi le graphiste/webdesigner : `#838892`.



En ce qui concerne les paragraphes, vous avez reçu comme consigne d'alterner leurs couleurs entre #5BBDBF et #FF5850.



### Dimensions :

<a href="https://viget.com/inspire/the-line-length-misconception" >Plusieurs</a>
études <a href="https://en.wikipedia.org/wiki/Line_length">suggèrent</a> que des
lignes trop longues ou trop courtes nuisent gravement à la lisibilité d'un
site. Pour traiter grossièrement le problème, limitez en CSS la largeur de
l'élément body à 600px.

Le centrer au milieu avec des marges auto, lui donner du padding et une
line-height de 150%

L'image beware.jpg a du style, mais elle prend un peu trop de place, limitez sa
hauteur à 300px.

H2 et H3 du padding et du border radius

### Fontes : 

p { font-family: "lucida calligraphy", "Arial", "sans-serif"; }

### Liens visités

Faire en sorte que les liens visités apparaissent en gris. Lorsque la souris
passe sur un lien, donner lui la couleur orange (sauf s'il a déjà été visité,
auquel cas il reste en gris).


## CSS et HTML des rôles bien distincts et complémentaires.

Il y a une séparation claire entre les rôles du HTML (Contenu) et des CSS
(Présentation).  Ce choix n'est pas évident au premier abord : par exemple votre
document .odt ou .doc ne sépare pas la présentation du contenu (Votre document
Latex oui).  Pour parler des trains qui arrivent à l'heure, il faut dire que
cette césure est une idée vraiment formidable.  Elle sous-tend la promesse de
pouvoir changer la forme très rapidement sans toucher au fond :

 * Cela permet de changer la présentation du document suivant s'il est destiné à
 	l'impression ou à être rendu par un navigateur, les unités métriques par
 	exemple ont plus de sens pour une imprimante que pour un écran.
 * Cela permet par exemple de refaire un site Web en se concentrant sur les CSS
   sans (trop) toucher au HTML.
 * Cela permet de réutiliser du CSS pour des sites dynamiques. Par exemple quand
   lemonde.fr publie un nouvelle article, on ne refait pas le style expressément
   pour ce dernier: il s'agit d'un nouveau document HTML partageant le même CSS
   des articles précédents.


## CSS et HTML, Entre la césure...

Souvent le CSS empiète sur le HTML et inversement. Quand le premier s'en
offusque et dit au deuxième de faire attention où il met les pieds, ce dernier
répond "je mets pieds où je veux,....".


Car la césure en apparence très nette cache en fait plusieurs entre-deux au
travers l'utilisation de certaines balises HTML dénuées de sémantiques (n'ayant
qu'un but de présentation) ainsi que la possibilité au travers des styles
inlines (du style ajouté directement dans le HTML) de se substituer aux CSS.

## Mon navigateur, mes règles

La complexité des CSS est parfois "artificielle" au sens où elle repose sur de
l'existant, sur des différences entre navigateurs.



### Utiliser le HTML pour la présentation

Par le passé, les navigateurs étant tous à des degrés différents conformes aux
directives CSS. Il est probable que les intégrateurs ayant eux affaire à
Internet Explorer 6 par exemple soient plus souvent chauves que la moyenne.  Il
était courant de voir des sites utiliser des tables pour faire des layouts entre
autre exemple.  Cela n'est pas forcément du à une méconnaissance de la part de
l'intégrateur, mais bien au contraire parfois d'une expertise sur des solutions
qui marchent sur des






