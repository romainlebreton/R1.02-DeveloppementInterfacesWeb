---
title: TD2
subtitle: structuration et stylisation.
layout: tutorial
---


Comme vous avez pu le constater au cours du TD précédent, certains éléments
peuvent cohabiter sur une même ligne et d'autres non. La spécification HTML5
propose différentes manières de classer les balises/éléments selon leurs
caractéristiques
([Liste des balises par catégorie](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)). Nous
allons ici nous intéresser à deux types spécifiques :

* les balises de structure : elles permettent de délimiter l'articulation
  logique de la page web en la découpant en différentes sections. Par défaut,
  ces balises découpent la page web en sections horizontales qu'elles occupent
  en entier (du bord gauche au bord droit de la section). Deux balises de flux
  ne peuvent pas partager une même section horizontale aussi les espaces
  qu'elles délimitent dans la page s'enchaînent-ils verticalement. Elles peuvent
  contenir d'autres balises de structure ou des balises de contenu.

* les balises de contenu : elles permettent de délimiter le texte de la page et
  d'en altérer le formatage. Par défaut, ces balises n'occupent que l'espace
  horizontal minimum nécessaire à afficher le texte qu'elles contiennent, et
  plusieurs balises de contenu peuvent partager une même ligne
  horizontale. Lorsque le contenu d'une de ces balises est trop grand pour tenir
  sur une ligne, il se poursuit automatiquement à la ligne suivante. Les balises
  de contenu peuvent contenir d'autres balises de contenu.

Quelques exemples :

* balises de structure :

   * `<div>` : cette balise est « neutre », à savoir qu'elle permet de distinguer
une section qui ne revêt aucune signification particulière. À utiliser quand
aucune des autres balises de structure ne convient. Typiquement utilisé pour
donner à la page sa structure visuelle à l'aide de règles CSS header : section
contenant l'en-tête affiché de la page
   * `<nav>` : section contenant une série de liens hypertextes pour la navigation
     sur le site
   * `<main>` : section principale de la page, celle qui contient le contenu
     spécifique à cette page. Cette balise ne peut être présente dans une autre
     balise présentée ici à l'exception de « div ». Elle n'est pas supportée par
     Internet Explorer <= 10 mais le support peut en être ajouté grâce à
     Javascript et en utilisant la règle css « main {display : block} ».
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
   * `<p>` : paragraphes du texte
   * `<address>` : coordonnées de contact de l'auteur. Il ne peut y avoir qu'un bloc
     « address » par article et un pour le restant de la page

* balises de contenu :

   * `<span>` : cette balise est neutre, sans signification particulièrement. Permet
     entre autres de créer des règles de formatage spécifiques du contenu
     textuel, par exemple une lettre plus grande pour la 1e lettre d'un
     paragraphe.
   * `<quote>` : une citation
   * `<img>` : une image
   * `<sup>` : un exposant
   * `<time>` : mise en valeur d'une date

## Structuration de la page

Vous allez d'abord structurer logiquement le contenu du site à l'aide des balises de structure.

1. Ajouter une balise `<header>`. Son contenu sera la citation du TD1 et une barre de navigation `<nav>`,
2. Ajouter une balise `<main>` et une balise `<article>` et `<aside>`,
3. Ajouter une balise `<footer>` qui contient le lien vers le retour au début du site.
4. Ajouter dans la balise `<nav>` deux liens :
Un qui pointe sur la page courante ("./index.html") et un qui pointe vers une page contact.html
5. Construire cette page contact.html au même niveau que index.html. Y ajouter l'adresse avec la balise `<adress>`
Contenant  :
 * Email chuckn@caramail.com
 * IUT de Montpellier Sète
 * 99 avenue d'Occitanie
 * 34296 Montpellier Cedex 5
 Ainsi que l'image contanct.jpg pour bien illustrer que nous sommes à l'écoute.


À ce point, le travail de division du site n'a pas encore de résultat visuel
marquant. C'est avant tout un travail de structuration logique qui permet au
navigateur, à un moteur de recherche de mieux comprendre votre page web.
Nous verrons comment structurer la page dans les tds suivants, nous allons ajouter du style aux éléments de la page courante.


## Règles de compositions des CSS


