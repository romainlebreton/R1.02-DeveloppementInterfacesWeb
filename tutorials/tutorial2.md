---
title: Les bases du HTML / CSS
subtitle: .
layout: tutorial
---

# CSS: un langage pour définir la mise en forme

Définition (source : Wikipedia) : CSS (Cascading Style Sheets : feuilles de
style en cascade) est un langage informatique qui sert à décrire la présentation
des documents HTML et XML. Les standards définissant CSS sont publiés par le
World Wide Web Consortium (W3C). Introduit au milieu des années 1990, CSS
devient couramment utilisé dans la conception de sites web et bien pris en
charge par les navigateurs web dans les années 2000.

En pratique, les CSS servent à séparer les données (HTML) de la présentation
(CSS). Cela permet de concevoir des sites évolutifs et maintenables ! Vous
pouvez voir sur le site http://www.csszengarden.com à quel point l'utilisation
des CSS est importante.  Pour vérifier que vos documents respectent les
standards, une seule adresse : http://validator.w3.org.

## Tutoriel d'introduction
Le code ci-dessous, appelé règle css, permet de définir des titres de couleur rouge sur
fond blanc.

~~~
h1 {
  color: red;
  background: white
}
~~~
{:.css}

Recopier la règle ci-dessus dans un fichier etudes.css à mettre le même répertoire que le
fichier HTML.

Pour indiquer au navigateur qu'il doit utiliser les règles de style de ce fichier pour le document
HTML il faut ajouter la ligne suivante dans l'en-tête du document HTML :

~~~
<link rel=‘’stylesheet’’ type=‘’text/css’’ href=‘’etudes.css’’>
~~~
{:.html}

## Couleurs

Les mots aqua, black, blue, fuchsia, gray, green, lime, maroon, navy, olive, orange, purple, red,
silver, teal, white, et yellow peuvent être utilisés pour définir une couleur.

Définir une couleur pour le fond du corps du document.

## Fontes

référence : http://www.w3.org/TR/CSS21/fonts.html

### La propriété font-family

Rajouter maintenant la règle suivante :

~~~
p{ font-family: "lucida calligraphy", "Arial", sans-serif; }
~~~
{.css}

### la propriété font-size

Utiliser la propriété font-size pour changer la taille de la citation.

## Textes

Tester les règles ci-dessous :

~~~
p {
  text-align: justify ;
  text-indent: 1em;
}

h1 { text-transform : uppercase;}
~~~
{.css}

Aligner la citation en début de document à droite de la page.

# Sélecteurs

## Regroupement

Il est possible de regrouper les sélecteurs :

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

### Classes

Il est aussi possible de définir un style pour un sous-ensemble (une classe) d'éléments de même
type. Par exemple la règle ci-dessous ne concerne que les paragraphes appartenant à la classe des
paragraphes importants :

~~~
p.important{ border-style: solid }
~~~
{:.css}

Côté HTML on peut assigner un élément à une classe en définissant pour cet élément son attribut
class :

~~~
<p class="important"> Texte du paragraphe... </p>
~~~
{:.html}
