---
title: TD2
subtitle: s
layout: tutorial
---


<!-- modèle de boite + auto -->


## Exercice :


### Ajouter dans le nav deux liens :
Un qui pointe sur la page courante ("./index.html") et un qui pointe vers une page contact.html


### Box:

 * Centrer le body avec des margin auto



### Position:

 * Ajouter les icônes de réseaux sociaux toujours positionnées en bas à droite.



### Float:

 * Placer l'image de Chuck jeune à gauche du texte, 
 * Placer l'image beware à droite du texte.

### Table

* Créer une table avec les sept noms de colonne suivants :

```Acteurs, Karaté, Taekwondo, Judo, Chun Kuk Do, Tangsudo, Ju-jitsu```


 Avec les six lignes suivantes (les nombres correspondent à la valeur de l'acteur dans l'art martial correspondant) :

     * Chuck Norris, 5, 5, 5, 5, 5, 5
     * Steven Seagal, 3, 5, 3, 2, 3, 5
     * Bruce Lee, 5, 3, 3, 3, 4, 3
     * Jean-Claude Van Damne, 5, 3, 3, 3, 4, 3
     * Bolo Yeung, 2, 4, 4, 2, 5, 3
     * Dolph Lundgren, 2, 4, 4, 2, 5, 3

 * Ajouter la classe span "skill" au noms des arts martiaux.

### Selecteurs Css.

 
 * Ajouter une règle pour que coll span nowrap,
 et la couleur noire aux skill (mais il ne faut pas que votre regle change le style des skill du texte)

 * Faire en sorte que les liens visités apparaissent en
gris. Lorsque la souris passe sur un lien, lui donner la couleur orange (sauf
s'il a déjà été visité, auquel cas il reste en gris).
 

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


# Ancien td 4 &ndash; Les tableaux en HTML

Nous décidons de structurer le contenu de la première section du document
(POST-BAC) à l'aide d'un tableau.

Référence pour ce tp :
[http://www.w3.org/html/wg/drafts/html/CR/tabular-data.html](http://www.w3.org/html/wg/drafts/html/CR/tabular-data.html)

## Les éléments *table*, *tr*, et *td*

Supprimez le contenu de la première section et remplacez-le par le code ci-dessous :

~~~
<table>
   <tr>
      FAC</td>
      Licence</td>
      Informatique</td>
      L'institut Universitaire de Technologie permet aussi à ceux qui ont besoin d'aspect... semaines.</td>
   </tr>
   <tr>
      IUT</td>
      DUT</td>
      GEII</td>
      Le DUT Informatique est le diplôme... cette discipline.</td>
   </tr>
</table>
~~~
{:.html}

Observez le résultat et trouvez un sens aux éléments HTML *table*, *tr* et *td*.

Ecrivez une règle CSS pour faire apparaître les bords de chaque cellule en
définissant à *solid* leur propriété *border-style*.

## L'élément *th*

Dans l'arborescence du document, un élément *th* doit être le fils d'un élément
*tr*. Il représente une cellule en-tête (le titre d'une colonne ou le titre d'une
ligne du tableau). Il peut être utilisé à la place d'un élément *td*.

Ajoutez au tableau les titres de colonne **Composante, Diplôme, Spécialité** et **Le +
du DUT Informatique**.

## Les éléments *thead* et *tbody*

Ajoutez la ligne suivante en dessous de la ligne de titre pour expliciter des
titres de colonne :

| Unité ou Institut | Universitaire | limités aux domaines voisins de l'informatique | avantages du DUT Informatique |

Remarquez que les deux premières lignes constituent un groupement particulier
dans ce tableau, mais qu'à moins de comprendre le sens du contenu des cellule,
rien ne l'indique dans le document. Il est possible de spécifier en HTML cette
structure en utilisant les éléments *thead*, *tbody* ou *tfoot*.

Rattachez dans l'arborescence les deux premières lignes à un même élément *thead*
et les deux autres à un élément *tbody*.

Par défaut cette structuration n'a pas d'implication sur le rendu par le
navigateur mais elle ajoute du sens à la structure.

Définissez un fond gris pour la partie en-tête du tableau.

## L'attribut rowspan

Modifiez le tableau de la façon suivante où on ajoute un établissement non
universitaire :


Etablissement |	Composante | Diplôme | Spécialité |	Le + du DUT Informatique
 | Unité, Institut, Section | | limités aux domaines voisins de l'informatique | 
Université | FAC | Licence | Informatique | 
Université | IUT | DUT | GEII | 
Lycée | STS | BTS | SIO | 

Il faudrait fusionner les deux cellules "Université" dans la première
colonne. Supprimez pour cela la deuxième occurrence et définir l'attribut
*rowspan* de la première avec la valeur 2.

Vérifiez la validité.

## L'attribut colspan

Ajoutez une sixième ligne au tableau :

Etablissement |	Composante | Diplôme | Spécialité |	Le + du DUT Informatique
 | Unité, Institut, Section | | limités aux domaines voisins de l'informatique | 
Université | FAC | Licence | Informatique | 
Université | IUT | DUT | GEII | 
Lycée | STS | BTS | SIO | 
Ecole privée | sans objet | Bachelor | Informatique | Formation gratuite, diplôme Universitaire et National

Utilisez l'attribut *colspan* pour fusionner les deux premières cellules de la
dernière ligne en conservant uniquement le contenu de la première.

Vérifiez la validité de votre document.

## Pour les plus avancés

1. Remplacez ce tableau par le tableau du document *etudes2_tableau.pdf*
1. Avancez sur votre projet

