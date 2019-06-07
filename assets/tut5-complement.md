---
title: Compléments du TD5 &ndash; Responsive Design
subtitle: Framework CSS, grille à 12 colonnes
layout: tutorial
---

## Compléments (optionnels) au TD

<!-- ### Responsive images  -->
<!-- * image responsive avec srcset ? -->

### Les framework CSS

Dans vos futurs projets Web, vous serez sûrement amenés à utiliser des framework
CSS tels que [Foundation](http://foundation.zurb.com/) et
[Bootstrap](http://getbootstrap.com/css/). Ces logiciels vous donneront accès à
un certain nombre éléments d'interface CSS clés en main pour pouvoir concevoir
un site Web responsive (boutons, formulaires, menus, ...). 

**Le système de grille à 12 colonnes**  
L'un des éléments les plus importants des frameworks CSS est un systèmes de
grille qui permet de créer facilement des mises en pages. L'arrivée du modèle
FlexBox a considérablement simplifié le code CSS derrière le framework (par
exemple, regardez le
[Flex Grid de Foundation](http://foundation.zurb.com/sites/docs/flex-grid.html)).

Notre but dans ce TD est de comprendre comment le modèle FlexBox permet de coder
facilement le modèle de grille. **Attention :** Nous n'utiliserons pas ces
frameworks dans ce cours (et encore moins dans le projet) mais nous souhaitons
démystifier leur fonctionnement.

Nous suivrons la présentation des fonctionnalités faites dans [le système de grille à 12 colonnes](https://getbootstrap.com/docs/3.4/css/#grid).

#### Les bases

Le système de grille permet de créer une boîte `<div>` qui se partitionne en
plusieurs colonnes. La largeur de ces colonnes est indiquée par un entier,
sachant que la largeur totale est de 12 unités. Selon la largeur totale de
l'affichage (`small` si `<640px`, `medium` pour `<1024px` et `large` sinon) nous
pouvons définir des largeurs variables pour nos colonnes.

**Exemple :** Le HTML suivant sert (en Foundation) à créer une boîte (de classe
  `row`) qui sera divisée en deux colonnes dont la largeur dépend de la taille de
  l'écran.

```html
<div class="row">
  <div class="small-8 medium-6 large-4">8/6/4 columns</div>
  <div class="small-4 medium-6 large-8">4/6/8 columns</div>
</div>
```

<div class="row">
<div class="small-8 medium-6 large-4">
8/6/4 columns
</div>
<div class="small-4 medium-6 large-8">
4/6/8 columns
</div>
</div>

<div class="exercise">
1. Utilisez le *device mode* de Chromium (une version récente, *cf*
précédemment), pour découvrir les points de rupture de la page. Observez la
taille des colonnes varier selon la taille de l'écran.

2. Comment coderiez-vous cette fonctionnalité ?  
   **Note :** Quand on spécifie une `width`, elle s'applique à la `content box`
     et donc n'inclut pas le padding ni la bordure. Il est souvent plus pratique
     de définir la largeur totale (padding et bordure incluse), auquel cas on
     rajoute `box-sizing:border-box;`.

<!-- Il y a besoin de media queries, de définir la largeur en pourcentage du parent -->
<!-- (avec border-box) et des flex box pour mettre deux boîtes à côté -->

</div>

#### Dimensionnement avancé

La classe `columns` permet de définir le comportement par défaut *"je prends la
place restante"*. Si plusieurs éléments ont la classe colonne, alors ils se
partagent équitablement la largeur restante.

```html
<div class="row">
  <div class="small-4 columns">4 columns</div>
  <div class="columns">Whatever's left!</div>
  <div class="columns">Whatever's left!</div>
  </div>
  <div class="row">
  <div class="small-8 medium-6 large-4">8/6/4 columns</div>
  <div class="small-4 medium-6 large-8">4/6/8 columns</div>
</div>
```

<div class="row">
<div class="small-2 columns">
2 columns if small
</div>
<div class="columns">
Whatever's left!
</div>
<div class="columns">
Whatever's left!
</div>
</div>

<div class="exercise">
1. Utilisez le *device mode* de Chromium (une version récente, *cf*
précédemment), pour découvrir les points de rupture de la page. Observez la
taille des colonnes varier selon la taille de l'écran.

1. Pour cet exemple précis, combien d'unités prennent respectivement les trois
colonnes selon si l'écran est `small`, `medium` ou `large` ?

   <!-- small 2/5/5, medium et large 4/4/4  -->

2. Comment coderiez-vous cette fonctionnalité ?

<!-- Il y a besoin de media queries. Et on va utiliser flex-grow:1 pour répartir la -->
<!-- largeur restante. Mais pour ne pas prendre en compte la largeur de base des -->
<!-- éléments en columns, on met une taille de base 0px. -->
<!-- Par exemple flex: 1 1 0px -->

</div>

À l'inverse, la classe `shrink` indique que le bloc ne prend que la place nécessaire.

```html
<div class="row">
  <div class="shrink columns">Shrink!</div>
  <div class="columns">Expand!</div>
</div>
```

<div class="row">
<div class="shrink">
Shrink!
</div>
<div class="columns">
Expand!
</div>
</div>

#### Ajustements réactifs

Pour faire que les colonnes s'empilent, il faut spécifier leur largeur à `12`
unités. Dans l'exemple suivant, les colonnes s'empilent sur petit écran et se
mettent côte à côte sinon.

```html
<div class="row">
  <div class="small-12 large-expand columns">One</div>
  <div class="small-12 large-expand columns">Two</div>
  <div class="small-12 large-expand columns">Three</div>
  <div class="small-12 large-expand columns">Four</div>
  <div class="small-12 large-expand columns">Five</div>
  <div class="small-12 large-expand columns">Six</div>
</div>
```

<div class="row">
<div class="small-12 large-expand columns">
One
</div>
<div class="small-12 large-expand columns">
Two
</div>
<div class="small-12 large-expand columns">
Three
</div>
<div class="small-12 large-expand columns">
Four
</div>
<div class="small-12 large-expand columns">
Five
</div>
<div class="small-12 large-expand columns">
Six
</div>
</div>

Ce comportement se trouve à l'aide de la propriété `flex-wrap:wrap;` qui indique
de passer à la ligne quand elle est pleine.

#### Autres

Nous vous laissons trouver par vous-même à quelles propriétés du Flexbox model
correspondent les autres fonctionnalités. Vous pouvez toujours inspecter le CSS
sur le site de Foundation pour découvrir la réponse et apprendre de nouvelles
techniques.

<!-- Pour comprendre flex-basis, voir -->
<!-- [https://developer.mozilla.org/fr/docs/Web/CSS/flex](https://developer.mozilla.org/fr/docs/Web/CSS/flex) -->

<!-- Tailles foundation -->
<!--   small: 0px, -->
<!--   medium: 640px, -->
<!--   large: 1024px, -->
<!--   xlarge: 1200px, -->
<!--   xxlarge: 1440px, -->

<!-- Flexgrid foundation -->

<!-- ```html
<!-- <div class="row"> -->
<!--   <div class="small-4 columns">4 columns</div> -->
<!--   <div class="columns">Whatever's left!</div> -->
<!-- </div> -->
<!-- ```

<!-- ```css
<!-- .row { -->
<!--   dislay:flex; -->
<!--   flex-wrap:wrap; -->
<!-- } -->
<!-- ```

<!-- ```css
<!-- @media () { -->
<!-- .small-4 { -->
<!-- flex: 0 0 33.33333%; -->
<!-- box-sizing : border-box; -->
<!-- } -->
<!-- } -->
<!-- ```

<!-- ```css
<!-- .columns { -->
<!--   flex: 1 1 0px; -->
<!-- } -->
<!-- ```

<!-- ```css
<!-- .shrink { -->
<!--   flex: 0 0 auto; -->
<!-- } -->
<!-- ```

<!-- ```css
<!-- @media() { -->
<!-- .medium-expand { -->
<!--   flex: 1 1 0px; -->
<!--   } -->
<!--   } -->
<!-- ``` -->


<style type="text/css">
.row {
    display:flex;
	margin: 24px 0;
	width:100%;
	background-color:#FBFBFB;
	flex-wrap:wrap;
}

.row > *:nth-child(odd) {
    background-color:#eee;
}

.row > * {
    padding : 0 15px;
    box-sizing:border-box;
	background-color:#cacaca;
}

.columns {
  flex: 1 1 0px;
}

.shrink {
  flex: 0 0 auto;
}

@media(min-width:1024px) {
    .large-2 {
	flex:0 0 16.6%;
    }

    .large-4 {
	flex:0 0 33.3%;
    }
    
    .large-6 {
	flex:0 0 50%;
    }
    
    .large-8 {
	flex:0 0 66.6%;
    }

    .large-10 {
	flex:0 0 83.3%;
    }

    .large-12 {
	flex:0 0 100%;
    }
}

@media (max-width:1023px) and (min-width:640px) {
    .medium-2 {
	flex:0 0 16.6%;
    }

    .medium-4 {
	flex:0 0 33.3%;
    }
    
    .medium-6 {
	flex:0 0 50%;
    }
    
    .medium-8 {
	flex:0 0 66.6%;
    }

    .medium-10 {
	flex:0 0 83.3%;
    }

    .medium-12 {
	flex:0 0 100%;
    } 
}

@media (max-width:639px) {
    .small-2 {
/* Or equivalently */
/*    width:16.6%; */
/*    flex:0 0 auto; */
    flex:0 0 16.6%;
    }

    .small-4 {
	flex:0 0 33.3%;
    }
    
    .small-6 {
	flex:0 0 50%;
    }
    
    .small-8 {
	flex:0 0 66.6%;
    }

    .small-10 {
	flex:0 0 83.3%;
    }

    .small-12 {
	flex:0 0 100%;
    }
}
</style>
