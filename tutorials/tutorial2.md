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


Le css permet de préciser pour chaque élement HTML un style associé.

Si savoir les bases des CSS est relativement facile, en maitriser tous les aspects est un metier (on parle d'integrateur Web).
Il ne s'agit donc pas ici de faire une étude poussée mais bien d'une initiation.

## Tutoriel d'introduction


Une regle CSS est composé de deux parties: 

 * un selecteur CSS
 * un bloc de déclaration


Recopier la règle ci-dessus dans un fichier styles.css à mettre le même répertoire que le
fichier HTML.

Pour indiquer au navigateur qu'il doit utiliser les règles de style de ce fichier pour le document
HTML il faut ajouter la ligne suivante dans l'en-tête du document HTML :

~~~
<link rel=‘stylesheet’ type=‘text/css’ href=‘styles.css’>
~~~
{:.html}


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


### Dimensions

Certains éléments peuvent avoir une taille définie par CSS, d'auter non. Cela caractérise entre autres chose des élements inline et block.

Nous préciserons ces notions dans le TD suivant, en attendant on s'en tiendra à expliciter les unités de dimensions applicables.

Pixels percentages vh,...em...

### Fontes

référence : http://www.w3.org/TR/CSS21/fonts.html


<b> La propriété font-family</b>

Rajouter maintenant la règle suivante :

~~~
p { font-family: "lucida calligraphy", "Arial", "sans-serif"; }
~~~
{.css}

Les dexu dernières fontes précisées par la règle sont des "fall-back" : Si le navigateur ne permet pas d'afficher la fonte "lucida calligraphy" il sera utiliser, "Arial",...et si cette dernière n'est pas disponible alors le "sans-serif" sera utilisé.

<b> la propriété font-size</b>

Utiliser la propriété font-size pour changer la taille de la citation.

### Textes

Tester les règles ci-dessous :

~~~
p {
  text-align: justify ;
  text-indent: 1em;
}

h1 { text-transform : uppercase;}
~~~
{.css}

Aligner la citation en début de document à droite de la page.


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


#### Combinaison

div.toto

#### Descendance

##### Directe

##### InDirecte

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






