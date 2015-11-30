---
title: TD5 &ndash; Responsive Design
subtitle: 
layout: tutorial
---


## Introduction

Les smartphones, les tablettes et tous les appareils de la mobilité demandent de
repenser le web d'aujourd'hui. Concevoir un site ou une application Web
s'adressant à tous ces médias n'est pas une tache triviale. Voici un aperçu des
nombreuses solutions existantes :

* Une solution en pur CSS. En effet, le CSS est le langage de base pour la mise
  en page des pages Web. Il est donc en constante évolution (CSS3 en cours
  d'élaboration) pour s'adapter aux nouveaux besoins.

* Coder deux sites en HTML/CSS : un pour les ordinateurs et un pour les
   smartphones (et un pour les tablettes ? et un pour les smartwatch ?). Exemple
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

Plus pour nous positionner dans cette jungle que par purisme, nous prendrons deux hypothèses de départ :

* *"Il n'y a pas besoin d'applications pour cela !"* : Pas besoin de faire du
   natif Android ou iOS.
* *"Il n'y a pas besoin de faire deux sites web pour cela!"* : On s'interdit de
   faire un site Web pour mobile et un pour ordinateur.


Nous adopterons dans ce TD une approche itérative, en rajoutant au fur et à
mesure des contraintes pour arriver à ce qui se fait aujourd'hui dans le
responsive design.


## CSS2

Certaines propriétés n'ont pas attendu ni les nouveaux médias ni le CSS3 pour
s'imposer aux développeurs. Elles prenaient déjà tout leur sens sur des sites
particulièrement fournis et/ou sur des petits écrans 15 pouces.

### Les pourcentages '%'

On peut commencer par exprimer toutes les tailles en relatif, en prenant comme
référence la largeur de l'écran. C'est ce que nous avons déjà fait en utilisant
des dimensions en `%`.

<div class="exercise">

1. Donnez à `<body>` la `width` de `100%`. Donner à la propriété `margin` la valeur `auto` si ce n'est pas le cas.
1. Enlevez au besoin la marge de gauche de `10%` sur le `<aside>` et changez les
   dimensions relatives de `<article>` et `<aside>` à respectivement `67%` et
   `33%`.

</div>


**Note :** Si adapter les largeurs en pourcentage marche bien, ce n'est pas le
cas des hauteurs.  Cela est dû au fait que la largeur de la page est connue
(c'est la largeur du navigateur) mais sa hauteur ne l'est pas encore
... (puisque la page n'est pas encore affichée et que la hauteur va dépendre de
la quantité de contenu). Autrement dit, la hauteur de la zone du navigateur où
s'affiche la page (`viewport height`) n'est pas forcément la hauteur de la page
[^somesamplefootnote] (c'est lié à la présence d'un ascenseur à droite pour
descendre dans la page).

[^somesamplefootnote]: L'unité `vh` permet maintenant de définir une taille de 0 à 100 relative au viewport.


### `max-with` et `min-with`


Les règles précédentes permettent d'avoir un rapport homogène, mais pas un rendu
optimal :

 - sur de petits écrans d'ordinateur, des éléments ne peuvent pas être
   correctement affichés (des images, des colonnes, ...)
 - sur de très grands écrans, le texte devient illisible : les yeux fatiguent à
   cause des lignes trop longues.
 
Pour contraindre les dimensions maximales et minimales, nous utiliserons
`max-width`, `max-height`, `min-width` et `min-height`, qui prennent le même
type de valeur que `width` et `height`.


<div class="exercise">
1. Ajoutez une limite minimale pour les photos de Chuck Norris à `150px`, (et
   encore, mieux vaut ne pas en parler à Chuck).
   <!-- ATTENTION : on n'a pas encore fixé la taille de l'image comme étant
relative. Veux-tu passer plus de choses en taille relative ? -->
1. Ajoutez une limite maximum de largeur à l'`<article>` et à l'`<aside>` de `500px` et de `250px`.
1. Ajoutez une limite minimum de largeur à l'`<article>` et à `<aside>` de `200px` et `150px`.
</div>


### Overconstraint

Évidemment lorsque l'on joue avec des `min-width` et un petit écran à un moment
çà dépasse.

Il va falloir donc utiliser des règles subtiles pour relâcher une ou des contraintes lorsqu'elles ne peuvent pas être toutes satisfaites (on parle d'overconstraint pour faire bien).

On va utiliser FlexBox pour exprimer cela en se servant de
[cette super page sur FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).
Grosso-modo nous avons déjà vu les règles de la colonne de gauche de cette
page : c'est celles qui s'appliquent au parent.  Nous allons maintenant
découvrir les règles de droites : celles qui s'appliquent aux éléments. Regardez
particulièrement les propriétés `flex-shrink`, `flex-grow`. Nous ne toucherons
pas à `flex-basis` (qui gardera donc son comportement par défaut `auto`).


<!-- Attention, le comportement de l'exercice précédent est déjà déformé par les
propriétés par défaut flex-grow:0; flex-shrink:1 -->

<!-- NOUVEL EXERCICE : ON EN PARLE -->
<div class="exercise">

1. Implémentez le comportement suivant :  
Changez les largeurs de `<article>` et `<aside>` pour qu'elles
soient par défaut de `300px` et `200px` et que :

   1. Quand l'écran est trop petit pour afficher `<article>` et `<aside>`,
    `<article>` diminuera de deux tiers de la largeur à supprimer et `<aside>`
    diminuera du reste.
	
   1. Quand l'écran est trop grand, faites en sorte que l'espace restant soit
    réparti entre `<article>` et `<aside>` de telle sorte que l'espace gagné par
    `<article>` soit 3 fois plus grand que celui gagné par `<aside>`.

   Bien sûr, toutes ces largeurs respecteront les anciennes contraintes `min-width` et `max-width`.

2. Redimensionnez la fenêtre du navigateur pour que la largeur de `<body>` soit de `620px`. Inspectez les largeurs de `<article>` et `<aside>`. Vérifiez que
   votre comportement satisfait le cahier des charges.

   <!-- Réponse : article 390 px et aside 230px car 120px de rab réparti en 30px de rab par unité -->

<!-- 3. Redimensionnez la fenêtre du navigateur  pour que la largeur de `<body>` soit de `380px`. Inspectez les largeurs de `<article>` et `<aside>`. Vérifiez que -->
<!--    votre comportement satisfait le cahier des charges. -->

   <!-- Réponse : article 220 px et aside 160px car 120px à gagner réparti en 40px à enlever par unité   -->
   <!-- Je ne sais pas pourquoi chromium fait 210 / 170 ??? -->
   <!-- EXERCICE 3.3 buggé à cause de flex-shrink buggé ??? -->
   
<!--
ATTENTION :
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

### Les outils pour travailler ?

Jusqu'ici on pouvait considérer que tous les outils de développement d'Internet
Explorer / Firefox / Chrome étaient égaux. En fait celui de Chrome était déjà un
peu meilleur :
<!-- (Suivant les habitudes des développeurs cela peut être plus ou moins sujet à -->
<!-- controverse.) -->

  * auto complétion des règles CSS ajoutées dynamiquement,
  * liste déroulante des valeurs possibles des champs,
  * plus rapide, plus stable (un processus par onglet)
  * etc.

En tout cas, pour le Reponsive design il n'y a pas photo : Chrome (ou son
pendant libre Chromium) est <strong>vraiment</strong> votre "best-friend-ever".

