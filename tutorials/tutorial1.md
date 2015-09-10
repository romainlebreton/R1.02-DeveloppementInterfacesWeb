---
title: TD1 &ndash; HTML &#58; un langage à balises pour structurer logiquement les documents
subtitle: .
layout: tutorial
---

Nous pouvons considérer qu'un document (par exemple le document etudes.pdf) est
constitué d'éléments comme des paragraphes, des images, des mots importants, des
titres de sections ou encore des listes à puces.

Ces éléments et leur agencement structurent logiquement le document. Le HTML est
un langage permettant d'exprimer cette structure grâce à l'insertion de
mots-clefs, appelés balises, à l'intérieur d'un fichier contenant le texte du
document.

## Transformation d'un document texte en un document HTML

Récupérer le fichier etudes.txt (fichier de base de travail) et etudes.pdf (résultat à obtenir).

1. Ouvrir le fichier etudes.txt avec un navigateur.
2. Le HTML permet de décrire la structure logique d'un document. Par exemple,
   pour signifier que la première phrase est le titre du document, on peut ajouter
   la séquence de caractères <h1> (appelée balise ouvrante) devant et la séquence
   de caractères </h1> (appelée balise fermante) derrière. Observer le résultat
   dans le navigateur.
3. Renommer le fichier etudes.txt en etudes.html, ouvrir le fichier dans un
   navigateur et observer le résultat.
4. Dans le point n°4 "DUT Métiers du multimédia et de l'Internet", observer le
   problème que pose le mot "oeuvrant". Pour le résoudre, ajouter <meta
   charset="iso-8859-15"> en première ligne du document. Observer le résultat.
5. Utiliser le formulaire http://validator.w3.org/ pour faire analyser la
   conformité du document au standard html. Quel est le résultat ?
6. Pour que le document soit valide et reconnu comme un document HTML 5 il est
   nécessaire d'ajouter la ligne <!DOCTYPE html> au tout début du
   fichier. Réessayer de le valider.
7. L'entête du document est définie grâce à l'ajout des balises <head> et
   </head> qui doivent contenir la balise <meta>. Réessayer de le valider. Le
   validateur indique que l'élément head doit obligatoirement avoir un titre.
8. Insérer après la balise meta un titre "Etudes en Informatique" encadré par
   les balises <title> et </title>. Observer le résultat et envoyer le fichier au
   validateur. Le titre défini est utilisé pour renommer l'onglet du navigateur.


A ce stade, le validateur indique que le fichier etudes.html est un document HTML 5 valide.

## Structure standard d'un document HTML

1. Encadrer par les balises <body> et </body> toute la partie du document se trouvant
en dessous de </head>.
2. Insérer une balise <html> avant la balise <head> et une balise </html> après la
balise </body>.

Les balises HTML définissent une structure arborescente du document où :

* html est l'élément racine
* head et body sont les deux fils de l'élément html
* title et meta sont deux fils de l'élément head
* "Etudes en Informatique" est un fils de l'élément title.

## Titres

Utiliser les balises <h1> à <h3> pour identifier les titres du documents.

## Éléments de regroupement

### Paragraphes

Utiliser maintenant les balises <p> et </p> autour des paragraphes du document.

### Listes

~~~
<ul>
  <li>premier item</li>
  <li>deuxième item</li>
</ul>
<ol>
  <li>premier item</li>
  <li>deuxième item</li>
</ol>
~~~
{:.html}

1. Utiliser les balises `<ul>` et `<li>` pour structurer la liste à puces de la
section "A savoir".
2. Utiliser les balises `<ol>` et `<li>` pour structurer la liste numérotée de
la section "Post-BAC".
3. Essayez maintenant d'imbriquer une liste non-ordonnée dans une liste ordonnée
pour structurer la section "POST DUT : que faire avec mon DUT informatique en
poche ?"

## Image : un exemple d'élément embarqué

Télécharger l'image Etudes.png qui se trouve dans la section du Moodle et insérer la
balise ci dessous sous le titre principal du document HTML.

~~~
<img src="Etudes.png" alt="Nuages de mots composés de termes
relatifs aux études supérieures en informatique."/>
~~~
{:.html}

src et alt sont des attributs de l'élément img.

L'attribut alt permet d'ajouter un texte alternatif pour les navigateurs ne pouvant afficher
l'image.

## Éléments sémantiques

### Liens

1. Le code suivant permet de produire un lien vers le site web des licences pro
   d'informatique à l'IUT. Il s'ouvrira dans la fenêtre en cours.

   ~~~
   <a href="http://iutdepinfo.iutmontp.univ-montp2.fr/index.php/formations/licences-pro/">Les licences pro à l'IUT de Montpellier</a>
   ~~~
   {:.html}

2. Une image peut également servir de lien hypertexte : il suffit que l'élément
   img soit défini comme un fils d'un élément a. Faire pointer le nuage de mots
   Etudes.png vers l'adresse suivante :
   www.letudiant.fr/etudes/secteurs/informatique-multimedia.html

3. Il est également possible de mettre des liens « internes » à une page HTML
   donnée, par exemple en déclarant une « ancre » intitulée «top» de la manière
   suivante au début de votre document : <a name="top"></a>.  Vous pourrez alors
   permettre à l'utilisateur de remonter au début de la page web en définissant le
   lien suivant en fin de document : <a href="#top">Remonter en haut de la page</a>

### Citation

Utiliser la balise <cite> pour entourer le nom de l'auteur de la citation "Le
seul mauvais choix est l'absence de choix." et la balise <blockquote> pour
entourer la citation et le nom de l'auteur.

### Emphase

La balise <em> permet de mettre en évidence des passages importants dans un
texte. Identifier les mots en gras dans le document .pdf et les marquer avec cette balise
dans le fichier HTML.

## Pour les plus avancés

1. Passer le document sous l'encodage utf-8 (que nous priviligierons désormais).
2. Travaillez sur votre projet en définissant les structures HTML des pages de votre site web.
