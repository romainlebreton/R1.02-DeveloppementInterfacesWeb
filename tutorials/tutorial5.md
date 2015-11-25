---
title: TD5
subtitle: OverConstraint, Fluid Layout, Responsive design, Mobile first...
layout: tutorial
---

## Introduction

Les mobiles, les tablettes (les smartwatch ?  les lunettes de réalité vituelles/augmentées ?) sont apparues il y a peu, 
le CSS évolue donc aussi. Concevoir un site internet ou une web application pour tout ces médias n'est pas une tache triviale, et les solutions ne manques pas :

 - applications natives Android, IOS en Windows Phone ?
 - utilisation de Phone Gap pour faire une application hybride (le site web est "converti" en application, on a un seul code source)
 - coder deux sites : un pour les ordinateurs et un pour les smartphones (et un pour les tablette ? et un pour les smartwatch ?)
 - utiliser du Javacript pour faire des layouts adaptatifs ?
 - une solution en pur CSS ?
 - faire le site en Flash (non !!!!)
 - React Native,...

Plus pour nous positionner dans cette jungle, que par considération de puristes, nous prendrons deux hypothèses de départ :

 - "il n'y a pas besoin d'applications pour cela !". Pas besoin de faire du natif Android ou IOS.
 - "il n'y a pas besoin de faire deux sites web pour cela!". On s'interdit de faire deux sites web : un pour mobile et un pour ordinateurs.


Nous adopterons dans ce td une approche itérative, en rajoutant au fur et à mesure des contraintes pour arriver à ce qui se fait aujourd'hui dans le responsive design.


## CSS2

### Les pourcentages '%'

On peut commmencer par exprimer toutes les tailles en relatif, en prenant appuit sur la taille de l'écran.
Nous avons déjà utilisé le `%`. 


