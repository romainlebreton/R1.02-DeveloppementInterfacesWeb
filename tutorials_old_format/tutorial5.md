---
title: TD5 &ndash; Responsive Design
subtitle: 
layout: tutorial
---

<!--
Où est-il dit que poucentage relatif au containing block ?
tut3 : le redire ici !
-->

<!--
Antoire Affouard:

J'ai fait l'exercice 3 (flex shrink et grow) et je pense que je vais perdre un
bon nombre d'étudiants sur cette partie.

Je n'arrive pas à comprendre le rendu attendu ? avec des tailles 67% / 33% et
des grow de 3 / 1 et des shrink de 0.67 / 0.33, ça ne change rien dans aucun des
cas (cf correction de GitLab). Je pense qu'il faut remplacer ça par des tailles
fixes (cf énoncé du TD5) et surtout supprimer les min et max width qui empêchent
de voir le rendu des flex.
-->

<!--
Exemple utilisation flex-grow/shrink non triviale : solved by flex
-->

<!-- L'iconographie et les points de rupture ont changés ? -->

## Introduction

Les smartphones, les tablettes et tous les appareils de la mobilité demandent de
repenser le web d'aujourd'hui. Concevoir un site ou une application Web
s'adressant à tous ces médias n'est pas une tâche triviale. Voici un aperçu des
nombreuses solutions existantes :

