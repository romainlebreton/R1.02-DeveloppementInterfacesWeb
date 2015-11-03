---
title: TD5
subtitle: OverConstraint, Fluid Layout, Responsive design, Mobile first...
layout: tutorial
---

## Introduction


## Overconstraint


### `max-with` et `min-with`


### problème complexe d'overconstraint (solution : FlexBox)


### problèmes plus complexes ...


Supposons maintenant que nous voulons carrément supprimer visuellement un élément d'un visuel sur notre mobile.
Ou même changer le layout de row en column pour utiliser le défilement. 
Ici nous n'avons pas de solution via Flex seul car nous voulons assujétir des règles CSS à certaines caractéristiques (des règles spéciales pour une taille d'écran maximum par exemple). Nous verrons dans la prochaine section comment cela est possible en CSS.


## Les outils pour travailler ?

Outil de dévellopement Chrome !
Jusqu'ici on considéré que tus les outils de dévellopement d'Internet EXplorer Firefox et Chrome étaient égaux.
En fait celui de Chrome était déjà unp eu meilleur :

  * auto completion des règles css ajoutées dynamiquement,
  * liste déruolante des valeurs possibles des champs,
  * plus rapide, etc.

Suivant les habitudes des devellopeurs cela peut être plus ou moins sujet à contreverse.
Mais pour le Reponsive design il n'y a pas photo : Chrome (ou son pendant libre Chromium) devient <strong>vraiment</strong> votre "best-friend-ever".

* Allez sur le site 
* Appuyez sur F12 et cliquez sur la petite icone <img src="{{site.baseurl}}/assets/phone-responsive.png" alt="Outil opur mobile" style="margin: 0 auto;display: block;">



<div class="exercise" >

 * Ouvrez maintenant votre site de Chuck Norris avec Chrome en choisissant un téléphone (genre Galaxy S3) pour la visualisation). 
 Constatez que le site s'affiche en tout petit. 
</div>


## Que fait mon navigateur web sur téléphone par défaut pour un site ?

"Gérard ? il y a des mobiles qui ont internet maintenant ? comment on fait pour afficher internet dedant ?"


Et bien oui, la question s'est posée, et il a fallut d'abord trouver une rpéonse pour afficher TOUS LES SITES DE L'UNIVERS qui avaient été créer jusque là. Mêeme ceux qui avaient connus le minitel.
Alors par défaut eun solution au rabai a été implémentée :

 * générer le site sur un écran viruel 800 par 600 
 * Faire un scalling pour faire "rentrer cela" dans l'écran du smartphone
 * Considérer que l'utilisateur connait le pinch to zoom pour naviguer dans le site .

 Et çà marche ! 

Mais on peut faire mieux : on veut pouvoir changer completement le design du site pour un msartphone. 

La première chose à faire donc c'est de demander aux navigateurs de ne plus faire l'algo précédent (puisqu'on va gérer nous-mêmes) dnas la balise `<head>` :


 `<meta name="viewport" content="width=device-width, initial-scale=1">`

<div class= "exercise">

 * Ajouter cette instruction au site de Chuck Norris et visualisez avec Chrome en choissisant un smartphone. Que constatez vous ?

</div>


Bon vous devez constatez que l'algo ne se fait plus. En gros le navigateur n'essait plus d'être intelligent : il va falloir prendre le relai.


## La solution technique :  les media queries



<div class= "exercise">

 * Allez sur le site  .... constater les points de ruptures 

</div>


<div class="exercise">

</div>

## Une solution plus pratique que les media queries 

### Le classique 12 colonnes.



### Responsive images 





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

Parler rapidement des caractères spéciaux en HTML &lt; < ... et peut-être aussi
de l'encodage des caractères dans l'URL quand on fait les formulaires

Faire du sass ... 

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