---
title: TD1 Partie 1 &ndash; HTML - un langage à balises pour structurer les documents
subtitle: Doctype et premières balises
layout: tutorial
---

Le but de ce TD est de comprendre comment sont écrites les pages Web basiques,
aussi appelées pages statiques (Web 1.0). Une telle page Web contient deux
parties :

1. **HTML** : Le fichier HTML contient la structure de la page et son contenu ;
en plus du texte brut, il donne du sens au texte en indiquant ce qui relève
d'un paragraphe, d'un titre, *etc*, à l'aide de balises (exemple `<p>`,
`<title>`,...);

2. **CSS** : Le fichier CSS est responsable de la mise en page de ces éléments
   (mettre ce paragraphe en rose, utiliser la fonte "Sans Serif" pour ce
   titre,... )

Le navigateur (Firefox, Chrome, Safari, IE/Edge, ...) est le logiciel qui nous
permet de visualiser les pages Web. Le but de ce TD est de démystifier la façon
dont sont interprétés ces deux types de fichiers par le navigateur.
Pour cela nous allons réaliser un site dont le rendu correspond au fichier
[target.png]({{site.baseurl}}/assets/target.png), en partant du fichier
[index.txt]({{site.baseurl}}/assets/index.txt), qui contient le contenu quasiment
"brut" du site à réaliser.

Nous allons tout d'abord nous consacrer à préciser la structure (le HTML donc)
que l'on peut ajouter à notre contenu brut. Nous verrons ensuite dans la
[deuxième partie du TD](tutorial1_2.html) comment atteindre le rendu proposé par
[target.png]({{site.baseurl}}/assets/target.png) en réalisant un fichier CSS.


## Transformation d'un document texte en un document HTML

Le HTML, qui signifie *HyperText Markup Language* (langage de balisage
d’hypertexte), est donc un langage à balise contenant des liens, dits
*hypertextes*, vers d'autres documents.

