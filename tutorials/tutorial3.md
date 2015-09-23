---
title: TD2
subtitle: s
layout: tutorial
---


<!-- modèle de boite + auto -->


Exercice :

4. **Liens visités :** Faire en sorte que les liens visités apparaissent en
gris. Lorsque la souris passe sur un lien, donner lui la couleur orange (sauf
s'il a déjà été visité, auquel cas il reste en gris).
 <!-- Attention -->**On n'a pas parlé des :visited :hover ...

-------------------

La suite et fin des sélecteurs

### Règles de compositions, Sélecteurs complexes

Un sélecteur CSS peut être plus ou moins compliqué. Sa sémantique peut aller de :

* je vais appliquer la règle à tous les div de la page
* je vais appliquer la règle à tous :
	* les div ayant la class "toto" et qui sont fils d'un élément d'id #titi mais aussi fils directs d'un élément de type span.
	* **ou** l'élément qui a pour id "my_id".

### Pseudo Classes

Pseudo Classes des liens 

~~~
.skill {
a:link {color: yellow;}
a:visited {color: purple;}
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