* Une solution en pur CSS. En effet, le CSS est le langage de base pour la mise
  en page des pages Web. Il est donc en constante évolution (CSS3 en cours
  d'élaboration) pour s'adapter aux nouveaux besoins.

* Coder deux sites en HTML/CSS : un pour les ordinateurs et un pour les
   smartphones (et un pour les tablettes ? et un pour les smartwatch ?). Exemple
   [lemonde.fr](http://lemonde.fr) et [mobile.lemonde.fr](http://mobile.lemonde.fr).

* Des applications natives pour chaque système (Android, iOS, Windows Phone, ...)

* L'utilisation de la puissance de Javascript pour faire des mises en page
  adaptatives. 
  <!-- (et dire du mal de Javascript ensuite...) -->

* Faire le site en Flash (très mauvaise idée car il n'est plus supporté sur
  Android ni iOS).

 <!-- - utilisation de Phone Gap pour faire une application hybride (le site web est -->
 <!--   "converti" en application, on a un seul code source) -->
 <!-- - React Native,... -->

Plus pour nous positionner dans cette jungle que par purisme, nous prendrons
deux hypothèses de départ :

* *"Il n'y a pas besoin d'applications pour cela !"* : Pas besoin de faire du
   natif Android ou iOS.
* *"Il n'y a pas besoin de faire deux sites web pour cela !"* : On s'interdit de
   faire un site Web pour mobile et un pour ordinateur.


Nous adopterons dans ce TD une approche itérative, en rajoutant au fur et à
mesure des contraintes pour arriver à ce qui se fait aujourd'hui dans le
responsive design.


## CSS2

Certaines propriétés n'ont pas attendu ni les nouveaux médias ni le CSS3 pour
s'imposer aux développeurs. Elles prenaient déjà tout leur sens sur des sites
particulièrement fournis et/ou sur des petits écrans 15 pouces.

### Les pourcentages '%'

On peut commencer par exprimer toutes les tailles en relatif. C'est ce que nous
avons déjà fait en utilisant des dimensions en `%`. [Rappelez
vous]({{site.baseurl}}/tutorials/tutorial3#exercices) que la largeur d'un
élément en `display:block` ou en `display:flex` se calcule par rapport à son
*containing block*, c'est-à-dire son plus proche ancêtre `block` ou `flex`. Par
défaut, les éléments en `block` ou `flex` prennent toute la largeur de leur
*containing block*. Et si on fixe une largeur en pourcentage, ce sera
relativement à la largeur du *containing block*.

<!-- 
A-t-on un "vrai" exemple où on fixe une largeur (donc l'élément est block ou
flex) et où le containing block n'est pas le père ?
-->

<div class="exercise">

1. Donnez à `<body>` la `width` de `100%`. Donnez à la propriété `margin` la valeur `auto` si ce n'est pas le cas.
1. Enlevez au besoin la marge de gauche de `10%` sur le `<aside>` et changez les
   dimensions relatives de `<article>` et `<aside>` à respectivement `67%` et
   `33%`.

</div>


**Note :** Si adapter les largeurs en pourcentage marche bien, ce n'est pas le
cas des hauteurs.  Cela est dû au fait que la largeur de la page est connue
(c'est la largeur de la fenêtre d'affichage du navigateur) mais sa hauteur ne
l'est pas encore... (puisque la page n'est pas encore affichée et que la
hauteur va dépendre de la quantité de contenu). Autrement dit, la hauteur de la
zone du navigateur où s'affiche la page (`viewport height`) n'est pas forcément
la hauteur de la page [^somesamplefootnote] (et c'est lié à la présence d'un
ascenseur à droite pour descendre dans la page).

[^somesamplefootnote]: L'unité `vh` permet maintenant de définir une taille de 0 à 100 relative au viewport.


### `max-width` et `min-width`


Les règles précédentes permettent d'avoir un rapport homogène, mais pas un rendu
optimal :

 - sur de petits écrans d'ordinateur, des éléments ne peuvent pas être
   correctement affichés (des images, des colonnes, ...)
 - sur de très grands écrans, le texte devient illisible : les yeux fatiguent à
   cause des lignes trop longues.
 
Pour contraindre les dimensions maximales et minimales, nous utiliserons
`max-width`, `max-height`, `min-width` et `min-height`, qui prennent le même
type de valeur que `width` et `height`.


<div class="exercise">
<!-- 1. Ajoutez une limite minimale pour les photos de Chuck Norris à `150px` de -->
<!--    hauteur (et encore, mieux vaut ne pas en parler à Chuck).   -->
<!--    <\!-- ATTENTION : -->
<!--    on n'a pas encore fixé la taille de l'image comme étant relative. Veux-tu -->
<!--    passer plus de choses en taille relative ? -\-> -->
1. Ajoutez une limite maximum de largeur à `<article>` et à `<aside>` de `500px` et de `250px`.
1. Ajoutez une limite minimum de largeur à `<article>` et à `<aside>` de `200px` et `150px`.
</div>


### Overconstraint

Mais que se passe-t-il quand on mélange `min-width` et des tailles en
poucentage ? Prenons l'exemple suivant


```html
<div style="display:flex">
	<div style="width:50%;max-width:400px;">
		Div1
	</div>
	<div style="width:50%;">
		Div2
	</div>
</div>
```

qui s'affiche comme suit

<div style="display:flex;border:1px solid black;">
<div style="width:50%;max-width:400px;background-color:orange;">
Div1
</div>
<div style="width:50%;background-color: cornflowerblue;">
Div2
</div>
</div>

<br>

<div class="exercise">

**Remarquez** en changeant la largeur de votre fenêtre (ou en zoomant) que :

1. les deux `<div>` prennent toute la largeur quand `<body>` a une largeur
   inférieure à `800px` (donc le premier `<div>` a une largeur de moins de
   `400px`)
2. mais quand la largeur de `<body>` est supérieure à `800px`, alors les deux
   `<div>` ne remplissent plus toute la largeur de `<body>`. Div2 garde une
   largeur de 50% mais Div1 ne peut plus prendre les `50%` restant car il est
   contraint par sa largeur maximale de `400px`.

</div>


Nous allons utiliser `display:flex` pour mieux mélanger les tailles relatives et
les contraintes `min-width`/`max-width`. Nous avions déjà vu les règles de la
colonne de gauche de
[cette super page sur FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
; c'était celles qui s'appliquaient au parent. Nous allons maintenant nous
pencher sur la colonne de droite qui s'applique aux balises enfants. Regardez
particulièrement les propriétés `flex-shrink` (valeur par défaut `1`),
`flex-grow` (valeur par défaut `0`). Pour l'instant, nous ne toucherons pas à
`flex-basis` (qui gardera donc son comportement par défaut `auto`).

<!-- Nous vous invitons à faire d'autres recherches pour mieux comprendre -->
<!-- `flex-shrink` et `flex-grow` si nécessaire. En particulier, le site du -->
<!-- [Mozilla Developer Network](https://developer.mozilla.org/fr/) est une mine -->
<!-- d'information. -->

<!-- Attention, le comportement de l'exercice précédent est déjà déformé par les
propriétés par défaut flex-grow:0; flex-shrink:1 -->

<div class="exercise">

1. Lisez la section sur `flex-shrink` et `flex-grow` dans [le guide de
   FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) ou tout
   autre page Web. N'hésitez pas à parler de votre compréhension avec votre
   professeur.

1. Donnons un exemple d'utilisation de `flex-grow`. Votre boulot est de vérifier
   que vous comprenez son fonctionnement.

   Nous pouvons désormais résoudre le problème précédent avec `flex-grow:1;`.

   ```html
   <div style="display:flex">
   	<div style="width:50%;max-width:400px;">
   		Div1
   	</div>
   	<div style="width:50%;flex-grow:1;">
   		Div2
   	</div>
   </div>
   ```
   
   qui s'affiche comme suit
   
   <div style="display:flex;border:1px solid black;">
   <div style="width:50%;max-width:400px;background-color:orange;">
   Div1
   </div>
   <div style="width:50%;flex-grow:1;background-color: cornflowerblue;">
   Div2
   </div>
   </div>

   Maintenant que la largeur de `<body>` est supérieure à `800px`, alors le
   second `<div>` voit sa largeur augmenter grâce à `flex-grow:1;`. Donc les
   deux `<div>` remplissent toujours la largeur de `<body>`.

1. Changez les largeurs de `<article>` et `<aside>` pour qu'elles soient par
défaut de `300px` et `200px`. Mettez les propriétés `flex-shrink` et `flex-grow`
pour ces deux éléments à `0`.  
**Bougez** la largeur de la page. Est-ce que les largeurs de `<article>` et
`<aside>` changent ?

1. Nous souhaitons que quand l'écran est trop large, l'espace restant soit
   réparti entre `<article>` et `<aside>` de telle sorte que l'espace gagné par
   `<article>` soit 3 fois plus grand que celui gagné par `<aside>`.  
   **Quelle propriété** CSS devez-vous utiliser pour avoir ce comportement ?
   Implémentez ce comportement.

1. Pour vérifier que vous avez bien répondu à la question précédente,
   redimensionnez la fenêtre du navigateur pour que la largeur de `<body>` soit
   de `620px`.   
   Quelles devraient être selon vous les largeurs de `<article>` et `<aside>` ?
   Inspectez maintenant les largeurs de `<article>` et `<aside>` pour vérifier votre calcul.
   <!-- Réponse : article 390 px et aside 230px car 120px de rab réparti en 30px de rab par unité -->

1.  Nous souhaitons que quand l'écran est trop petit, `<article>` diminue de
    deux tiers de la largeur à supprimer et `<aside>` diminue du reste.  
   **Quelle propriété** CSS devez-vous utiliser pour avoir ce comportement ?
   Implémentez ce comportement.

   <!-- Bien sûr, toutes ces largeurs respecteront les anciennes contraintes `min-width` et `max-width`. -->

<!-- 3. Redimensionnez la fenêtre du navigateur pour que la largeur de `<body>` soit -->
<!--    de `476px`. Inspectez les largeurs de `<article>` et `<aside>`. Vérifiez que -->
<!--    votre comportement satisfait le cahier des charges. -->

<!-- Réponse : -->

<!-- La mauvaise réponse tentante est : article 284 px et aside 192px car 24px à -->
<!-- gagner réparti en 8px à enlever par unité. -->

<!-- Cependant le rétrécissement se fait en proportion de la taille des -->
<!-- éléments. Donc on doit enlever 6% à 300px (282) et 3% à 200px (194). -->

<!-- Référence : http://www.w3.org/TR/css3-flexbox/#flex-property -->
<!-- Note: The flex shrink factor is multiplied by the flex base size when -->
<!-- distributing negative space. This distributes negative space in proportion to -->
<!-- how much the item is able to shrink, so that e.g. a small item won’t shrink to -->
<!-- zero before a larger item has been noticeably reduced. -->
   
<!--
ATTENTION :
* ne pas utiliser le raccourci flex: 3 2; ne va pas car il force flex-basis:0% au
lieu de flex-basis: auto;
-->

</div>


### Problèmes plus complexes


Il arrive un moment où diminuer encore la taille n'a plus de sens. Il faut
prendre des mesures draconiennes, par exemple passer `<aside>` sous `<article>`
ou carrément supprimer `<aside>`.

Les règles CSS déjà vues en TDs ne permettent pas de coder ce genre de
comportement. Il nous faut une façon d'écrire du CSS qui ne sera valide que dans
des cas précis. Nous verrons dans la prochaine section comment cela est possible
en CSS3.

## Votre site de Chuck Norris sur mobile

### Les outils pour travailler ?

Jusqu'ici on pouvait considérer que tous les outils de développement d'Internet
Explorer / Firefox / Chrome étaient égaux. En fait celui de Chrome était déjà un
peu meilleur :
<!-- (Suivant les habitudes des développeurs cela peut être plus ou moins sujet à -->
<!-- controverse.) -->

  * auto complétion des règles CSS ajoutées dynamiquement,
  * liste déroulante des valeurs possibles des champs,
  * plus rapide, plus stable (un processus par onglet)
  * etc.

En tout cas, pour le *reponsive design* il n'y a pas photo : Chrome (ou son
pendant libre Chromium) est <strong>vraiment</strong> votre "best-friend-ever".


### Que fait mon navigateur Web sur téléphone par défaut pour un site ?

Comment peut-on rendre un site internet compatible mobile à moindre coût ?

Voici l'algorithme (simplifié) opérant par défaut :

 * Générer le site sur une taille d'écran virtuel, disons d'une largeur de `980px` ;
 * Faire un zoom arrière de manière à faire rentrer le site dans l'écran du
   smartphone ; (oui, cela fait de petits éléments)
 * Supposer que l'utilisateur connaît le *pinch to zoom* pour naviguer dans le site :
 <img src="{{site.baseurl}}/assets/pinch_zoom.png " alt="Pinch to zoom schema"
style="margin: 0 auto;height:100px;vertical-align:middle;">

<!--

OK, d'après mes tests avec le device mode, le comportement par défaut est
bien de générer le site pour 960px de largeur puis de le scaler

As-tu des références sur cela ?

Attention, si on touche au page scale des device mode alors il faut modifier la
page puis la recharger pour retrouver le comportement par défaut.

-->

Et ça marche ! De fait, c'est ce que font par défaut les smartphones quand ils
tombent sur un site non responsive.

<div class="exercise">

1. Dans les outils développeurs (`F12`) de Chrome/Chromium, passez dans le
device mode 
<img src="{{site.baseurl}}/assets/phone-responsive.png" alt="Outil pour mobile" style="margin: 0 auto;width:45px;vertical-align:middle;">
*"Samsumg Galaxy S5"* sous Chrome/Chromium et rechargez votre page. Constatez
que le site s'affiche en tout petit.

<!-- **Attention :** En appuyant sur `F12` sur Chrome/Chromium, vous devez voir la -->
<!-- petite icône <img src="{{site.baseurl}}/assets/phone-responsive.png" alt="Outil -->
<!-- pour mobile" style="margin: 0 auto;width:45px;vertical-align:middle;">. Sinon, -->
<!-- c'est que votre version de Chrome ou Chromium n'est pas à jour. Dans ce cas, -->
<!-- allez sur le [site de l'IUT](https://iutdepinfo.iutmontp.univ-montp2.fr/), -->
<!-- identifiez-vous puis téléchargez -->
<!-- [l'archive suivante](https://infolimon.iutmontp.univ-montp2.fr/public/windows/chrome-win32.zip) -->
<!-- (à décompresser avec *7-zip*).  Il faudra d'abord fermer toutes vos fenêtres de -->
<!-- Chrome avant de lancer l'exécutable `chrome.exe` contenu dans l'archive. -->

<!-- 1. Inspectez le `<body>` de votre page pour voir sa largeur. -->

<!--    <\!-- largeur : 980 px sur mon PC -\-> -->

<!-- 1. Zoomez et dézoomez avec les boutons - et + de <img -->
<!-- src="{{site.baseurl}}/assets/zoom-button.png" alt="Bouton pour le zoom" -->
<!-- style="vertical-align:middle"> (émulation du *pinch-to-zoom*). Passez au niveau -->
<!-- de zoom 1 pour voir le site non zoomé. -->

1. Vérifiez que la taille du `<body>` est de `980px`, ce qui signifie que
   l'algorithme précédent a été utilisé pour l'affichage.  
   Remarquez aussi que la largeur de l'affichage est de `360px`, ce qui signifie
   d'un zoom arrière est effectué.

</div>

Même si cela marche, on ne peut pas dire que cela soit optimal. L'utilisateur
mobile n'a pas la même attente que l'utilisateur sur ordinateur, il veut avoir
accès rapidement aux informations essentielles, sans fioritures.  On imagine que
sur une smart watch par exemple un site comme méteo france serait largement plus
dépouillé (sur une smartwatch elle afficherait un nuage ou un soleil et la
température par exemple).

Typiquement nous voulons enlever des parties entières du site suivant la taille
de l'écran.

La première chose à faire est donc de demander aux navigateurs de ne plus faire
l'algorithme précédent (puisqu'on va le gérer nous-mêmes) dans la balise
`<head>` :

```html
 <meta name="viewport" content="width=device-width, initial-scale=1">
```

<!--
C'est encore au stade de Working draft !! Mais çà marche sur chrome ...
Référence :
https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes

http://www.alsacreations.com/article/lire/1490-comprendre-le-viewport-dans-le-web-mobile.html

Meta name viewport viendrait de Apple et serait propriétaire

Pré-norme de remplacement avec @viewport dans CSS
https://www.w3.org/TR/css-device-adapt-1/
-->

<div class="exercise">

Ajouter cette instruction au site de Chuck Norris et visualisez avec Chrome en
choisissant un smartphone. Inspectez la largeur de `<body>`. Que constatez-vous ?

</div>

Vous devez constatez que l'algorithme précédent ne s'applique plus. En gros le
navigateur n'essaie plus d'être intelligent : il vous laisse prendre le relai.

## La solution technique CSS3 :  les media queries

Les media queries sont un jeu d'options ajoutées à la norme CSS3 et qui permettent
de définir des règles CSS qui ne s'appliqueront que sous certaines conditions
spécifiques.

Il existe deux manières différentes de faire appel à une *media query* :

* Soit vous souhaitez un fichier CSS spécifique en entier, mais uniquement dans
  certaines conditions. Alors il faut ajouter à l'en-tête `<head>` de la page
  web une déclaration de fichier CSS standard, à laquelle on rajoute l'attribut
  `media` et une condition spécifique.

  ```html
  <link rel="stylesheet" media="condition" href="mon_css_special.css"/>
  ```
  
  N'oubliez pas que le dernier CSS chargé prend le pas sur les
  précédents. Pensez donc à toujours déclarer vos media-queries en dernier,
  sinon elles seront systématiquement écrasées par votre CSS *“standard"*.

* Soit vous souhaitez que juste certaines règles s'appliquent sous
  certaines conditions. Alors vous englobez vos règles avec la syntaxe suivante :

  ```css
  @media(ma_condition) {
    div {background-color:white;}
     ...
  }
  ```

Une media query fonctionne de la manière suivante : la condition est évaluée et
retourne une valeur “vrai” ou “faux”. Si la valeur est vraie, le fichier CSS/ la
règle CSS (selon la méthode employée) est appliquée.

Chaque condition est formée à partir d'une ou plusieurs conditions de
base. Parmi
[l'ensemble des conditions possibles](https://developer.mozilla.org/fr/docs/Web/CSS/Media_queries),
nous allons nous intéresser particulièrement aux suivantes :

* `min-width`, `max-width`, `min-height` et `max-height` : permettent de
  renseigner une dimension minimale/maximale à remplir pour que la condition
  soit vraie. Par exemple,

  ```css
    @media(min-width:100px) {
      div {background-color:white;}
    }
  ```

  <!-- Définies dans l'une des unités supportées par le CSS (px, em, cm, in...). Si -->
  <!-- ni “min” ni “max” n'est utilisé, alors la condition se réfère à une taille -->
  <!-- exacte. -->
  <!-- * « color » : le nombre de bits par couleur supportés par l'écran (0 = noir et -->
  <!--   blanc, 8 = 256 couleurs, 16 = 65000 couleurs) -->
  
* `orientation` : prend les valeurs `landscape` (écran horizontal) ou `portrait`
  (écran vertical)

<!-- * « type de média » : prend l'une de ces valeurs. Vous pouvez créer avec un jeu -->
<!--   de règles CSS qui ne s'appliquera que pour une impression ou un système de -->
<!--   synthèse vocale pour les aveugles. -->

<!-- * « monochrome » : 0 si l'écran est couleur, sinon une valeur en nombre de bits -->
<!--   par couleur pour les écrans supportant des niveaux de gris. Il est donc -->
<!--   possible en combinant les conditions de base “color” et “monochrome” de cibler -->
<!--   spécifiquement les devices “noir et blanc”, “niveau de gris” ou “couleur” pour -->
<!--   adapter par exemple les couleurs de police de caractère -->



Les conditions de base peuvent être combinées ensemble pour former des
conditions complexes en utilisant les opérateurs logiques :

* “and” (ET) : les deux conditions de base doivent être vraies pour que la
  condition soit vraie
* “,” (OU) : au moins l'un des conditions de base doit être vraie pour que la
  condition soit vraie
* “not” (NON) : la condition de base qui suit le not doit être fausse pour que la
  condition soit vraie

**Exemple :** la règle `(min-width: 500px) and (min-height: 800px)` n'est
vraie que si la largeur de l'affichage est supérieure (ou égale) à `500px` et la
hauteur supérieure à `800px`.


<div class="exercise">

* Allez sur le site [Bootstrap](http://getbootstrap.com/) et constatez qu'il y a
  2 largeurs pour laquelle la mise en page change.
* Utilisez le *device mode* pour afficher les *media queries* (cliquer sur les 3
  points verticaux du *device mode* pour afficher ces *media queries*).
* Que se passe-t-il visuellement dans le menu lorsque vous redimensionnnez la
fenêtre autour du point de rupture situé à `768px` ?

</div>


### Les points de ruptures.

Afin d'organiser nos *media queries*, on utilise en général 3 à 4 valeurs de largeur d'écrans, par exemple : 
 
 * `480px` (Smartphone)
 * `768px` (Tablette)
 * `992px` (écran d'ordinateur "Standard")
 * `1200px` (écran d'ordinateur "Large")

<div class="exercise">
 1. en dessous de 768px ne plus afficher la table de comparaison (de toute façon
    s'il ne doit rester qu'un seul, ce sera Chuck Norris).
 1. en dessous de 480px faire en sorte qu'`<aside>` et `<article>` soient en
    colonne et plus en ligne.
 1. (Optionnel) Sur une smartwatch (width `168px`), n'affichez que les citations
 de Chuck Norris contenues dans le `<aside>`.
 <!-- Peut-être que le sélecteur :not() peut grandement faciliter la suppression
 de tout le contenu SAUF quelques petites choses -->

</div>


### Mettez-moi un burger au menu !

Quand la taille de l'écran est limitée, une bonne pratique en *responsive design*
est de changer l'affichage du menu pour un bouton burger :

<img alt="Burger button, three horizontal lines, (two corresponding to the
bread, and the one for the meal) " src="{{site.baseurl}}/assets/burger.png"
style="margin:0 auto;display: block;">

Lorsque l'on cliquera dessus, le menu apparaîtra. Cela permet de ne pas perdre
de place sur la page lorsque le menu est fermé. Pour fixer les idées, nous
voulons un menu qui apparaît latéralement à la manière des exemples suivants :
 
 * [http://codepen.io/gungorbudak/pen/XbazEX](http://codepen.io/gungorbudak/pen/XbazEX)
 * [http://codepen.io/drewr/pen/uxvdt](http://codepen.io/drewr/pen/uxvdt)

Dans l'exercice suivant, nous allons coder un menu burger HTML/CSS (donc sans
JavaScript) qui apparait quand la souris passe au dessus du burger (la gestion
du clic nécessiterait du JavaScript).  (Notez au passage que
[codepen.io](http://codepen.io/) est un très bon outil pour découvrir de
nouvelles techniques !)

<div class="exercise">

Nous allons coder un deuxième menu, identique au premier dans son contenu, mais
avec une mise en page différente. Nous allons afficher l'un ou l'autre des menus
en fonction de la taille de l'écran.

1. Ajouter un `<div>` de classe `burger` contenant l'image de burger (largeur
   `50px`) juste avant le menu `<nav>`.
1. À partir du point de rupture 'Smartphone', faites disparaître l'ancien menu
et faites apparaître le `<div class="burger">` à droite de la page (à la place
du menu).
1. Implémentez le deuxième menu avec les caractéristiques suivantes :

   * Son contenu est

     ```html
     <div class="burger">
       <img src="images/burger.png" alt="burger" width="50px">
       <div id="menu2">
         <div><a href="./index.html">Accueil</a></div>
         <div><a href="./facts.html">Facts</a></div>
         <div><a href="./news.html">Actualités</a></div>
         <div><a href="./contact.html">Contact</a></div>
      </div>
     </div>
     ```


    * il se positionne par rapport à la fenêtre d'affichage (quelle valeur de
    `position` faut-il mettre ?), tout en haut à droite.
	* il occupe 80% de la largeur de la fenêtre d'affichage et 100% de sa
      hauteur (Cherchez sur le Web les unités de mesure `vh` et `vw`
      [^somesamplefootnote])
    * il est visuellement au-dessus des autres éléments du site (cherchez sur le
    Web la propriété `z-index`)
	* les sous-menus sont disposés verticalement.

1. Cachez par défaut en CSS le `menu2`. Au survol du `<div class="burger">`,
   faites-le réapparaître.
1. (Optionnel) Changez la logique pour masquer le `menu2` : À la manière de
   [http://codepen.io/gungorbudak/pen/XbazEX](http://codepen.io/gungorbudak/pen/XbazEX),
   cachez le menu en le décalant sur sa gauche de sa largeur avec la propriété
   `margin-left`. Faites une transition dessus (ohhhh! c'est beauuuu!)

<!-- PROBLEME : ON NE PEUT PAS CLIQUER SUR LE MENU CAR IL DISPARAIT LE TEMPS QUE
LA SOURIS L'ATTEIGNE -->

</div>

**Note :** Le hover sur les sous-menus n'a pas de sens sur téléphone
  portable. Il faudra gérer le clic avec du JS. La bonne solution est
  ... suspense, vous la verrez en 2ème année.


### La mobilité en général

Les contraintes liées à la mobilité ne se limitent pas au responsive design.
Pour vous donner une idée plus complète, voici d'autres exemples de contraintes
fortes qui viennent s'ajouter :

 * débit du réseau
 * faible capacité du média (processeur, mémoire vive,...)
 * mode offline (on peut passer sous un pont... il faut prévoir pour le cas échéant un cache local qui stocke les opérations courantes, afin de les consommmer lorsque le réseau revient) 
 * changement de paradigme de l'interface homme machine (mouse over, menu déroulant,... )

<!-- ## Autre page intéressante pour avoir des idées -->

<!-- https://developer.mozilla.org/en-US/Apps/Design/UI_layout_basics/responsive_design_building_blocks -->

<!-- https://philipwalton.github.io/solved-by-flexbox/ -->
