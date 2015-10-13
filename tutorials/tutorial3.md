---
title: TD3 &ndash; HTML / CSS avancé 2/2
subtitle: display property and Layout
layout: tutorial
---

## Display 

A chaque élément HTML d'un page lui correspond une boite (voir le box model du TD précédent).
La façon dont cette boite va occuper l'espace est géré par l'attribut display.
Nous verrons dans cette section les quatres valeurs princpales de display.

Par exemple : 

 * un paragraphe `<p>` va il voir son espace grandir par le texte qu'il contient ?
 * Lorsque l'on ajoute un header qui va contenir la navigation d'un site, sa place est elle dictée par son contenu ou a elle plutôt tendance à occuper un espace fixe ?


### block

Lors du TD1, nous sommes parti d'un texte d'un seul tenant illisible.
Afin de spérarer ce texte en sections séparées par des titres nous avons ajouter des titres `<h2>` et `<h3>`.
L'ajout de cette structure au HTML a e uun impacte visuel sur le rendu  : les titres ont occupé une ligne complète, forcant un retour à la ligne avant et après eux.
C'est que ces éléments sont de type block.


### inline

...

### Exercices ?



## Cacher ou Enlever un élément du rendu

Il existe plusieurs façons de faire disparaitre de l'écran un élément HTML.

### cacher display:none 

### enlever visibility:hidden


<div class="exercise">

1. combiner avec li:hover img, visibility:default pour liker un lien (ou un site)


</div>

### suite des positions

menu avec position:absolute pour ne pas décaler le corps de la page

## Ordre d'application des sélecteurs CSS.


<!-- On peut aussi parler des sélecteurs de base sur les attributs -->

<!--

Rajouter référence MDN ???

Parler aussi des pseudo-éléments type ::first-letter ?
::after
::before
::first-letter
::first-line

MDN : Tout comme les pseudo-classes, les pseudo-éléments sont ajoutés aux
sélecteurs. Mais au lieu de décrire un état spécial, ils permettent de styler
certaines parties du document.

<style type="text/css">
p::first-letter { font-size:1.4em; }
</style>

-->

Il a plusieurs emplacements pour déclarer du style CSS.
Nous commençons par préciser ces dernières et donner leurs ordre de priorité.

### priorité du style par emplacement.
Nous avons utilisé un ficher de style externe styles.css pour ajouter des règles CSS.
Il est aussi possible d'ajouter du CSS directement dans le HTML via l'attribut `style` (on parle de style "inline") :

~~~
<p style="font-size: 12pt; color: fuchsia">
   Aren't style sheets wonderful?
</p>
~~~
{:.html}

Ou d'inclure des règles CSS dans une balise `<style>` (on parle de "internal style"):


~~~
<style type="text/css">
   p {font-size: 12pt; color: pink}
</style>
~~~
{:.html}

Enfin les navigateurs appliquent un style par défaut sur les éléments.
Cela permet de ne pas avoir à définir pour chaque balise tout le style qui doit lui être associé.

L'ordre de priorité d'application des règles CSS est la suivante :

1. styles 'inline' par l'attribut `style` à même le HTML,
1. styles contenu dans les fichiers CSS (external style),
1. styles définis dans une balise `<style>` dans le fichier HTML (internal style),
1. style par défaut des navigateurs.


En pratique on préférera les styles externes comme "styles.css", cela respecte mieux la césure entre la structure HTML et le style CSS. 


### Priorité des règles par leurs sélecteurs.

Des règles CSS rentrent inévitablement en conflit sur certains éléments :

~~~
div {color: yellow;}
div.toto {color: red;}
~~~
{:.css}

Afin de savoir la couleur qui sera appliquée sur les éléments `<div>` ayant la classe toto, des priorités sont définis sur les sélecteurs CSS.

Cette priorité est une valeur (a,b,c,d) définie comme suit :

 * soit a la règle est dans un style inline (voir plus haut), (a=1 si le style est inline, 0 sinon)
 * soit b est le nombre de sélecteur d'identifiant (`#`),
 * soit c est le nombre de classe (`.`) ou pseudo classe (`:over`,`:visited`,...)
 * soit d est le nombre d'élément contenu dans le sélecteur (`div` , `span`, `p`, ...)

l'ordre de priorité est défini comme lexicographique (la valeur de a est plus discriminante que b qui lui même est plus discriminant que c). 

Pour revenir à l'exemple précédent, les règles ont donc comme priorité  :

~~~
 div -> (0,0,0,1) (un élément div)
 div.toto -> (0,0,1,1) (une classe toto et un élément div)
~~~
{:.html}


Soit la fonction `cssprior` qui à un sélecteur CSS donne sa priorité `(a,b,c,d)`, 
voici quelques exemples d'ordre.
Vérifier bien que les ordres suivants vous semblent normal :

~~~
 cssprior(.titi span ) >= cssprior(div span)
 cssprior( nav.titi .tata + div div div div div  > ul li div.toto) 
    <= cssprior(#truc)
 cssprior(div > a) == cssprior(div + a)
~~~
{:.html}



C'est donc la deuxième qui sera appliquée (sur les div ayant la classe toto bien sûr).


Remarque si deux règles ont la même priorité, alors c'est l'emplacement de leurs déclaration (inline, ficher externe, style interne, style par défaut) qui prévaut 
et si les deux règles sont dans le même emplacement, alors c'est le dernier qui l'emporte.


### le joker en cas d'impasse !important 

 Le style inline ne peut être dépassé par les règles CSS dans notre fichier styles.css. 
De plus nous pourrions utiliser des CSS externes et vouloir écraser certaines de ces règles pourtant très précises. 
 Pour cela le CSS propose la règle !important : 

~~~ 
div {color: yellow !important;} 
div.toto {color: red;} 
~~~ 
 {:.css} 

Elle permet de rendre la règle plus prioritaire que l'ordre (a,b,c,d) de n'importe quelle règle qui n'a pas le `!important`. 
Nous en parlons juste pour être exhaustif sur les règles de priorité : en pratique, `!important` est très peu utilisé, c'est le dernier recours,  


## Display avancés

### inline-block

### Flexbox

https://css-tricks.com/snippets/css/a-guide-to-flexbox/


## Layout

### Column layout


### holly grail layout

Nous sommes en 2015, et jusquà peu il n'est toujours pas évident de faire ce layout (d'où son nom).

https://philipwalton.github.io/solved-by-flexbox/

## Media Object


## vertical centering


## box-model


## le model par défaut

## le border-layout