Les balises permettent de structurer le document. La plupart des balises
commencent par une *balise ouvrante* `<mabalise>`, puis du *contenu* et
finissent par une *balise fermante*
`</mabalise>`. [Certaines balises](http://www.w3.org/TR/html5/syntax.html#void-elements)
n'acceptent pas de contenu et consistent juste d'une balise ouvrante.

<!--  http://www.w3.org/TR/html5/syntax.html#void-elements -->

**Exemple :**

~~~
<p>Ceci est un paragraphe HTML puisqu'il est entouré des balises 'p' </p>
La balise 'br' du saut de ligne ne prend pas de contenu <br>
~~~
{:.html}

Nous allons commencer par des balises un peu particulières qui sont là pour
donner des informations sur le document.

<div class="exercise">

1. Ouvrez le fichier [index.txt]({{site.baseurl}}/assets/index.txt) dans le navigateur.

2. Sauvegardez ce fichier en local dans un dossier `HTMLCSS/TD1/` en le
renommant `index.html`. Ouvrir le fichier dans un navigateur. Quelles
différences observez-vous ?

  
3. Notre document `index.html` est bien interprété comme un document HTML par le
navigateur. Cependant que se passe-t-il lorsque l'on teste sa conformité au
standard html à l'aide du validateur
[http://validator.w3.org/](http://validator.w3.org/) . Quelles sont les erreurs
indiquées ?

   **Note :**

   * Le HTML5 est un standard, c'est-à-dire un langage complètement
   décrit. N'hésitez pas à jeter un rapide coup d'œil
   [à sa spécification](http://www.w3.org/TR/html5/). Ce document est très technique
   mais complet.
   * Si le validateur ne marche plus, un validateur alternatif est
   [https://html5.validator.nu/](https://html5.validator.nu/).

4. Commençons par l'erreur **Unable to Determine Parse Mode!**. La validateur
veut vous dire qu'il ne sait pas dans quel langage est écrit votre document. Il
existe plusieurs standards de "langages HTML" : HTML4, XHTML, HTML5,
.... Aujourd'hui, les gens utilisent majoritairement HTML5 et nous ferons de
même.  
   Pour que le document soit valide et reconnu comme un document HTML 5,
   **ajoutez** la ligne

   ~~~
   <!DOCTYPE html>
   ~~~
   {:.html}
   
   au tout début du fichier. **Retestez** la conformité de votre document.

5. Le validateur nous indique **The character encoding was not declared**.
Spécifier l'encodage des caractères est nécessaire pour que les caractères
spéciaux (accents, œ, ...) de votre page soient bien affichés. Dans notre cas,
nous utiliserons toujours l'encodage UTF-8.  
   **Rajoutez** donc la ligne suivante qui déclare l'encodage dans l'en-tête du
   document juste après le DOCTYPE. **Retestez** la conformité de votre document.

   ~~~
   <meta charset="utf-8">
   ~~~
   {:.html}

   **Note :** Vous avez sûrement rencontré des pages Web avec des **Ã©**, **Ã¨**,
     .... Ceci est dû à une mauvaise détection de l'encodage. En effet, le code
     du caractère **é** en UTF-8 correspond à **Ã©** en `iso-8859-15` (encodage
     encore très utilisé dans Windows).

4. La dernière erreur nous parle d'un élément `head` auquel il manque un `title`.
Corrigez votre page Web en insérant un titre après le `<meta>`.

   ~~~
   <title>Le site non officiel de Chuck Norris</title>
   ~~~
   {:.html}

</div>

À ce stade, le validateur indique que le fichier `index.html` est un document
HTML5 valide.

<!--
La dernière erreur nous parle d'un élément `head` auquel il manque un `title`.
Nous allons corriger cela dans la section suivante.
-->

## Structure standard d'un document HTML

La bonne structure d'une page HTML est :

~~~
<!DOCTYPE html>
<html>
    <head>
        <!-- L'en-tête du document avec au moins un titre -->
        <title>Un titre qui s'affiche dans l'onglet du navigateur</title>
    </head>
    <body>
	   <!-- Le corps du document -->
	</body>
</html>
~~~
{:.html}


Après la ligne `<!DOCTYPE html>` de déclaration du langage, le document est
inclus dans la balise `<html>` et est composé de deux parties :

* l'en-tête `<head>` contient des informations sur le document HTML
* le corps `<body>` contient le vrai contenu

Les balises HTML donnent une structure d'arbre au document. Dans notre exemple
`index.html`

~~~
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Le site non officiel de Chuck Norris</title>
    </head>
    <body>
	   ...
	</body>
</html>
~~~
{:.html}

<div style="float:right">
<p style="margin:0">
<img alt="Structure d'arbre" src="{{site.baseurl}}/assets/arbre.svg">
</p>
</div>

l'arbre est le suivant :


* html est l'élément racine
* head et body sont les deux fils de l'élément html
* title et meta sont deux fils de l'élément head
* "Le site non officiel de Chuck Norris" est un fils de l'élément title.

<div style="clear:both" class="exercise">
Mettez à jour votre page `index.html` pour qu'elle respecte la structure HTML
ci-dessus. (Vous devez rajouter les balises `<html>`, `<head>` et `<body>`)
</div>

<!-- Explication orale sur l'importance de la validation : standard, uniformité -->

## Outils de développement Web

Dans la suite du TD, nous allons utiliser notre navigateur pour "inspecter"
notre page internet.  Pour cela nous conseillons Chrome ou Firefox. Appuyer sur
la touche `F12`. Les outils de développement affichent deux parties bien
distinctes, une dédiée au HTML et l'autre...aux CSS.  Ces outils sont fabuleux
pour apprendre comment se construit une page internet.

Il y a trois façons de s'intéresser à un élément en particulier :

* Un clic droit avec la souris dans la page affichée, suivi d'un
  "Inspecter/Examiner l'élément", permet de voir le code HTML correspondant dans
  l'outil de développement.
* Un clic sur ![inspecteur]({{site.baseurl}}/assets/magnifying.png) dans l'outil
de développement permet d'aller inspecter une zone d'intérêt dans la page (par
survol avec la souris).
* Quand on passe la souris au-dessus d'un élément dans l'outil de développement,
  il le colore dans la page.

<div class="exercise">

Familiarisez-vous avec ces trois techniques en inspectant la page du TD.  Par
exemple faite un clic droit sur l'élément "il y a trois façons..." puis
"inspecter l'élément".  L'outil de développement doit vous présenter le code
HTML et vous positionner directement sur `<p>Il y a `.

</div>

<!-- Hé ! ceci est un commentaire HTML, vous n'êtes pas censé le voir, à moins
que vous ne sachiez utiliser les outils de développeurs ? -->

## Les Commentaires en HTML

Il est possible de rajouter des commentaires dans le HTML. Ces commentaires ne
sont pas interprétés par le navigateur, et ne sont donc pas affichés (mais ils
restent présents dans le code source).  Il s'agit donc d'informations laissées par
des développeurs pour des développeurs. On les place entre les balises `<!--`
et `-->` :


~~~
<!--Cela est un commentaire dans un fichier HTML  -->
~~~
{:.html}

Il y a justement des commentaires dans le fichier index.html, comme autant de consignes afin de les remplacer par du HTML.
Nous expliciterons ces dernières dans les sections suivantes.

## Titres

Nous allons commencer par rajouter de la structure à notre page.  Pour ce faire
nous allons utiliser les balises `<h1>` à `<h6>` pour identifier les différentes
sections :

* `<h1>` est utilisé pour les gros titres du document
* `<h2>` est utilisé pour les sections du document
* `<h3>` est utilisé pour les sous-sections du document et ainsi de suite.

Par exemple, le titre ci-dessus est obtenu avec le code suivant (et vous pouvez
le vérifier en inspectant) :

~~~
<h2>Titres</h2>
~~~
{:.html}

Si vous cherchez un bon exemple d'utilisation de balises `<h2>`, inspectez le
titre **Titres** juste au-dessus en faisant un clic droit dessus.

<div class="exercise">

1. Ajoutez la balise `<h2>` aux éléments de `index.html` marqués par les commentaires : `<!-- section -->`.
2. Ajoutez la balise `<h3>` aux éléments de `index.html` marqués par les commentaires : `<!-- sous section -->`. 

</div>

## Éléments de regroupement

### Paragraphes

Utilisez maintenant les balises `<p>` et `</p>` autour des paragraphes du
document. Les paragraphes vous sont signifiés par `<!--début paragraphe -->` et
`<!--fin paragraphe -->`.

**Note :** Si vous faites un clic droit suivit de "inspecter l'élément" sur
ce paragraphe, vous verrez justement que ce texte est dans un paragraphe.


### Listes

En HTML nous pouvons faire des listes ordonnées (numérotées) ou non ordonnées :

~~~
<ul> <!-- ul pour unordered list -->
  <li>premier item non ordonné </li> <!-- li pour list item -->
  <li>deuxième item</li>
</ul>
<ol> <!-- ol pour ordered list -->
  <li>premier item ordonné </li>
  <li>deuxième item</li>
</ol>
~~~
{:.html}

Ce qui donne une fois interprété par le moteur de rendu du navigateur :

<div class="codeexample">
<ul>
  <li>premier item</li>
  <li>deuxième item</li>
</ul>
<ol>
  <li>premier item</li>
  <li>deuxième item</li>
</ol>
</div>

<b>Exercice : </b>

1. Utilisez les balises `<ul>` et `<li>` pour structurer la liste à puces
`<!--liste -->` dans `index.html`.  
(Ne vous souciez pas encore des commentaires `<!-- lien externe -->`)
2. Utiliser les balises `<ol>` et `<li>` pour structurer la liste numérotée
   `<!--liste numérotée -->` dans `index.html`.
3. Pensez à valider régulièrement votre page pour la vérifier. Rappel : adresse
   du validateur [https://validator.w3.org/nu/](https://validator.w3.org/nu/).

## Image : un exemple d'élément embarqué

Pour insérer une image, on peut utiliser la balise

~~~
<img src="adresse_image" alt="texte alternatif mais obligatoire">
~~~
{:.html}

Cette balise n'a pas de balise fermante car elle ne peut avoir de contenu
(cf. [le début du TD](#transformation-dun-document-texte-en-un-document-html)).
On remarque qu'elle possède deux champs `src` et `alt` que l'on appelle les
*attributs* de la balise. Précédemment, on avait vu une autre balise avec un
attribut: `<meta>` avec l'attribut `charset`. Les attributs se trouvent toujours
dans la balise ouvrante.

L'attribut `src` doit contenir l'adresse de l'image. L'attribut `alt` permet
d'ajouter un texte alternatif pour les navigateurs ne pouvant les afficher
(navigateur textuel <a href="http://lynx.browser.org/">Lynx</a>) ou pour les
personnes ne pouvant pas bien les distinguer (aveugles ou déficits visuels légers).



1. Enregistrez l'image
[chuck-jeune.jpg]({{site.baseurl}}/assets/chuck-jeune.jpg) dans un
répertoire `images` par rapport à votre fichier `index.html`.

2. Remplacez le commentaire `<!--l'image de Chuck Young doit être positionnée
ici -->` par la balise `<img>` suivante

   ~~~
   <img src="./images/chuck-jeune.jpg" alt="Une photo de Chuck Jeune, la légende est en marche."/>
   ~~~
   {:.html}

3. Faites de même avec l'image [beware.jpg]({{site.baseurl}}/assets/beware.jpg)
   à positionner en lieu et place du commentaire `<!--l'image de Chuck Beware
   ici -->`.

## Éléments sémantiques

### Liens externes

L'un des éléments les plus emblématiques du HTML est sans doute la balise
`<a>`. Elle permet de faire des liens hypertextes (le HT dans HTML).

Un lien est composé principalement d'une URL cible et d'un libellé (le texte
cliquable souvent souligné en bleu):

~~~
<a href="http://urlcible">le libellé</a>
~~~
{:.html}

On peut renseigner l'URL complète de la
cible (URL en chemin absolu):

~~~
<a href="http://lynx.browser.org/">Lynx</a>
~~~
{:.html}
   
ou donner une adresse relative à la page courante (URL en chemin relatif)
   
~~~
<a href="images/chuck-jeune.png">Image</a>
~~~
{:.html}

1. Remplacez les commentaires `<!-- lien externe ...` par des balises `<a>` avec
   la bonne adresse.

### Liens internes

On peut rajouter à ces *liens externes* une partie *lien interne* basée sur les
ancres `#monancre`. Toutes les balises peuvent prendre un attribut `id` comme
dans l'exemple suivant

~~~
<h2 id="un_identifiant">
~~~
{:.html}

Attention, la valeur de cet attribut doit être unique dans le document. On peut
alors faire un lien vers cette balise en rajoutant `#un_identifiant` à la fin
de l'URL. Exemple de lien interne à la page Web courante `index.html` :

~~~
<a href="index.html#un_identifiant">Exemple de lien interne</a>
~~~
{:.html}

<!-- verif cette adresse -->

Un exemple important est l'URL `#ancre` : le lien externe est vide, ce qui
correspond au document courant. Donc ce lien va vers la balise d'identifiant
`id="ancre"` du document courant.

1. Remplacez le commentaire `<!-- lien interne ...-->` de `index.html` par une
balise `<a>` qui pointera sur l'une des premières balises. Vous aurez donc
besoin de rajouter un identifiant à cette balise cible.

<!--
### Table 

Les tables.
-->

### Emphase

La balise `<em>` permet de mettre en évidence des passages importants dans un
texte. 

1. Justement, il faut mettre en exergue le fait que Chuck Norris est très fort dans différents arts martiaux.
Pour cela il faut mettre en emphase la phrase qui suit le commentaire : `<!-- mettre en emphase cette phrase -->` dans le fichier `index.html`.

**Note :** Il existe un autre type d'emphase qui s'obtient avec la balise `<strong>`.

### Citation

Voici un magnifique exemple de citation :

<blockquote> 
Un biscuit ça n'a pas de 'spirit', c'est juste un biscuit. 
Mais avant c'était du lait, des oeufs. Et dans les oeufs, il 
y a la vie potentielle.  
<cite>Jean-Claude Van Damme</cite>
</blockquote>

Les citations permettent d'identifier un court texte sur lequel on veut attirer l'attention.
Cela est utilisé notamment pour montrer qu'on a du 'spirit'.

1. Allez voir le code source de notre citation à l'aide des outils de
développement. Quels sont les deux balises utilisées ?
<!-- `<blockquote>` et `<cite>` -->

1. La première balise (qui commence par un **b**) entoure la citation complète
   tandis que la deuxième (qui commence par un **c**) contient uniquement la
   référence (l'auteur, le livre, ...). Utilisez ces deux balises pour mettre en
   avant la citation en tout début de document (rechercher `<!-- utiliser
   blockquote ici -->`).

2. Avez-vous vérifié tout au long du TD que votre page HTML reste valide ?

## Fini !

Nous en avons fini en ce qui concerne le contenu et la structure de notre site.
Nous savons ajouter de la structure à une page HTML avec les balises spécifiques.


Une remarque peut être informulée de votre part : mais pourquoi le fait de
rajouter `<h1>` à un titre change effectivement l'apparence des titres ? cela
n'est pas à la charge du CSS justement ?  Les navigateurs appliquent des CSS par
défaut associés aux balises HTML (exemple : par convention les liens `<a>` sont en
bleus et soulignés sans que l'on est rien à faire).  Cela évite d'avoir
justement TOUT à refaire en CSS : des styles par défaut sont proposés.  Dans le
[TD suivant](tutorial1_2.html) nous verrons comment améliorer l'aspect du site.

<!-- Dans le devtools, elles s'appelent user agent rules -->

<!--
iframe
span
div
table
-->

<!--
Questions complémentaires :
- em et exemple avec marge de taille différentes à cause d'une taille de fonte parente différente
- comprendre les subtilités de px
- favicon
- background image (il m'a fait une valeur cover qui étire l'image)
- bord rond
- inclusion de mp3
<audio controls="controls><source ..> texte alternatif ..
-->