**Attention :** Si vous n'avez pas Chrome ou Chromium, ou si en appuyant sur F12
vous ne voyez pas la petite icône 
<img src="{{site.baseurl}}/assets/phone-responsive.png" alt="Outil pour mobile"
style="margin: 0 auto;width:100px;vertical-align:middle;">
allez sur le [site de l'IUT](https://iutdepinfo.iutmontp.univ-montp2.fr/),
identifiez-vous et téléchargez directement
[le lien](https://infolimon.iutmontp.univ-montp2.fr/public/windows/chrome-win32.zip).

<!-- Veuillez alors choisir dans *Device*, l'appareil *Samsung Galaxy SIII*. -->

### Que fait mon navigateur Web sur téléphone par défaut pour un site ?

Comment peut-on rendre un site internet compatible mobile à moindre coût ?

Voici l'algorithme (simplifié) opérant par défaut :

 * Générer le site sur une taille d'écran virtuel, disons d'une largeur de `980px` ;
 * Faire un zoom arrière de manière à faire rentrer le site dans l'écran du smartphone ; (oui, cela fait de petits éléments)
   <!-- Tu veux dire avoir des tailles relatives partout qui ont étés étudiées pour 800x600 ? -->
 * Supposer que l'utilisateur connaît le *pinch to zoom* pour naviguer dans le site :
 <img src="{{site.baseurl}}/assets/pinch_zoom.png " alt="Pinch to zoom schema"
style="margin: 0 auto;height:100px;vertical-align:middle;">

<!--

OK, d'après mes tests avec le device mode, le comportement par défaut est
bien de générer le site pour 960px de largeur puis de le scaler

As-tu des références sur cela ?

Attention, si on touche au page scale des device mode alors il faut modifier la
page puis la recharger pour retrouver le comportement par défaut.

-->

Et çà marche ! De fait, c'est ce que font par défaut les smartphones quand ils
tombent sur un site non responsive.

<div class="exercise">

1. Dans les outils développeurs (`F12`) de Chrome/Chromium, passez dans le
device mode "Samsumg Galaxy SIII" sous Chrome/Chromium et rechargez votre
page. Constatez que le site s'affiche en tout petit.
1. Inspectez le `<body>` de votre page pour voir sa largeur.

   <!-- largeur : 980 px sur mon PC -->

1. Zoomez et dézoomez avec les boutons - et + de <img
src="{{site.baseurl}}/assets/zoom-button.png" alt="Bouton pour le zoom"
style="vertical-align:middle"> (émulation du *pinch-to-zoom*). Passez au niveau
de zoom 1 pour voir le site non zoomé.  

</div>

Cela marche mais on ne peut pas dire que cela est forcément le mieux.
L'utilisateur mobile n'a pas la même attente que l'utilisateur sur ordinateur,
il veut avoir accès rapidement aux informations essentielles, sans fioritures.
On imagine que sur une smart watch par exemple un site comme méteo france serait
largement plus dépouillé (sur une smartwatch elle afficherait un nuage ou un
soleil et la température par exemple).

Typiquement nous voulons enlever des parties entières du site suivant la taille
de l'écran.

La première chose à faire est donc de demander aux navigateurs de ne plus faire
l'algo précédent (puisqu'on va le gérer nous-mêmes) dans la balise `<head>` :

~~~
 <meta name="viewport" content="width=device-width, initial-scale=1">
~~~
{:.html}

<!--
C'est encore au stade de Working draft !! Mais çà marche sur chrome ...
Référence :
https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes
-->

<div class="exercise">

Ajouter cette instruction au site de Chuck Norris et visualisez avec Chrome en
choisissant un smartphone. Inspectez la largeur de `<body>`. Que constatez-vous
?

</div>

Vous devez constatez que l'algorithme précédent ne s'applique plus. En gros le
navigateur n'essaie plus d'être intelligent : il vous laisse prendre le relai.

## La solution technique CSS3 :  les media queries

Les media queries sont un jeu d'options ajoutées à la norme CSS3 et qui permettent
de définir des règles CSS qui ne s'appliqueront que sous certaines conditions
spécifiques.

Il existe deux manières de faire appel à une media query:

* charger un fichier CSS spécifique en entier, uniquement dans certaines
  conditions. Il faut ajouter à l'en-tête `<head>` de la page web une
  déclaration de fichier CSS standard, à laquelle on rajoute l'attribut `media`
  et une condition spécifique.  
  N'oubliez pas que le dernier CSS chargé prend le pas sur les
  précédents. Pensez donc à toujours déclarer vos media-queries en dernier,
  sinon elles seront systématiquement écrasées par votre CSS *“standard"*.

  ~~~
  <link rel="stylesheet" media="condition" href="mon_css_spécial.css"/>
  ~~~
  {:.html}

* au sein même d'un fichier CSS, on peut définir certaines règles qui ne
  s'appliqueront que sous certaines conditions :

  ~~~
  @media(ma_condition) {
     ...
  }
  ~~~
  {:.css}

Une media query fonctionne de la manière suivante: la condition est évaluée et
retourne une valeur “vrai” ou “faux”. Si la valeur est vraie, le fichier CSS/ la
règle CSS (selon la méthode employée) est appliquée.

Chaque condition est formée à partir d'une ou plusieurs conditions de base. Les
conditions de base peuvent être combinées ensemble pour former des conditions
complexes en utilisant les opérateurs logiques:

* “and” (ET): les deux conditions de base doivent être vraies pour que la
  condition soit vraie
* “,” (OU): au moins l'un des conditions de base doit être vraie pour que la
  condition soit vraie
* “not” (NON): la condition de base qui suit le not doit être fausse pour que la
  condition soit vraie

**Exemple :** la règle `(min-width: 500px) and (min-height: 800px)` n'est
vraie que si la largeur de l'affichage est supérieure (ou égale) à `500px` et la
hauteur à `800px`.


<div class="exercise">

Allez sur le site [Bootstrap](http://getbootstrap.com/) et constatez les 2 points de ruptures. Aidez-vous du
bouton *"media query"* <img src="{{site.baseurl}}/assets/media-query-icon.png"
alt="Bouton pour découvrir les media-query" style="vertical-align:middle">. (Au besoin actualisez la page pour que l'outil puisse correctement émuler le comportement sur mobile).
Que ce passe-t-il visuellement dans le menu lorsque vous redimensionnnez la fenêtre autour du point de rupture situé à `768px` ?



</div>


### Les points de ruptures.

Afin d'organiser notre media queries, on utilise en général 3 à 4 valeurs de largeur d'écrans, par exemple : 
 
 * `480px` (Smartphone)
 * `768px` (Tablette)
 * `992px` (écran d'ordinateur "Standard")
 * `1200px` (écran d'ordinateur "Large")

<div class="exercise">
 1. en dessous de 768px ne plus afficher la table de comparaison (de toute façon
    s'il ne doit rester qu'un seul, ce sera Chuck Norris).
 1. en dessous de 480px faire en sorte qu'`<aside>` et `<article>` soit en
    colonne et plus en ligne.
 1. (Optionnel) Sur une smartwatch (width `168px`), n'affichez que les citations
 de Chuck Norris contenues dans le `<aside>`.
 <!-- Peut-être que le sélecteur :not() peut grandement faciliter la suppression
 de tout le contenu SAUF quelques petites choses -->

</div>


### Mettez-moi un burger au menu !

Quand la taille de l'écran est limitée, une bonne pratique en *responsive design*
est de changer l'affichage du menu pour un bouton burger :

<img alt="Burger button, three horizontal lines, (two corresponding to the
bread, and the one for the meal) " src="{{site.baseurl}}/assets/burger.png"
style="margin:0 auto;display: block;">

Lorsque l'on cliquera dessus, le menu apparaîtra. Cela permet de ne pas perdre
de place sur la page lorsque le menu est fermé. Pour fixer les idées, nous
voulons quelque chose se rapprochant de cela :
 
 * [http://codepen.io/gungorbudak/pen/XbazEX](http://codepen.io/gungorbudak/pen/XbazEX)
 * [http://codepen.io/drewr/pen/uxvdt](http://codepen.io/drewr/pen/uxvdt)

(Notez au passage que [codepen.io](http://codepen.io/) est un très bon outil pour
découvrir de nouvelles techniques !)

<div class="exercise">

Nous allons coder un deuxième menu, identique au premier dans son contenu, mais
avec une mise en page différente. Nous allons afficher l'un ou l'autre des menus
en fonction de la taille de l'écran.

1. Ajouter un `<div>` de classe `burger` contenant l'image de burger (largeur
   `50px`) juste avant le menu `<nav>`.
1. À partir du point de rupture 'Smartphone', faites disparaître l'ancien menu
et faites apparaître le `<div class="burger">` à droite de la page (à la place
du menu).
1. Implémentez le deuxième menu avec les caractéristiques suivantes :

   * Son contenu est

     ~~~
     <div class="burger">
       <img src="images/burger.png" alt="burger" width="50px">
       <div id="menu2">
         <div><a href="./index.html">Accueil</a></div>
         <div><a href="./facts.html">Facts</a></div>
         <div><a href="./news.html">Actualités</a></div>
         <div><a href="./contact.html">Contact</a></div>
      </div>
     </div>
     ~~~
     {:.html}


    * il se positionne par rapport à la fenêtre d'affichage (quelle valeur de
    `position` faut-il mettre ?), tout en haut à gauche.
	* il occupe 80% de la largeur de la fenêtre d'affichage et 100% de sa
      hauteur (Cherchez sur le Web les unités de mesure `vh` et `vw`
      [^somesamplefootnote])
    * il est visuellement au-dessus des autres éléments du site (cherchez sur le
    Web la propriété `z-index`)
	* les sous-menus sont disposés verticalement.

1. Cachez par défaut en CSS le `menu2`. Au survol du `<div class="burger">`,
   faites-le réapparaître.
1. (Optionnel) Changez la logique pour masquer le `menu2` : À la manière de
   [http://codepen.io/gungorbudak/pen/XbazEX](http://codepen.io/gungorbudak/pen/XbazEX),
   cachez le menu en le décalant sur sa gauche de sa largeur avec la propriété
   `margin-left`. Faites une transition dessus (ohhhh! c'est beauuuu!)

<!-- PROBLEME : ON NE PEUT PAS CLIQUER SUR LE MENU CAR IL DISPARAIT LE TEMPS QUE
LA SOURIS L'ATTEIGNE -->

</div>

**Note :** Le hover sur les sous-menus n'a pas de sens sur téléphone
  portable. Il faudra gérer le clic avec du JS. La bonne solution est
  ... suspense, vous la verrez en 2ème année.


<!--
## Une solution plus pratique que les media queries 

### Le classique 12 colonnes.


### Responsive images 

* image responsive avec srcset ?



### La mobilité en général

Les contraintes liées à la mobilité ne se limitent pas au repsonive design.
D'autres contraintes fortes viennent aussi s'ajouter :

 * débit du réseau
 * faible capacité du média (processeur, memoire vive,...)
 * mode offline (on peut passer sous un pont... il faut prévoir pour le cas échéant un cache local qui stoque les opérations courantes, afin de les consommmer lorsque le réseau revient) 
 * changement de paradigme IHM (mouse over, menu déroulant,... )
 -....
-->