<div class="exercices">

 - Donnez au body une width de `100%` et changer les dimensions relatives de `<article>``et `<aside>` de repectivment `67%` et `33%`

</div>


<strong>Note</strong> : Si adapter les éléments en `%` par rapport à la largeur `width` marche bien, ce n'est pas le cas en `height`.
Cela est du au fait que la width max est connue : c'est celle du navigateur alors que la `height` ne l'est pas encore...(puisque pas encore affichée...)
Dans ce dernier cas nous avons en fait plus à l'esprit la taille de l'écran (`viewport`) que nous avons confondu avec la taille de la page [^somesamplefootnote].

[^somesamplefootnote]: L'unité `vh` permet maintenant de définir une taille de 0 à 100 relative au viewport.


### `max-with` et `min-with`


Les règles précédentes permettent d'avoir un rapport homogène, mais pas un rendu optimal :

 - sur de petit écrans ordinateurs, des éléments ne peuvent pas être correctement affichés (des images, des colonnes, ...)
 - sur des très grands écran, le texte devient illisible : les yeux fatiguent dans les retours à la ligne.
 


<div class="exercices">

 - Limitez les photos de Chuck Norris à ne pas avoir une width plus petite que `150px`, (et encore mieux vaut ne pas en parler à Chuck).
 - Ajoutez une limite maximum de largeur à l'`<article>` et à l'`<aside>` de `600px` et de `300px`.
 - Ajoutez une limite minimum de largeur à l'`<article>` et à `<aside>` de `300px`.
</div>



### Overconstraint (solution : FlexBox)

Evidement lorsqu'on joue avec des `min-width` et un petit écran...à un moment çà dépasse...

Il va falloir donc utiliser des règles subtiles pour savoir qui relache sa contrainte entre `<aside>` et `<article>`.

On va utiliser cette super page sur [FlexBox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).
Grosso-modo nous avons déjà vu les règles de la colonne de gauche de cette page : c'est celles qui s'appliquent aux parent.
Nous allons maintenant découvir les règles de droites : celles qui s'appliquent aux ...éléments.

Nous n'en disons pas plus sur cette page volontairement : le travail d'un devellopeur web consite pour une bonne partie à aller sur ce genre de page.

<div class="exercices">
 - Quand l'écran est trop petit pour afficher `<article>` et `<aside>` avec leurs contraintes de tailles minimales de la section précente, fait en sorte qu'`<article>` prenne les deux tiers de la place et `<aside>` le reste.
 - Quand l'écran est trop grand faite en sorte qu'`<article>` soit 3 fois plus grand qu'`<aside>`.
</div>


<!--
box-sizing : border-box
Que se passe-t-il si on fait 2 colonnes à 50% avec flex-shrink:0 et flex-wrap:nowrap
-->


### problèmes plus complexes ...


Il arrive un moment ...ou diminuer encore la taille même relative n'a plus de sens. Il faut prendre des mesures draconiennes.

Supposons maintenant que nous voulons carrément supprimer visuellement un élément d'un visuel sur notre mobile.
Ou même changer le layout de row en column pour utiliser le défilement. 
Ici nous n'avons pas de solution via Flex seul car nous voulons assujétir des règles CSS à certaines caractéristiques (des règles spéciales pour une taille d'écran maximum par exemple). Nous verrons dans la prochaine section comment cela est possible en CSS3.



## Que fait mon navigateur web sur téléphone par défaut pour un site ?



Comment peut on à moindre coût rendre tous les sites internets compatibles mobile ?"


Ue solution pas chère est faite par défaut :

 * générer le site sur un écran viruel 800 par 600 
 * Faire un scalling pour faire "rentrer cela" dans l'écran du smartphone
 * Considérer que l'utilisateur connait le pinch to zoom pour naviguer dans le site.

 Et çà marche ! 

Cela marche mais on ne peut pas dire que cela est forcément le mieux.
L'utilisateur mobile n'a pas la même attente que l'utilisateur sur ordinateur, il veut avoir accès rapidement aux informations essentielles, sans fioritures.
On imagine que sur une smart watch par exemple un site comme méteo france serait largement plus dépouillé (sur une smartwatch elle afficherait un nuage ou un soleil et la temperature par exemple).

Typiquement nous voulons enlever des parties entières du sites suivant la taille de l'écran.


La première chose à faire donc c'est de demander aux navigateurs de ne plus faire l'algo précédent (puisqu'on va gérer nous-mêmes) dnas la balise `<head>` :


 `<meta name="viewport" content="width=device-width, initial-scale=1">`

<div class= "exercise">

 * Ajouter cette instruction au site de Chuck Norris et visualisez avec Chrome en choissisant un smartphone. Que constatez vous ?

</div>


Bon vous devez constatez que l'algo ne se fait plus. En gros le navigateur n'essait plus d'être intelligent : il va falloir prendre le relai.



## Les outils pour travailler ?

Outil de dévellopement Chrome !
Jusqu'ici on considéré que tus les outils de dévellopement d'Internet EXplorer Firefox et Chrome étaient égaux.
En fait celui de Chrome était déjà un peu meilleur :

  * auto completion des règles css ajoutées dynamiquement,
  * liste déruolante des valeurs possibles des champs,
  * plus rapide, etc.

Suivant les habitudes des devellopeurs cela peut être plus ou moins sujet à contreverse.
Mais pour le Reponsive design il n'y a pas photo : Chrome (ou son pendant libre Chromium) devient <strong>vraiment</strong> votre "best-friend-ever".

* Allez sur le site 
   https://iutdepinfo.iutmontp.univ-montp2.fr/
   https://infolimon.iutmontp.univ-montp2.fr/public/windows/chrome-win32.zip
* Appuyez sur F12 et cliquez sur la petite icone <img src="{{site.baseurl}}/assets/phone-responsive.png" alt="Outil opur mobile" style="margin: 0 auto;display: block;">


## La solution technique CSS3 :  les media queries



<div class= "exercise">
 * Ouvrez maintenant votre site de Chuck Norris avec Chrome en choisissant un téléphone (genre Galaxy S3) pour la visualisation). 
 Constatez que le site s'affiche en tout petit. 
 * Allez sur le site  Bootstrap .... constater les points de ruptures 

</div>

Idée :
3 Poiins de ruptures : 
480px
768px
992px
1200px
<div class="exercise">
 - en dessous de 768px ne plus afficher la table de comparaison. (De toute façon s'il ne doit rester qu'un seul, ce sera Chuck Norris)
 - supprimer les marges latérales en dessous de 768px
 - optionnel sur une smartwatch (width 168 pixels) n'affichez que les citations de Chuck Norris contenu dans le aside.
</div>



### Le bouton burger !


* menu burger qui arrive de la gauche, par dessus la page, et qui grise le reste
de la page ? Le grisé avec une couche noire et de la transparence

Note :

* le hover sur les sous-menus n'a pas de sens sur téléphone portable. Il faudra
  gérer le clic avec du JS. Et dire, la bonne solution est ... et vous la verrer
  en 2ème année.



## Une solution plus pratique que les media queries 

### Le classique 12 colonnes.


### Responsive images 

* image responsive avec srcset ?

## Coment çà il est moche votre site de Chuck Norris ?

Au hasard d'une conversation entendue, il semblerait que le design utilisé pour le site ne fait pas l'hunanimité.
Certains seraient même allé jusqu'à dire que le site est môche.

Comment faire du beau, ergnomique, etc ?
et bien tout d'abord il s'agit d'autres métiers !

 * le  Web Designer 
 * l'Ergonome 


 Cela dit il est biensur essentiel d'être sensibilié à ces aspects.

Un ensemble de "guidelines" sont souvent associés à un 

https://www.google.com/design/spec/material-design/introduction.html

Notamment pour les couleurs :
https://www.google.com/design/spec/style/color.html#color-color-palette


## Autres Idées 

Beau layout pour les formulaires

Parler rapidement des caractères spéciaux en HTML &lt; < ... et peut-être aussi
de l'encodage des caractères dans l'URL quand on fait les formulaires


::before
::after
content, numérotation automatique (voir les div.exercise dans les pages du cours)


---> + ou -.
--->J'ai peur qu'ils s'imaginent qu'on peut foutre du HTML dans du css ...


border-image, border-shadow : c'est peu technique mais bien visuel
curseur : idem
inclusion d'audio, vidéo

--->Le border image et le border shadow pourrait en effet être intéressant !
--->On peut faire des choses jolies avec.

CSS columns

--->Si c'est çà :
--->http://caniuse.com/#search=column

--->J'en ai jamais entendu parlé...et puis j'ai l'impression qu'avec flex on peut tout faire.


max-wdth max-height
--->on pourrait utiliser vmin pour faire un sticky footer (pour la page contact on veut que le footer soit en bas de la page no même si le contenu de la page est inférieur à la taille écran).
---> dans le responsive design cela arrive plus ou moins naturellement je crois.


overflow

z-index associé à l'attribut position , lorsque les éléments se trouvent les uns sur les autres

les ordres  de contraintes sur auto entre width et margin pour un élément sur contraint

la fusion des marges.


#d'autres éléments HTML
1. select

1. button

1. textarea 

1. Form



caniuse preisentation



### holly grail layout

Nous sommes en 2015, et jusquà peu il n'est toujours pas évident de faire ce layout (d'où son nom).

https://philipwalton.github.io/solved-by-flexbox/

## Media Object



## box-model

## le model par défaut

## le border-layout

<!-- On peut aussi parler des sélecteurs de base sur les attributs -->




1. Faire une [lettrine](https://fr.wikipedia.org/wiki/Lettrine) en début du paragraphe "Après son mariage, il rejoint... " (il vous sera nécessaire de rajouter une classe `<span>` autours de la lettre A)



Exemple de site en flex layout

http://heckhouse.com/

quizzz

http://espn.go.com/espn/feature/story/_/id/13035450/league-legends-prodigy-faker-carries-country-shoulders

Comment est fait le T de Two years ago qui commence l'article ?
Quel est le problème à propos du deuxième paragraphe ?


## Fini !

Mais que se passe t il lorsque l'on visualise notre superbe layout sur un petit écran genre mon smartphone ?
et pls généralement comment avoir un layout intelligent qui s'adapte à ma tablette ? ma smartwatch ? mon smartphone ? mon rétro projecteur ?


Responsive design 

Un layout repsonsive simple avec Flex

Un layout grid avec Flex

Les images
