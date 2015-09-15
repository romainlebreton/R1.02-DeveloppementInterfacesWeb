---
title: Les bases du HTML / CSS
subtitle: Le CSS, responsable du rendu.
layout: tutorial
---

# CSS: un langage pour définir la mise en forme

Définition (source : Wikipedia) : CSS (Cascading Style Sheets : feuilles de
style en cascade) est un langage informatique qui sert à décrire la présentation
des documents HTML et XML. Les standards définissant CSS sont publiés par le
World Wide Web Consortium (W3C). Introduit au milieu des années 1990, CSS
devient couramment utilisé dans la conception de sites web et bien pris en
charge par les navigateurs web dans les années 2000.


Le CSS permet de préciser pour chaque élement HTML un style associé.
Les CSS sont aussi utilisés pour les impressions papier du site (des règles spécifiques seront alors utilisées). 



Si savoir les bases des CSS est relativement facile, en maitriser tous les aspects est un metier (on parle d'integrateur Web).
Il ne s'agit donc pas ici de faire une étude poussée mais bien d'une initiation.

## Tutoriel d'introduction

Pour indiquer au navigateur qu'il doit utiliser les règles de style de ce fichier pour le document
HTML il faut ajouter la ligne suivante dans l'en-tête du document HTML (dans la partie `head`) :

~~~
<link rel=‘stylesheet’ type=‘text/css’ href=‘styles.css’>
~~~
{:.html}

Nous travaillerons donc maintenant sur le fichier styles.css.
Nous déclarerons dans ce fichier des règles CSS.

Une règle CSS est composée de deux parties: 

 * un selecteur CSS,
 * un bloc de déclaration.

Par exemple la règle css suivante donne à tous les div la hauteur de 200 pixels et de couleur de fond bleu : 

~~~
div { height:200px;background-color:blue;}
~~~
{.css}

 * le selecteur est `div`,
 * le bloc de déclaration est `height : 200px; background-color:blue;`.

Nous consacrerons plus loin deux sections aux sélecteurs CSS et aux blocs de déclaration.

## L'outil pour les dévellopeurs sur Chrome ou Firefox est votre ami.

Pour la partie HTML c'était votre ami; pour les CSS, il est promu au grade de "best-friend-ever".
Car sélectionner un élement html avec l'outil des dévellopeurs ne permet pas seulement de voir les CSS appliqués à ce dernier, 
il permet aussi de les CHANGER. Autant dire qu'il est conseiller d'abuser de cet outil pendant le TD pour bidouiller tout et n'importe quoi.


## Commentaires

En CSS, seul les commentaires avec `/*` et `*/` sont autorisés.
Si vous utilisez `//` dans votre fichier CSS vous allez avoir des problèmes (les règles CSS suivantes ne seront pas appliquées).

## Bloc de déclaration

### Couleurs

Les mots `aqua`, `black`, `blue`, `fuchsia`, `gray`, `green` ...  peuvent être utilisés pour définir une couleur.
Mais votre palette risque de faire pauvre au final.

Vous pouvez être plus précis et définir une couleur avec le format #RRVVBB ou RR, VV et BB sont les valeurs en hexadécimal de la composante respectivement Rouge, Vert et Bleue.
Comme ces nombres sont en hexadécimal (base 16) sur deux chiffres, les valeurs vont de 00 à FF en passent par A8).

 * `#000000` est noir
 * `#FFFFFF` est blanc
 * `#FF0000` est rouge
 * `#FF00FF` est rose (c'est beau le rose)


Vous pouvez aussi définir les couleurs par les composantes sur 256 valeurs en décimal (de 0 à 255) avec le format suivant `RGB(255,0,255)` (encore du rose !)


Les couleurs peuvent s'utiliser sur plusieurs attributs d'un élément HTML :

 * la couleur du text : color:red;
 * la couleur du fond : background-color:pink;
 * la couleur de bordure : border-color:grey;
 * ...


<a id="dimensions"></a>

### Dimensions

Certains éléments peuvent avoir une taille définie par CSS, d'autres épousent la place minimale nécesssaire à leur rendu.
Cela caractérise entre autres chose des élements inline et block. Nous préciserons ces notions dans le TD suivant, en attendant on s'en tiendra à 
expliciter les unités de dimensions applicables.

L'unité la plus utilisée est le pixel "px" pour pixel CSS. Cette unitée ne compte pas le nombre de pixels physique à l'écran mais est plutôt basée sur une échelle de bonne lisibilité pour le média en cours (i.e il est différent pour un écran d'ordinateur, pour un smartphone, pour une tablette,...).

Pour plus de détails sur ce qu'est cette unité : http://www.w3.org/TR/css3-values/


On peut aussi donner des dimensions relatives en pourcentages.


On utilisera dans le reste du TD des unités de dimensions en px, en se souvenant juste qu'elle convient quelque soit la densité physique 
de pixels de votre média.


### Fontes

référence : http://www.w3.org/TR/CSS21/fonts.html


<b> La propriété font-family</b>

Rajouter maintenant la règle suivante :

~~~
p { font-family: "lucida calligraphy", "Arial", "sans-serif"; }
~~~
{.css}

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
{.css}

<a id="selectors"></a>

## Les Sélecteurs CSS


Les selecteurs CSS permettent de préciser les éléments qui vont être impactés par la règle CSS.
Les selecteurs CSS sont aussi utilisés sur d'autres problématiques du dévellopement Web que nous verrons l'année prochaine.
Bref vous en aurez au partiel, c'est sûr.


On peut construire un sélecteurs CSS complexe à partide selecteurs de bases et de règles de compositions.


{:.css}

### Selecteurs de bases 

Il nous faut completer nos connaissance sur le HTML.
Toutes les balises peuvent se voir adjoindre différents attributs.
Suivant le type (i.e `<span>`, `<div>`, `<a>`,....) des balises, ces attributs auront des sens différents.
Deux attributs sont très important pour les règles CSS : l'id et la class d'un élément.

Par exemple :

~~~
<div id="monidentifiant" class="skill feature" ></div>
~~~
{:.css}


Ce code HTML déclare un élément de type `div` avec comme identifiant unique `monidentifiant` et ayant deux classes : `skill` et `feature`.
Un identifiant est unique pour toute la page HTML. Un élément peut avoir plusieurs classes comme dans l'exemple précédent et ces classes ont du sens si elles sont attribuées à de multiples élement de la page.

Les classes, id et type permettent de construire 95 % des règles CSS.
Voyons la syntaxe pour les utiliser.

#### type

Il s'agit juste d'utiliser le type sans autre décorateur.
si l'on veut donner la couleur rose à tous les liens d'une page, il faut écrire

~~~
a {
  color: pink ;
}
~~~
{.css}


#### id

Le décorateur associé à l'id est le caractère `'#'`.
si l'on veut donner une widht de 100px à notre div déclaré plus haut il faut écrire

~~~
#monidentifiant {
  width: 100px;
}
~~~
{.css}

#### Classes


Le décorateur associé aux classes est le caractère `'.'`.
si l'on veut donner une height de 200px à tous les éléments qui ont la classe `skill`,  il faut écrire

~~~
.skill {
  height: 200px;
}
~~~
{.css}


<a id="select_complex"></a>
### Règles de compositions, Sélecteurs complexes.

Un selecteur CSS peut être plus ou moins compliqué. Sa sémantique peut aller de :

* je vais appliquer la règle à tous les div de la page
* je vais appliquer la règle à tous :
	* les div ayant la class "toto" et qui sont fils d'un élement d'id #titi mais aussi fils directs d'un element de type span.
	* <b>ou</b> l'élement qui a pour id "my_id".

### Pseudo Classes

Pseudo Classes des liens 

~~~
.skill {
a:link {color: yellow;}
a:visited {color: pink;}
~~~
{.css}

Pseudo Classes d'interaction


~~~
.skill {
a:hover {text-decoration: underline;}
~~~
{.css}

#### Les combinaisons (Combinators) 

http://www.w3.org/TR/css3-selectors/#combinators

A partir des sélecteurs de bases précédents, il est possible de créer des sélecteurs complexes.
Nous présentons dans la suite les sélecteurs qui sont utilisés en moyenne 95 % du temps.


#### Regroupement 

La première façon de "composer" des selecteurs et juste le regroupement :

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

On veut parfois préciser un élement au travers de plusieurs sélecteurs de bases sur ce dernier, il suffit pour cela de coller les sélecteurs de base.

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

L'élement qui a la classe toto ET titi.


#### Descendance

Pour discriminer certains éléments sur lequel on veut que porte un selecteur il est très courant de préciser de quoi il est descendant dans le code HTML.
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

Signifie les éléments qui ont la classe toto ET qui sont descendants d'un élement d'id titi.


##### Fréres/adjacents

Les deux élements sont ous deux fils directs d'un même élement.

Par exemple 

~~~
#titi + .toto
~~~
{:.css}

Signifie que l'élement ayant la classe toto et qui est frère de l'élement d'id titi doit avoir son texte en rouge.

## Comment se décline les CSS appliquables sur un site.

Il est possible d'ajouter plusieurs fichiers CSS dans une page et même si l'on n'a qu'un seul fichier, plusieurs règles peuvent être contradictoires.
Pour complexifier le tout, nous verrons que l'on peut ajouter du CSS dit "inline" directement dans le HTML...
et que les navigateurs appliquent des styles par défaut.
Enfin on peut finir une règle CSS avec le code `important!` ce qu'il lui 

### Style par defaut des navigateurs 


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
<li>Style avec le selecteur le plus précis
(si plusieurs fois le même selecteur pour des déclarations non compatibles, la dernière gagne),</li>
<li>Style du navigateur.</li>
</ul>

## CSS et HTML des rôles bien distincts et complémentaires.

Il y a une séparation claire entre les roles du HTML (Contenu) et des CSS (Présentation).
Ce choix n'est pas évident au premier abord : par exemple votre document .odt ou .doc ne sépare pas la présentation du contenu (Votre document Latex oui).
Pour parler des trains qui arrivent à l'heure, il faut dire que cette césure est une idée vraiment formidable.
Elle sous-tend la promesse de pouvoir changer la forme très rapidement sans toucher au fond :

 * Cela permet de changer la présentation du document suivant s'il est destiné à l'impression ou à être rendu par un navigateur, 
 	les unités métriques par exemple ont plus de sens pour une imprimante que pour un écran.
 * Cela permet par exemple de refaire un site web en se concentrant sur les CSS sans (trop) toucher au HTML.
 * Cela permet de réutiliser du css pour des sites dynamiques. Par exemple quand lemonde.fr publie un nouvelle article, on ne refait pas le style expressement pour ce dernier: il s'agit d'un nouveau document HTML partageant le même CSS des articles précédents.


## CSS et HTML, Entre la césure...

Souvent le CSS empiete sur le HTML et inversement. Quand le premier s'en offusque et dit au deuxième de faire attention où il met les pieds, ce dernier répond "je mets pieds où je veux,....".


Car la césure en apparence très nette cache en fait plusieurs entre-deux au travers l'utiliation de certaines balises HTML dénuées de sémantiques (n'ayant qu'un but de présentation) ainsi que la possibilité au travers des styles inlines (du style ajouté directement dans le HTML) de se substituer aux CSS.

## Mon navigateur, mes règles

La complexité des CSS est parfois "artificielle" au sens où elle repose sur de l'existant, sur des différences entre navigateurs.



### Utiliser le HTML pour la présentation

Par le passé, les navigateures étant tous à des degrés différents conformes aux directives CSS.
Il est probable que les intégrateurs ayant eux affaire à Internet Explorer 6 par exemple soient plus souvent chauves que la moyenne.
Il était courant de voir des sites utiliser des tables pour faire des layouts entre autre exemple.
Cela n'et pas forcément du à une méconnaissance de la part de l'intégrateur, mais bien au contraire parfois d'une expertise sur des solutions qui marchent sur des 






