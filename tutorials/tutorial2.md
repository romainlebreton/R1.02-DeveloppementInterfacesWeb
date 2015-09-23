---
title: TD1 Partie 2 &ndash; Les bases du CSS
subtitle: Un langage de mise en page
layout: tutorial
---

Les standards définissant le CSS sont publiés par le World Wide Web Consortium
(<a href="http://www.w3.org/">W3C</a>).

<!-- lien pour HTML et compléter le lien pour CSS -->


> <i>Cascading Style Sheets (CSS) est un mécanisme simple pour ajouter du style
> (exemple fonte, couleurs, espace) à un document web.</i>  
> <cite><a href="http://www.w3.org/Style/CSS/">W3C</a></cite>

Le CSS est responsable du rendu du site sur votre écran, mais aussi sur un
smartphone et des impressions papier (des ensembles de règles CSS peuvent être
spécifiés pour chacun de ces médias).


Bien que l'acronyme signifie donc **des** feuilles de style, on parlera
**du** CSS (le langage utilisé ou le mécanisme), mais on ne fera pas les pédants
tant les deux sont confondus à l'usage (l'usage fait très souvent loi lorsque
l'on fait du CSS !).

Savoir les bases du CSS est relativement facile et indispensable pour qui veut
travailler dans les métiers du Web. En maîtriser tous les aspects est un métier
(celui d'intégrateur Web, qui traduit en HTML et CSS le travail du
Web-designer).

## Tutoriel d'introduction

Nous allons travailler principalement sur ce TD sur un fichier `styles.css`.
Créer ce fichier à partir du fichier `index.html` dans le répertoire `css/`.

Dans le fichier `index.html`, il faut ajouter la ligne suivante dans l'en-tête du
document HTML (dans la partie `head`) :

~~~
<link rel="stylesheet" type="text/css" href="css/styles.css">
~~~
{:.html}


Nous déclarerons dans ce fichier des règles CSS.

Une règle CSS est composée de deux parties: 

 * un sélecteur CSS,
 * un bloc de déclaration.

Par exemple la règle CSS suivante donne à tous les `h3` le style italique et défini comme couleur de texte le bleu : 

