---
title: TD1 Partie 2 &ndash; Les bases du CSS
subtitle: Un langage de mise en page
layout: tutorial
---

Les standards définissant le CSS sont publiés par le World Wide Web Consortium
(<a href="http://www.w3.org/">W3C</a>) à l'adresse
[http://www.w3.org/Style/CSS/](http://www.w3.org/Style/CSS/).

> Cascading Style Sheets (CSS) est un mécanisme simple pour ajouter du style
> (exemple fonte, couleurs, espace) à un document web.  
> <cite><a href="http://www.w3.org/Style/CSS/">W3C</a></cite>

Le CSS est responsable du rendu du site sur votre écran, mais aussi sur
smartphone et des impressions papier (des ensembles de règles CSS peuvent être
spécifiés pour chacun de ces médias).

<!-- Bien que l'acronyme signifie donc **des** feuilles de style, on parlera -->
<!-- **du** CSS (le langage utilisé ou le mécanisme), mais on ne fera pas les pédants -->
<!-- tant les deux sont confondus à l'usage (l'usage fait très souvent loi lorsque -->
<!-- l'on fait du CSS !). -->

Savoir les bases du CSS est relativement facile et indispensable pour qui veut
travailler dans les métiers du Web. En maîtriser tous les aspects est un métier
(celui d'intégrateur Web, qui traduit en HTML et CSS le travail du
Web-designer).

## Tutoriel d'introduction

Voici un exemple de règle CSS

```css
h3 {
  font-style:italic;
  color:blue;
}
```

Cette règle CSS donne à toutes les balises `<h3>` le style
italique et défini comme couleur de texte le bleu.

Une règle CSS est composée de deux parties: 

* un sélecteur CSS qui indique à quels éléments HTML s'applique le style. Dans
   notre exemple, le sélecteur `h3` signifie que nous allons appliquer le style
   suivant à toutes les balises HTML `<h3>` ;
* un bloc de déclarations composé de plusieurs paires propriété CSS /
 valeur. Dans notre exemple, le bloc contient deux déclarations :
  1. nous donnons la valeur `italic` à la propriété CSS `font-style`;
  1. nous donnons la valeur `blue` à la propriété CSS `color`.

<div class="exercise">

Mettons en place nos règles CSS :

1. Nous allons travailler principalement sur ce TD sur un fichier `styles.css`.
Créer un fichier texte vide `styles.css` dans un nouveau répertoire `css/`.
Nous déclarerons dans ce fichier des règles CSS.

1. Copiez dans `styles.css` le style ci-dessus `h3 { ... }`.  
   Ouvrez la page `index.html` et remarquez que le style ne s'est pas appliqué
   car nous n'avons pas encore lié le HTML avec le CSS.

2. Dans le fichier `index.html`, ajouter la ligne suivante dans l'en-tête du
document HTML (dans la partie `head`) :

   ```html
   <link rel="stylesheet" type="text/css" href="css/styles.css">
   ```

   Cette ligne permet de charger le fichier de style CSS `styles.css` et de
   l'appliquer à la page Web.

3. Réouvrez la page `index.html` et notez que le style est désormais appliqué.

</div>


Nous allons vous présenter quelques [propriétés CSS](#quelques-propriétés-css) et la
façon de concevoir des [sélecteurs](#les-sélecteurs-css-de-base).

## Les outils de développement sont vos amis

Pour la partie HTML, les outils de développement étaient déjà vos amis ; pour le
CSS, ils sont promus au grade de "best-friend-forever".  Sélectionner un élément
HTML avec les outils de développement ne permet pas seulement de voir les règles
CSS appliquées à ce dernier, il permet aussi de les **changer**. Autant dire
qu'il est conseillé d'abuser de cet outil pendant le TD pour bidouiller tout et
n'importe quoi.

<div class="exercise">

1. Inspectez avec les outils de développement (`F12`) l'un des textes en
rouge. Dans la colonne de droite, vous voyez les styles CSS appliqués à cette
balise.

2. Désactiver la déclaration `color:#d00` et remarquez le changement.

3. Remarquez que vos changements disparaissent quand vous rafraîchissez la page
   (`F5`). En effet, il faut les reporter dans la feuille de style pour les
   sauvegarder.

</div>

<!--
Exercice sur les outils de développement : changer temporairement la
couleur des codes, la marge des blocs de codes, la taille de la police, ...
-->


## Commentaires

En CSS, seuls les commentaires avec `/*` et `*/` sont autorisés.  Si vous
utilisez `//` dans votre fichier `styles.css` vous allez avoir des problèmes
(les règles CSS suivantes ne seront pas appliquées).
 
<div class="exercise">

Commentez la règle CSS `h3 { ... }` dans `styles.css` et remarquez que les
titres `<h3>` ne sont plus en bleu ni en italique.

</div>

## Quelques propriétés CSS

Comme dit précédemment, les blocs de déclarations comportent plusieurs
déclarations de la forme `proprieteCSS:valeur;`.  Nous présentons ici quelques
exemples de propriétés CSS et de valeurs associées.

### Couleurs

Les couleurs peuvent s'utiliser sur plusieurs attributs d'un élément HTML :

 * la couleur du texte : `color:red;`
 * la couleur du fond : `background-color:blue;`
 * la couleur de la bordure : `border-color:yellow;` ...

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

Vous pouvez être plus précis et accéder aux 16 millions de couleurs que peut
afficher un écran en donnant les valeurs `R`, `V` et `B` en hexadécimal des
composantes Rouge, Verte et Bleue respectivement de la couleur. Cela s'écrit
avec le format `#RRVVBB` (ou `#RVB` qui est un raccourci). Par exemple :

 * `#000000` est noir,
 * `#FFFFFF` est blanc,
 * `#F00`, qui est un raccourci pour `#FF0000`, est rouge,
 * `#FF00FF` est rose, que l'on peut aussi accéder avec le mot clé `pink`.

**Remarque :** Vous pouvez utiliser le site Web
  [http://www.colorpicker.com/](http://www.colorpicker.com/) pour trouver
  facilement le code `#RRVVBB` de n'importe quelle couleur.

### Dimensions

Certains éléments peuvent avoir une taille définie par CSS, d'autres épousent la
place minimale nécessaire à leur rendu.

L'unité absolue de mesure la plus utilisée est le "pixel CSS" `px`. Cette unité
correspond souvent avec les pixels physiques de l'écran mais avec certaines
subtilités :

1. les navigateurs actuels permettent de zoomer, ce qui a pour effet d'afficher
un "pixel CSS" sur plusieurs pixels.
2. certains médias comme l'imprimante ne disposent pas de pixels ; le pixel CSS
est alors défini comme une échelle permettant une bonne lisibilité sur le média.  

Les dimensions sont utilisées sur différentes parties d'un élément. Par exemple,
les propriétés CSS `width` et `height` permettent de forcer respectivement la
largeur et la hauteur d'un élément (ici les balises `<img>`) :

```css
img {
    width:50px;
    height:100px;
}
```

On peut aussi donner des dimensions relatives en pourcentages ; `width:50%` va
diminuer de moitié la largeur par rapport à celle qui aurait été calculée
normalement.

**Référence :** Pour plus de détails sur les unités disponibles
[http://www.w3.org/TR/css3-values/#absolute-lengths](http://www.w3.org/TR/css3-values/#absolute-lengths)
<!-- les autres unitées sont in cm mm pt pc => font de plus de sens pour
d'autres médias-->

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

### Fontes

Nous allons lister ici les propriétés les plus utilisées sur les fontes :

1. **`font-size` :** Cette propriété permet de définir la taille de la police. Exemple :

   ```css
   font-size:12px;
   ```

1. **`font-weight` :** Cette propriété permet de passer en mode **gras**. Exemple :

   ```css
   font-weight:bold;
   ```

1. **`font-style` :** Cette propriété permet de définir le style de la fonte
   (*i.e.* italique ou non). Exemple :

   ```css
   font-style:italic;
   ```

1. **`font-family` :** Cette propriété permet de choisir la fonte que vous
   souhaitez utiliser. Exemple :

   ```css
   font-family: "Lucida Sans Unicode", "Arial", "sans-serif";
   ```

   **Important :** Les deux dernières fontes précisées par la règle sont des
fontes de secours (fallback) : elles seront utilisées si et seulement si les
précédentes ne sont pas disponibles sur le navigateur. Quelques fontes
classiques sont répertoriées sur
[http://www.w3schools.com/cssref/css_websafe_fonts.asp](http://www.w3schools.com/cssref/css_websafe_fonts.asp).


**Importer de nouvelles fontes :** Vous pouvez associer à votre page Web de
  nouvelles fontes à l'aide de la règle `@font-face`. Exemple :

```css
@font-face {
    font-family: myFontName;
    src: url(path/to/font/font.otf);
}
```

<!--
L'URL est relative au fichier CSS
Attention aux extensions non reconnues par Firefox (comme .eot)
-->

Si vous souhaitez en savoir plus, allez sur
[https://developer.mozilla.org/fr/docs/Web/CSS/@font-face](https://developer.mozilla.org/fr/docs/Web/CSS/@font-face). Voici
deux sites pratiques pour télécharger de nouvelles fontes : 
[http://www.1001fonts.com](http://www.1001fonts.com) et 
[http://www.fontsquirrel.com](http://www.fontsquirrel.com).

**Référence :**
  [http://www.w3.org/TR/CSS21/fonts.html](http://www.w3.org/TR/CSS21/fonts.html)
  et [http://www.w3.org/TR/css-fonts-3/](http://www.w3.org/TR/css-fonts-3/).

### Textes

Nous allons lister ici les propriétés les plus utilisées concernant l'affichage
des paragraphes de texte :

1. **`text-align` :** Cette propriété affecte l'alignement des lignes de texte. Exemple :

   ```css
   text-align:center; /* ou left, right, justify */
   ```
   
   Pour rappel, un paragraphe justifié est un paragraphe où les lignes s'arrêtent à
   la marge à droite et à gauche.

1. **`line-height` :** Cette propriété permet d'espacer verticalement les lignes
   de texte. Exemple :

   ```css
   line-height:150%;
   ```
   
1. **`text-indent` :** Cette propriété indente la première ligne du texte,
   c'est-à-dire qu'elle la décale horizontalement. Exemple :

   ```css
   text-indent:12px;
   ```

   <!--  text-indent:1em; serait plus naturel -->

   Si l'on donne un pourcentage comme valeur de `text-indent`, celui-ci est
   compris comme un pourcentage de la largeur de l'élément parent.

### Exercices

1. **Couleurs :** Le fond de notre page est tout blanc par défaut. Nous allons
changer cela en donnant au `<body>` la couleur qu'a choisi le graphiste / Web-designer :
`#838892`.  

2. **Dimensions :** plusieurs études (cf.
[1](https://viget.com/inspire/the-line-length-misconception) et
[2](https://en.wikipedia.org/wiki/Line_length) ) suggèrent que des lignes trop
longues ou trop courtes nuisent gravement à la lisibilité d'un site. Pour
traiter grossièrement le problème, limitez la largeur de l'élément `<body>` à
`600px`.

4. Les titres des sections doivent avoir leur texte centré.

5. le texte doit être aéré : utiliser une hauteur de ligne de `150%`.

6. Chaque paragraphe doit être indenté de `5px`.

3. Allez chercher une fonte de votre choix sur
   [http://www.fontsquirrel.com](http://www.fontsquirrel.com). Liez-là à votre
   document avec la règle `@font-face`. Appliquez-la aux titres de section
   `<h2>` en n'oubliant pas de mettre des fontes en *fallback* (fonte de
   recours).  
   **Attention :** Ne mettez pas d'espaces dans le nom de votre fonte, ou sinon
   entourez-là avec des guillemets.

10. Le CSS est un standard au même titre que le HTML. Testez la conformité de
    votre fichier CSS avec le validateur
    [https://jigsaw.w3.org/css-validator](https://jigsaw.w3.org/css-validator).


## Les sélecteurs CSS de base

Les sélecteurs CSS permettent de préciser les éléments qui vont être impactés
par la règle CSS.  Ils sont aussi utilisés sur d'autres problématiques du
développement Web que nous verrons l'année prochaine.  Bref vous en aurez au
partiel, c'est sûr.

Comme vous le savez depuis le
[TD1 HTML]({{site.baseurl}}/tutorials/tutorial1_1) une balise peut prendre des
attributs. Deux attributs sont très importants pour les règles CSS :
l'identifiant `id` et la classe `class` d'une balise.

Par exemple :

```html
<h2 id="monidentifiant" class="skill feature">...</h2>
```

Ce code HTML déclare une balise HTML `<h2>` avec comme identifiant unique
`monidentifiant` et ayant deux classes : `skill` et `feature`. **Attention**, un
identifiant est unique pour toute la page HTML. Un élément peut avoir plusieurs
classes comme dans l'exemple précédent et ces classes sont faites pour être
attribuées à de multiples éléments de la page.

Les classes, identifiant et le type des balises permettent de construire 95 % des sélecteurs
CSS de base. Voyons la syntaxe pour les utiliser.

### Les sélecteurs de balises

Il s'agit juste d'utiliser le nom de la balise (`a`, `p`, `img`,...) sans autre
décorateur. Si on veut donner la couleur rose à tous les liens d'une page, il
faut écrire

```css
a {
  color: purple ;
}
```


### Les sélecteurs d'identifiant

Le décorateur associé à l'identifiant est le caractère `'#'`. Si on veut
donner une largeur de `100px` à l'unique balise d'identifiant `monidentifiant`,
il faut écrire

```css
#monidentifiant {
  width: 100px;
}
```

### Les sélecteurs de classes

Le décorateur associé aux classes est le caractère `.`. Si on veut donner une
hauteur de `200px` à tous les éléments qui ont la classe `skill`, il faut écrire

```css
.skill {
  height: 200px;
}
```

### Exercices 

Tout va principalement se passer dans `styles.css`.

2. Conformément à la maquette du designer
[target.png]({{site.baseurl}}/assets/target.png), il faut alterner comme
couleurs de fonds pour les titres des sections les valeurs `#5BBDBF` et
`#FF5850`.  Pour cela il nous faudra rajouter une classe "pair" et "impair" aux
éléments `h2` et `h3` et leur associer le style adéquat dans `styles.css`.

3. L'image `beware.jpg` a du style, mais elle prend un peu trop de place : 
limitez sa hauteur à `300px`.  
**Attention :** la limite de `300px` doit s'appliquer seulement l'image
  `beware.jpg` et pas à `chuck-jeune.jpg`. Comment faire ?

5. On veut mettre en avant les innombrables arts martiaux que maîtrise Chuck
Norris. Pour ce faire :

   1. on va entourer chacun de ces arts martiaux (Taekwondo, Ju-Jitsu, ...)
      d'une balise `<span>` avec la classe `skill` dans le fichier HTML.

   2. D'un autre côté, il faut créer dans le CSS la règle qui associe à tous les
      éléments ayant la classe `skill` la mise en page suivante : texte en rouge
      et en italique (ou ce qui vous fait plaisir).

10. Testez la conformité de votre fichier CSS avec le validateur
    [https://jigsaw.w3.org/css-validator](https://jigsaw.w3.org/css-validator).

<!--
Questions complémentaires :
- autre unité de dimension (par exemple em) et créer un exemple de marge de
  taille différentes à cause d'une taille de fonte parente différente
  (margin:1em; qui se comportera différement si font-size différent)
- comprendre les subtilités de px
- favicon
- background image (il m'a fait une valeur cover qui étire l'image)
- bord rond (border-radius)
- inclusion de mp3 de assets/citation.mp3
<audio controls="controls><source ..> texte alternatif ..
-->

## Remarques finales

### Le CSS et HTML : des rôles bien distincts et complémentaires

Il y a une séparation claire entre les rôles du HTML (Contenu avec des balises
pour donner du sens) et des CSS (présentation / mise en page). Ce choix n'est
pas évident au premier abord : par exemple votre document "Word" ne sépare pas
la présentation du contenu. Mais cette séparation est indispensable et très puissante :

 * Elle permet de réutiliser une présentation d'une page à l'autre. Par exemple
   quand *lemonde.fr* publie un nouvel article, il ne refait pas le style
   expressément pour ce dernier: il s'agit d'un nouveau document HTML partageant
   le même CSS que les articles précédents ;
 * Elle permet de refaire un site Web en se concentrant sur les CSS sans (trop)
   toucher au HTML ;
 * Elle permet de changer la présentation d'un document suivant s'il est destiné à
 	l'impression ou à être visualisé avec un navigateur.
	
**Un petit piège ?** Quand on entoure un texte de la balise `<h1>`, cela
signifie que ce texte est un titre. C'est du HTML et donne de la structure. Mais
cela change aussi l'aspect visuel du texte en le mettant en gros et gras. Or
nous venons d'insister sur la séparation contenu HTML / présentation CSS, et
donc que le HTML ne doit pas changer la mise en page. Bizarre non ?

En fait, les navigateurs appliquent des styles CSS par défaut à certaines
balises HTML. Par exemple, les liens `<a>` sont en bleus et soulignés sans que
l'on ait rien à faire. Cela évite d'avoir justement TOUT à refaire en CSS : le
navigateur propose un style par défaut. Cela ne contredit pas le fait que la
mise en page soit le rôle du CSS.

<!-- Dans le devtools, elles s'appelent user agent rules -->

<!--
### Compatibilité des navigateurs


https://openclassrooms.com/courses/apprenez-a-creer-votre-site-web-avec-html5-et-css3/mettre-en-place-le-css#/id/r-1604836

problème de compatibilité
caniuse.com
On ne s'en soucie pas dans ce cours


Dans un passé assez récent, les navigateurs étant tous à des degrés différents
conformes aux directives CSS. Il est probable que les intégrateurs ayant eu
affaire à Internet Explorer 6 par exemple soient plus souvent chauves que la
moyenne.  Il était courant de voir des sites utiliser des tables pour faire des
layouts entre autre exemple.  Cela n'est pas forcément du à une méconnaissance
de la part de l'intégrateur, mais bien au contraire parfois d'une expertise sur
des solutions qui marchent sur des navigateurs mais pas sur d'autres.

-->