À partir des sélecteurs de bases présentés [dans le TD précédent]({{site.baseurl}}/tutorials/tutorial2.html), il est possible de créer des [sélecteurs complexes](http://www.w3.org/TR/css3-selectors/#combinators), par exemple :

  * les `<div>` ayant la class "toto" et qui sont fils d'un élément d'id #titi mais aussi fils directs d'un élément de type `<span>`.


Nous esposons dans cette section les principaux oyens de composéer un sélecteur css complexe.


### Regroupement 

La première façon de "composer" des sélecteurs est le regroupement :

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


### Combinaison

On veut parfois préciser un élément au travers de plusieurs sélecteurs de bases sur ce dernier, il suffit pour cela de coller les sélecteurs de base. Par exemple :

~~~
div.toto
~~~
{:.css}

Correspond au sélecteur des `<div>` qui ont la classe 'toto'.

Ou encore 

~~~
.titi.toto
~~~
{:.css}

Les éléments qui ont la classe 'toto' ET 'titi'.


### Descendance

Pour discriminer certains éléments sur lequel on veut que porte un sélecteur il est très courant de préciser de quoi il est descendant dans le code HTML.
Pour expliciter ce chemin on ajoute un espace entre les sélecteurs de base.

#### Directe (enfant)


La relation de descendance directe est signifiée par le caractère `>`. Par exemple :

~~~
#titi>.toto
~~~
{:.css}

Correspond au sélecteurs des éléments qui ont la classe 'toto' et qui ont pour parents l'élément d'id 'titi'.

#### Indirecte


La relation de descendance directe est signifiée par le caractère d'espacement. Par exemple :
Par exemple :

~~~
#titi .toto
~~~
{:.css}

Signifie les éléments qui ont la classe toto ET qui sont descendants de l'élément d'id 'titi'.


### Pseudo Classes

Pseudo Classes des liens 

~~~
/*le premier caractère d'un texte*/
p:first-child   {color:red;}

/*le troisième paragraphe */
p:nth-child(3) { color: green;}

/*les textes des éléments li impairs seront verts et les pairs rouges*/
li:nth-child(odd) { color: green;}
li:nth-child(even) { color: red;}

a:link {color: yellow;}
a:visited {color: purple;}
a:hover {text-decoration: underline;}
~~~
{:.css}



### Ordre d'application des sélecteurs CSS.

Nous avons utilisé un ficher de style externe styles.css pour ajouter des règles css.
Il est aussi possible d'ajouter du CSS directement dans le HTML via l'attribut `style` :

~~~
<p style="font-size: 12pt; color: fuchsia">
   Aren't style sheets wonderful?
</p>
~~~
{:.html}

Ou d'inclure des règles css dans une balise `<style>` (internal style):

~~~
<style type="text/css">
   p {font-size: 12pt; color: pink}
</style>
~~~
{:.html}

Enfin les navigateurs appliquent un style par défaut sur les éléments.

L'ordre de priorité d'application des règles css est la suivante :

1. styles 'inline' par l'attribut `style`,
1. styles contenu dans les fichiers css (external style),
1. styles définis dans une balise `<style>` dans le fichier html (internal style),
1. style par défaut des navigateurs.


En pratique on préférera les styles externes comme "styles.css", cela respecte mieux la césure entre la structure HTML et le style css. 

Mais même en ce limitant à un fichier css il est possible d'avoir des règles qui rentrent en conflit :

~~~
div {color: yellow;}
div.toto {color: red;}
~~~
{:.css}

Afin de savoir la couleur qui sera appliquée sur les éléments `<div>`, les sélecteurs css bénéficient d'une priorité.

Cette priorité de spécificitée est une valeur (a,b,c) définie comme cela :
 
 * a est le nombre de sélecteur d'id (`#`),
 * b est le nombre de class (`.`) ou pseudo class (`:over`,`:visited`,...)
 * c est le nombre d'élement contenu dans le sélecteur (`div` , `span`, `p`, ...)

L'ordre de priorité est défini comme lexicographique (la valeur de a est plus discriminante que b qui lui même est plus discriminant que c). 


 1. Faire en sorte que les liens `<a>` visités apparaissent en gris. Lorsque la souris passe sur un lien, lui donner la couleur orange (sauf
s'il a déjà été visité, auquel cas il reste en gris).


## Table

L'élément `<table>` correspond à une structuration récurrente des données, qui sert notamment à comparer des entités sur différentes caractéristiques.

### Les éléments `<table>`, `<tr>`, et `<td>`

L'élément `<table>` contient la table.
La table est composée de ligne (l'élément `<td>`) contenant des cellules (élément `<td>`).


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


1. Créer une table avec les sept noms de colonnes suivants :
```Acteurs, Karaté, Taekwondo, Judo, Chun Kuk Do, Tangsudo, Ju-jitsu```. Les noms doivent être contenus dans des balises ```<span>```
1. Ajouter la classe  "skill" aux ```<span>``` contenant les noms des arts martiaux.
1. Ajouter les six lignes suivantes (les nombres correspondent à la valeur de l'acteur dans l'art martial correspondant) :

     * Chuck Norris, 5, 5, 5, 5, 5, 5
     * Steven Seagal, 3, 5, 3, 2, 3, 5
     * Bruce Lee, 5, 3, 3, 3, 4, 3
     * Jean-Claude Van Damne, 5, 3, 3, 3, 4, 3
     * Bolo Yeung, 2, 4, 4, 2, 5, 3
     * Dolph Lundgren, 2, 4, 4, 2, 5, 3


### Les éléments `<thead>` et `<tbody>`

Les éléments `<thead>` et `<tbody>` servent à définir plus explicitement la structure de notre table:

 * la définition des colonnes (```Acteurs, Karaté,```...) 
 *  les lignes (nos héros et leurs niveaux de compétence).

1. Ajouter ces balises pour englober ces deux parties (en oubliant pas pour se faire leurs balises fermantes ```</thead>``` et ```</tbody>```)


### Les attributs ```rowspan``` et ```colspan``` 

Les attributs ```rowspan``` et ```colspan``` permettent de fusionner les cellules adjacentes :

 * ```rowspan``` permet de fusionner les cellules sur plusieurs lignes (i.e rows),
 * ```collspan``` permet de fusionner les cellules sur plusieurs colonnes.


1. Il apparaît que Chuck Norris est toujours au top (niveau 5) dans tous les martiaux. Fusionner les cellules représentant ses valeurs de manières à 
mettre cela encore plus en exergue.


À ce stade la structure de votre table reflète le sens que vous vouliez y mettre.
Voyons maintenant comment la styliser.

 1. Érivez une règle CSS pour faire apparaître les bords de chaque cellule en
   définissant à *solid* leur propriété *border-style*.
 1. Définissez une couleur de fond #00aaff pour la partie en-tête `thead` du tableau.
 1. Faire en sorte que les noms des acteurs soient maintenant des liens vers leurs pages Wikipedia.
 1. Ajouter une règle pour que les textes dans les colonnes ne soient pas sur plusieurs lignes (notamment 'Chun Kuk Do') en utilisant la bonne valeur pour la propriété `white-space`,
 1. donner la couleur noire aux skill sans modifier le style des éléments ayant la class `skill` dans les paragraphes,
 (voir la [section]({{site.baseurl}}/tutorials/tutorial3.html#rgles-de-compositions-des-css))
 1. ajouter une règle pour qu'un row de la table sur deux apparaisse blanc et l'autre avec la couleur `#CCC` SANS modifier de quelque façon le HTML 
 (voir la [section]({{site.baseurl}}/tutorials/tutorial3.html#rgles-de-compositions-des-css))


## Les contenus flottant :

La propiété float associé à un élément permet de faire flotter ce dernier complètement à gauche ou à droite de la ligne où il se trouve. 
Les valeurs de la propriété float sont  ```left```, ```right```, ```none``` et ```inherit```.

 1. Placer l'image de Chuck jeune de class ```young_chuck``` à gauche du texte, 
 1. Placer l'image beware ```beware_img``` à droite du texte.


## Le modèle de boite

Comme vous l'avez vu précédemment, les balises de type structure définissent des
boîtes. Ces boîtes disposent toutes des propriétés suivantes en CSS :

* padding : marge entre le contenu est la bordure de la boîte. Le padding est de
  la couleur de la boîte, donc il a le même background que la boîte,
* border : bordure qui entoure le contenu,
* margin : marge à l’extérieur de la bordure, entre cette boîte et la
  suivante. La margin est de la même couleur que la balise mère qui encapsule
  celui pour lequel la marge est définie,
* width : la largeur du contenu,
* height : la hauteur du contenu

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodel.png" style="margin:0
auto;display: block;">


A noter que la taille réelle d'une boîte est égale à la taille du content
(width, height) additionnée de l'épaisseur du padding, du bord et de la marge.


### Centrer horizontalement :

Pour centrer le contenu d'une balise :

* si le contenu occupe toute la largeur de la balise : text-align: center
* si le contenu est lui-même dans une balise moins large que la balise parent :
  margin : auto sur la balise du contenu.

 1. Centrer le body horizontalement,
 1. dans la table, le texte des cellules, (le 5 de Chuck notamment est trop discret)
 1. ajouter du padding horizontal de 5 px aux skill dans la table (pas dans les paragraphes)


## Position


 1. Ajouter les icônes de réseaux sociaux toujours positionnées en bas à droite.
 Pour ce faire nous n'allons pas utiliser plusieurs images mais une seule.

