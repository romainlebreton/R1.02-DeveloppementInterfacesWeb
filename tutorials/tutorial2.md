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
<link rel=‘’stylesheet’’ type=‘’text/css’’ href=‘’styles.css’’>
~~~
{:.html}


## L'outil pour les dévellopeurs sur Chrome ou Firefox est votre ami.

Pour la partie HTML c'était votre ami; pour les CSS, il est promu au grade de "best-friend-ever".
Car sélectionner un élement html avec l'outil des dévellopeurs ne permet pas seulement de voir les CSS appliqués à ce dernier, 
il permet aussi de les CHANGER. Autant dire qu'il est conseiller d'abuser de cet outil pendant le TD pour bidouiller tout et n'importe quoi.


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

### Fontes

référence : http://www.w3.org/TR/CSS21/fonts.html


<b> La propriété font-family</b>

Rajouter maintenant la règle suivante :

~~~
p{ font-family: "lucida calligraphy", "Arial", "sans-serif"; }
~~~
{.css}

Les trois fontes préciser par la règle ne vont pas fusionner. Leur ordre défini juste la précédence en fonction des disponibilités sur le navigateur.
Si le navigateur permet d'afficher du "lucida calligraphy" il sera utiliser, sinon le "Arial",...et sinon le "sans-serif".

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

## Sélecteurs



On peut avoir plusieurs selecteurs CSS et plusieurs bloc de déclaration pour une même règle CSS.

Par exemple  : la règle ci-contre permet de définir deux blocs de déclarations `color:red` et `background:white`.
Cela produira des titres de couleur rouge sur fond blanc.
Enfin cette règle s'applique via le selecteur `h1` sur les balises... `<h1>` :

~~~
h1 {
  color: red;
  background: white
}
~~~
{:.css}


### Selecteurs de bases 


#### type


#### id


#### Classes

Côté HTML on peut assigner un élément à une classe en définissant pour cet élément son attribut
class :

~~~
<p class="important"> Texte du paragraphe... </p>
~~~
{:.html}

Il est alors possible de définir un style pour un sous-ensemble (une classe) d'éléments de même
type. Par exemple la règle ci-dessous ne concerne que les paragraphes appartenant à la classe des
paragraphes importants :

~~~
p.important{ border-style: solid }
~~~
{:.css}


#### Pseudo-Classes



### Selecteur complexes 



#### Regroupement
Un selecteur CSS peut être plus ou moins compliqué. Sa sémantique peut aller de :

* je vais appliqué la règle à tous les div
* je vais appliqué la règle à tous :
	* les div ayant la class "toto" et qui sont fils d'un élement d'id #titi mais aussi fils directs d'un element de type span.
	* ou qui ont l'id "my_id".


Il est possible de regrouper les sélecteurs :

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

### Style par defaut des navigateurs 

(reset CSS),

### Style inline,

### Styles dans un fichier css,

### ordre de priorité de tout cela ?

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






