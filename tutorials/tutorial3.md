<!--
Si on repousse cet exo on peut parler plus en profondeur des contraintes de tailles sur le premier  block avec une size, et les ordres 
de contraintes sur auto entre width et margin
-->

1. select

1. button

1. textarea 

1. Form

1 Cacher un élément 
différence entre
 * display:none 
 * visibility:hidden


1. Faire une [lettrine](https://fr.wikipedia.org/wiki/Lettrine) en début du paragraphe "Après son mariage, il rejoint... " (il vous sera nécessaire de rajouter une classe `<span>` autours de la lettre A)



## L'attribut display


### block

### inline

### inline-bloc

### les autres (tables, flex)
1. Flex Layout

Exemple de site en flex layout

http://heckhouse.com/


## Ordre d'application des sélecteurs CSS.


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
le joker, un aveu d'échec...