~~~
h3 {  font-style:italic;color:blue;}
~~~
{:.css}

 * le sélecteur est `h3`,
 * le bloc de déclaration est `font-style:italic;color:blue;`.


 Nous allons plus amplement présenter quelques blocs de
 [déclarations](#bloc-de-dclaration) et la façon de concevoir des
 [sélecteurs](#les-slecteurs-css).  Nous passerons ensuite à la mise en pratique
 dans la section [Exercices](#exercices).


## Les outils de développement sont vos amis

Pour la partie HTML, les outils de développement étaient déjà vos amis ; pour le
CSS, ils sont promus au grade de "best-friend-forever".  Sélectionner un élément
HTML avec les outils de développement ne permet pas seulement de voir les règles
CSS appliquées à ce dernier, il permet aussi de les **changer**. Autant dire
qu'il est conseillé d'abuser de cet outil pendant le TD pour bidouiller tout et
n'importe quoi.

## Commentaires

En CSS, seuls les commentaires avec `/*` et `*/` sont autorisés.  Si vous
utilisez `//` dans votre fichier `styles.css` vous allez avoir des problèmes
(les règles CSS suivantes ne seront pas appliquées).


## Bloc de déclaration


Les blocs de déclarations portent sur des ensembles "`attributs:valeur`" séparés
par des "`;`" (exemple `height:200px;background-color:blue;`).  Nous présentons
ici quelques exemples valides de valeurs et des attributs associés.

### Couleurs

Les couleurs peuvent s'utiliser sur plusieurs attributs d'un élément HTML :

 * la couleur du texte : `color:red`;
 * la couleur du fond : `background-color:#FF00FF`;
 * la couleur de la bordure : `border-color:#F0F` ...

Les 16 mots clés suivants peuvent être utilisés pour définir une couleur :
`aqua`, `gray`, `navy`, `silver`, `black`, `green`, `olive`, `teal`, `blue`,
`lime`, `purple`, `white`, `fuchsia`, `maroon`, `red`, `yellow`. Ils ont été
choisis pour désigner 16 couleurs bien réparties comme le montre le diagramme
suivant :

<div style="text-align:center">
![Symétrie des 16 couleurs]({{site.baseurl}}/assets/HSL14colors.png).
</div>

Le CSS3 les a complétés par 147 mots-clés de couleurs que vous pouvez retrouver
à l'adresse
[http://www.w3.org/TR/css3-color/#svg-color](http://www.w3.org/TR/css3-color/#svg-color).

Vous pouvez être plus précis et définir une couleur avec le format #RRVVBB ou
#RVB. R, V et B sont les valeurs en hexadécimal des composantes Rouge, Verte et
Bleue respectivement.

 * `#000000` est noir,
 * `#FFFFFF` est blanc,
 * `#F00`, qui est un raccourci pour `#FF0000`, est rouge,
 * `#FF00FF` est rose, que l'on peut aussi accéder avec le mot clé `pink`.

### Dimensions

Certains éléments peuvent avoir une taille définie par CSS, d'autres épousent la
place minimale nécessaire à leur rendu.
<!-- Cela caractérise entre autres choses des éléments inline et block.  Nous -->
<!-- préciserons ces notions dans le TD suivant, en attendant on s'en tiendra à -->
<!-- expliciter les unités de dimensions applicables. -->

L'unité absolue de mesure la plus utilisée est le "pixel CSS" `px`. Cette unité
correspond souvent avec les pixels physiques de l'écran mais avec certaines
subtilités. Premièrement, les navigateurs actuels permettent de zoomer, ce qui a
pour effet d'afficher un "pixel CSS" sur plusieurs pixels. Deuxièmement,
certains médias comme l'imprimante ne disposent pas de pixels ; le pixel CSS est
alors défini comme une échelle permettant une bonne lisibilité sur le média.  
Pour plus de détails sur ce qu'est cette unité :
[http://www.w3.org/TR/css3-values/#absolute-lengths](http://www.w3.org/TR/css3-values/#absolute-lengths)

<!-- les autres unitées sont in cm mm pt pc => font de plus de sens pour
d'autres médias-->
<!-- D'autres unités de mesures sont possibles (`pt`, `cm`, ...), mais nous nous en
tiendrons aux `px`  -->

On peut aussi donner des dimensions relatives en pourcentages ; `width:50%` va
diminuer de moitié la largeur par rapport à celle qui aurait été calculée
normalement.
<!-- 50 % de quoi ? De la taille calculée normalement -->

<!-- Parle-t-on de em ex rem ch viewport-width ... -->

<!--
First, let’s consider em and ex , which are closely related. In CSS, one “em” is defined to
be the value of font-size for a given font. If the font-size of an element is 14 pixels,
then for that element, 1em is equal to 14 pixels.
Obviously, this value can change from element to element. For example, let’s say you
have an h1 with a font size of 24 pixels, an h2 element with a font size of 18 pixels, and
a paragraph with a font size of 12 pixels. If you set the left margin of all three at 1em ,
they will have left margins of 24 pixels, 18 pixels, and 12 pixels, respectively:
h1 {font-size: 24px;}
h2 {font-size: 18px;}
p {font-size: 12px;}
h1, h2, p {margin-left: 1em;}
small {font-size: 0.8em;}
<h1>Left margin = <small>24 pixels</small></h1>
<h2>Left margin = <small>18 pixels</small></h2>
<p>Left margin = <small>12 pixels</small></p>
-->


Les dimensions sont utilisées sur différentes parties d'un élément.
**Exemple :**

~~~ 
.ma_class {
  height:150px;
  width:50px;
  padding:15px;
  border-width:1px;
}
~~~
{:.css}

<!-- padding -->

### Fontes

Nous allons lister ici les propriétés les plus utilisées sur les fontes :

1. **`font-family` :** Cette propriété permet de choisir la fonte que vous
   souhaitez utiliser. Exemple :

   ~~~
   font-family: "Lucida Sans Unicode", "Arial", "sans-serif";
   ~~~
   {:.css}

   **Important :** Les deux dernières fontes précisées par la règle sont des
fontes de secours (fallback) : elles seront utilisées si et seulement si les
précédentes ne sont pas disponibles sur le navigateur. Quelques fontes
classiques sont répertoriées sur
[http://www.w3schools.com/cssref/css_websafe_fonts.asp](http://www.w3schools.com/cssref/css_websafe_fonts.asp).

1. **`font-size` :** Cette propriété permet de définir la taille de la police. Exemple :

   ~~~
   font-size:12px;
   ~~~
   {:.css}

1. **`font-weight` :** Cette propriété permet de passer en mode **gras**. Exemple :

   ~~~
   font-weight:bold;
   ~~~
   {:.css}

1. **`font-style` :** Cette propriété permet de définir le style de la fonte
   (*i.e.* italique ou non). Exemple :

   ~~~
   font-style:italic;
   ~~~
   {:.css}


**Référence :** [http://www.w3.org/TR/CSS21/fonts.html](http://www.w3.org/TR/CSS21/fonts.html) et [http://www.w3.org/TR/css-fonts-3/](http://www.w3.org/TR/css-fonts-3/).

**Note optionnelle :** Vous pouvez associer à votre page Web de nouvelles fontes
  à l'aide de la règle `@font-face`. Exemple :

~~~
@font-face {
    font-family: myFont;
    src: url(path/to/font/font.otf);
}
~~~
{:.css}

Si vous souhaitez en savoir plus, allez sur
[https://developer.mozilla.org/fr/docs/Web/CSS/@font-face](https://developer.mozilla.org/fr/docs/Web/CSS/@font-face). Voici
deux sites pratiques pour télécharger de nouvelles fontes : 
[http://www.1001fonts.com](http://www.1001fonts.com) et 
[http://www.fontsquirrel.com](http://www.fontsquirrel.com).

### Textes

Nous allons lister ici les propriétés les plus utilisées concernant l'affichage
des paragraphes de texte :

1. **`text-align` :** Cette propriété affecte l'alignement des lignes de texte. Exemple :

   ~~~
   text-align:center; \* ou left, right, justify *\
   ~~~
   {:.css}
   
   Pour rappel, un paragraphe justifié est un paragraphe où les lignes s'arrêtent à
   la marge à droite et à gauche.

1. **`line-height` :** Cette propriété permet d'espacer vertivalement les lignes
   de texte. Exemple :

   ~~~
   line-height:150%;
   ~~~
   {:.css}
   
1. **`text-indent` :** Cette propriété indente la première ligne du texte,
   c'est-à-dire qu'elle la décale horizontaliement. Exemple :

   ~~~
   text-indent:12px;
   ~~~
   {:.css}

   <!--  text-indent:1em; serait plus naturel -->

   Si l'on donne un pourcentage comme valeur de `text-indent`, celui-ci est
   compris comme un pourcentage de la largeur de l'élément parent.

## Les sélecteurs CSS de base

Les sélecteurs CSS permettent de préciser les éléments qui vont être impactés
par la règle CSS.  Ils sont aussi utilisés sur d'autres problématiques du
développement Web que nous verrons l'année prochaine.  Bref vous en aurez au
partiel, c'est sûr.

Comme vous le savez depuis le
[TD1 HTML]({{site.baseurl}}/tutorials/tutorial1.md) une balise peut prendre des
attributs. Deux attributs sont très importants pour les règles CSS :
l'identifiant `id` et la classe `class` d'une balise.

Par exemple :

~~~
<div id="monidentifiant" class="skill feature">...</div>
~~~
{:.html}

Ce code HTML déclare un élément de type `div` avec comme identifiant unique
`monidentifiant` et ayant deux classes : `skill` et `feature`.  Un identifiant
est unique pour toute la page HTML. Un élément peut avoir plusieurs classes
comme dans l'exemple précédent et ces classes sont faites pour être attribuées à
de multiples éléments de la page.

Les classes, identifiant et le type des balises permettent de construire 95 % des sélecteurs
CSS de base. Voyons la syntaxe pour les utiliser.

### Les sélecteurs de balises

Il s'agit juste d'utiliser le nom de la balise (`a`, `p`, `img`,...) sans autre
décorateur. Si on veut donner la couleur rose à tous les liens d'une page, il
faut écrire

~~~
a {
  color: purple ;
}
~~~
{:.css}


### Les sélecteurs d'identifiant

Le décorateur associé à l'identifiant est le caractère `'#'`. Si on veut
donner une largeur de `100px` à l'unique balise d'identifiant `monidentifiant`,
il faut écrire

~~~
#monidentifiant {
  width: 100px;
}
~~~
{:.css}

### Les sélecteurs de classes

Le décorateur associé aux classes est le caractère `.`. Si on veut donner une
hauteur de `200px` à tous les éléments qui ont la classe `skill`, il faut écrire

~~~
.skill {
  height: 200px;
}
~~~
{:.css}

## Exercices 

<!--
Exercice sur les outils de développement : changer temporairement la
couleur des codes, la marge des blocs de codes, la taille de la police, ...
-->

Tout va principalement se passer dans `styles.css`.

1. **Couleurs :** Le fond de notre page est tout blanc par défaut. Nous allons
changer cela en donner au `<body>` la couleur qu'à choisi le graphiste / Web-designer :
`#838892`.  
2. Conformément à la maquette du designer [target.png]({{site.baseurl}}/assets/target.png), il faut alterner comme couleurs de fonds pour les titres des sections les valeurs #5BBDBF et #FF5850.
Pour cela il nous faudra rajouter une classe "pair" et "impair" aux elements `h2` et `h3` et leurs associés le style adéquat dans styles.css.

2. **Dimensions :** plusieurs études (cf.
[1](https://viget.com/inspire/the-line-length-misconception) et
[2](https://en.wikipedia.org/wiki/Line_length) ) suggèrent que des lignes trop
longues ou trop courtes nuisent gravement à la lisibilité d'un site. Pour
traiter grossièrement le problème, limitez la largeur de l'élément `<body>` à
`600px`.

   <!--
   > Le centrer au milieu avec des marges auto, lui donner du padding et une
   > line-height de 150%
   On n'a pas parlé de marge, de padding ni de ligne-height pour l'instant !!!
   -->


3. L'image `beware.jpg` a du style, mais elle prend un peu trop de place : 
limitez sa hauteur à 300px.

   <!--
   > H2 et H3 du padding et du border radius
   Pas abordé !!!
   -->

4. Les titres des sections doivent avoir leur texte centré.

5. le texte doit être aéré : utiliser une hauteur de ligne de 150%.

6. Chaque paragraphe doit être indenté de 5px.

3. Allez chercher une fonte de votre choix sur http://www.fontsquirrel.com/ et appliquez-la aux
   titres de section `<h2>` en n'oubliant pas de mettre des fontes en *fall-back* (fonte de
   recours ).

5. On veut mettre en avant les innombrables arts martiaux que maîtrise Chuck
   Norris. Pour ce faire, on va entourer chacun de ces arts martiaux (Taekwondo,
   Ju-Jitsu, ...) d'une balise `<span>` avec la classe `skill` dans le fichier
   HTML. D'un autre côté, il faut créer dans le CSS la règle qui associe à la
   classe `skill` la mise en page suivante : texte en rouge et en italique (ou
   ce qui vous fait plaisir).

<!--
Exercices avec les fontes ou le texte (text-align, line-height, text-indent) ?
-->

<!--
Bord rond : sans encore parler de box model
-->

## CSS et HTML des rôles bien distincts et complémentaires

Il y a une séparation claire entre les rôles du HTML (Contenu avec des balises
pour donner du sens ) et des CSS (présentation / mise en page). Ce choix n'est
pas évident au premier abord : par exemple votre document "Word" ne sépare pas
la présentation du contenu. Mais cette séparation est indispensable et très puissante :

 * Elle permet de changer la présentation d'un document suivant s'il est destiné à
 	l'impression ou à être visualisé avec un navigateur ; 
 * Elle permet de refaire un site Web en se concentrant sur les CSS sans (trop)
   toucher au HTML ;
 * Elle permet de réutiliser une présentation d'une page à l'autre. Par exemple
   quand *lemonde.fr* publie un nouvel article, il ne refait pas le style
   expressément pour ce dernier: il s'agit d'un nouveau document HTML partageant
   le même CSS que les articles précédents.

<!--
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
directives CSS. Il est probable que les intégrateurs ayant eu affaire à
Internet Explorer 6 par exemple soient plus souvent chauves que la moyenne.  Il
était courant de voir des sites utiliser des tables pour faire des layouts entre
autre exemple.  Cela n'est pas forcément du à une méconnaissance de la part de
l'intégrateur, mais bien au contraire parfois d'une expertise sur des solutions
qui marchent sur des navigateurs mais pas sur d'autres.

-->
