---
title: TD1 Partie 1 &ndash; HTML - un langage à balises pour structurer les documents
subtitle: Doctype et premières balises
layout: tutorial
---

<!-- Faire une note plus complète sur l'encodage des caractères -->



Le but de ce TD est de comprendre comment sont écrites les pages Web basiques,
aussi appelées pages statiques (Web 1.0). Une telle page Web contient deux
parties :

1. **HTML** : Le fichier HTML contient la structure de la page et son contenu ;
en plus du texte brut, il donne du sens au texte en indiquant ce qui relève
d'un paragraphe, d'un titre, *etc*, à l'aide de balises (exemple `<p>`,
`<title>`,...);

2. **CSS** : Le fichier CSS est responsable de la mise en page de ces éléments
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

<!-- <div class="exercise"> -->

<!-- Avant toute chose, nous allons nous servir de ce que nous avons appris dans -->
<!-- [l'introduction à -->
<!-- Git](https://gitlabinfo.iutmontp.univ-montp2.fr/valicov/tutoGit1ereAnnee/blob/master/README.md) -->
<!-- et créer un projet Git pour stocker les fichiers des TDs. Cela aura des -->
<!-- avantages : vous pourrez y accéder de chez vous, garder une trace de -->
<!-- votre avancée grâce aux messages de commit, ... -->

<!-- 1. Allez sur le [GitLab de l'IUT](https://gitlabinfo.iutmontp.univ-montp2.fr/) -->
<!--    puis créez un projet HTMLCSS. -->
   
<!-- 1. Dans un terminal, clonez votre projet git et ajoutez-y un dossier `TD1` : -->
<!--    ```sh -->
<!--    ~$ git clone git@gitlabinfo.iutmontp.univ-montp2.fr:votre_login/htmlcss.git HTMLCSS -->
<!--    ~$ cd HTMLCSS -->
<!--    ~/HTMLCSS$ mkdir TD1 -->
<!--    ``` -->

<!-- </div> -->


## Transformation d'un document texte en un document HTML

### Le rôle du navigateur

Comme dit précédemment, le rôle du navigateur (Firefox, Chrome, Safari, IE/Edge,
...) est de visualiser les pages Web. Donc le navigateur transforme un fichier
texte contenant du langage HTML / CSS en un affichage mis en page, avec des
images... 

<div class="exercise">

1. La page du TD est une page Web. Ouvrez les sources de cette page pour voir le
code HTML qui est utilisé pour afficher cette page (clic droit puis code
source ou `Ctrl+U`).

</div>

<div class="exercise">

Pour créer une page Web, il suffit de créer un fichier texte et de lui donner
l'extension `.html` pour que le navigateur comprenne qu'il doit l'interpréter
comme un document HTML.

1. Sauvegardez le fichier [index.txt]({{site.baseurl}}/assets/index.txt) en
   local dans le dossier `HTMLCSS/TD1/`.  
   Faites une copie `index.html` de `index.txt` dans le même dossier.
   <!-- Sauvegardez le même fichier [index.txt]({{site.baseurl}}/assets/index.txt) en -->
   <!-- local dans le dossier `HTMLCSS/TD1/` en **le renommant** `index.html`. -->

1. Ouvrez les deux fichiers [index.txt]({{site.baseurl}}/assets/index.txt) et
   `index.html` dans le navigateur.  
   Quelles différences d'affichage observez-vous ? Pourquoi ?  
   Comment sont affichés les sauts de ligne d'un document HTML ?  
   Comment est affiché un texte HTML entouré de `<!--` et `-->` ?
   <!-- saut de ligne mangés, mauvais accents, commentaire coupés : interprétation du HTML -->

</div>


### Le standard du langage HTML

Notre document `index.html` est bien interprété comme un document HTML par le
navigateur.

Le HTML, qui signifie *HyperText Markup Language* (langage de balisage
d’hypertexte), est donc un langage à balise contenant des liens, dits
*hypertextes*, vers d'autres documents.

Le HTML est un standard, c'est-à-dire un langage complètement décrit (n'hésitez
pas à jeter un rapide coup d'œil
[à sa spécification](http://www.w3.org/TR/html5/), un document très technique
mais complet).

<div class="exercise">
  
1. Testons la conformité de `index.html` au standard HTML5 à l'aide du validateur
   [https://html5.validator.nu/](https://html5.validator.nu/). Quelles sont les
   erreurs indiquées ?

2. Commençons par l'erreur

   ```text
   Error: Non-space characters found without seeing a doctype first. Expected <!DOCTYPE html>.
   ```

   Le validateur nous dit qu'il s'attendait à voir `<!DOCTYPE html>` au début de
   notre document. Cette balise sert à déclarer que le document est écrit en
   HTML5. En effet, il existe plusieurs standards de "langages HTML" : HTML4,
   XHTML, HTML5, ... Aujourd'hui, les gens utilisent majoritairement HTML5 et
   nous ferons de même.

   Pour que le document soit valide et reconnu comme un document HTML 5,
   **ajoutez** la balise `<!DOCTYPE html>` au tout début du
   fichier.  
   **Retestez** la conformité de votre document.

3. Le validateur nous indique **The character encoding was not declared**.

   L'encodage indique la façon dont le fichier est enregistré (UTF-8, ANSI,
   `iso-8859-15`, ...). Si la plupart des caractères sont enregistrés de manière
   standard, les caractères spéciaux (accents, œ, ...) peuvent être enregistrés de
   manière très différente.

   Lorsque l'encodage n'est pas spécifié, le navigateur risque d'afficher **Ã©** au
   lieu de **é** à cause d'une mauvaise détection de l'encodage. En effet, le
   caractère **é** est enregistré en UTF-8 de la même manière que **Ã©** est
   enregistré en `iso-8859-15` (encodage encore très utilisé dans Windows).

   Spécifier l'encodage des caractères est donc nécessaire pour que les caractères
   spéciaux de votre page soient bien affichés. Nous utiliserons toujours
   l'encodage UTF-8 (et idéalement tout le monde devrait aussi l'utiliser).

   1. **Rajoutez** donc la ligne suivante qui déclare l'encodage dans l'en-tête du
   document juste après le DOCTYPE. 

      ```html
      <meta charset="utf-8">
      ```

   1. Réouvrez `index.html` dans le navigateur et vérifiez que tous les accents
      s'affichent bien.

      **Note :** Si les accents ne marchent toujours pas, c'est parce qu'**il ne
        suffit pas** de dire que votre fichier est en UTF-8. Il faut aussi que
        votre fichier soit **bien enregistré en UTF-8**. Par exemple dans
        Notepad++, l'encodage est marqué tout en bas à droite. Vous pouvez
        convertir votre fichier en UTF-8 en cherchant dans les menus.

   1. **Retestez** la conformité de votre document.

4. La dernière erreur nous parle d'un élément `head` auquel il manque un
`title`.  Corrigez votre page Web en insérant un titre après le
`<meta>`. Avez-vous trouvé ce qui change à l'affichage ?

   ```html
   <title>Le site non officiel de Chuck Norris</title>
   ```

</div>

À ce stade, le validateur indique que le fichier `index.html` est un document
HTML5 valide.

## Structure usuelle d'un document HTML

### Les balises HTML

Nous avons vu dans l'exercice précédent nos premières balises `<meta>` et
`<title>`.  Les balises permettent de structurer le document. Elles annotent le
texte qu'elles contiennent et permettent donc d'y rajouter du sens. On distingue
deux types de balises :

1. La plupart des balises **englobent du contenu** : elles commencent par une
*balise ouvrante* `<mabalise>`, puis le *contenu* que l'on veut "annoter" et
finissent par une *balise fermante* `</mabalise>`.  
Par exemple, la balise `<title>` sert à dire que le texte qu'elle englobe sera
le titre du document.

2. [Certaines balises](http://www.w3.org/TR/html5/syntax.html#void-elements)
**n'acceptent pas de contenu** : elles consistent juste d'une balise
ouvrante. On les appelle aussi balises auto-fermantes.
Par exemple, nous avons vu la balise `<meta>` et nous verrons bientôt `<img>`,
`<br>` ...

**Autres exemples :**

```html
<p>Ceci est un paragraphe HTML puisqu'il est entouré des balises 'p' </p>
La balise 'br' du saut de ligne ne prend pas de contenu <br>
```

### La structure de base

Servons-nous donc des balises pour créer une bonne structure de base de document HTML :

```html
<!DOCTYPE html>
<html>
    <head>
        <!-- L'en-tête du document avec au moins un titre -->
        <meta charset="utf-8">
        <title>Un titre qui s'affiche dans l'onglet du navigateur</title>
    </head>
    <body>
	   <!-- Le corps du document -->
	</body>
</html>
```


Après la ligne `<!DOCTYPE html>` de déclaration du langage, le document est
inclus dans la balise `<html>` et est composé de deux parties :

* l'en-tête `<head>` contient des informations sur le document HTML, comme
  * un `<title>` (balise obligatoire)
  * un `<meta>` pour définir l'encodage

* le corps `<body>` contient le vrai contenu. Nous verrons des exemples de
  balises dans la section *Balises communes*.

### Un document HTML est comme un arbre

Les balises HTML donnent une structure d'arbre au document. Dans notre exemple
`index.html`

```html
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
```

<div style="float:right">
<p style="margin:0">
<img alt="Structure d'arbre" src="{{site.baseurl}}/assets/arbre.svg">
</p>
</div>

l'arbre est le suivant :

* `<html>` est l'élément racine
* `<head>` et `<body>` sont les deux fils de l'élément `<html>`
* `<title>` et `<meta>` sont deux fils de l'élément `<head>`
* "Le site non officiel de Chuck Norris" est un fils de l'élément `<title>`.

<div style="clear:both" class="exercise">

1. Mettez à jour votre page `index.html` pour qu'elle respecte la structure HTML
   ci-dessus.  
   (Vous devez rajouter les balises `<html>`, `<head>` et `<body>`)
2. **Retestez** la conformité de votre document.
<!-- 3. Enregistrez de temps en temps votre progression sous Git. Par exemple,  -->
<!--    ```sh -->
<!--    # Pour enregistrer l'état de tous les fichiers dans le dossier TD1 -->
<!--    ~/HTMLCSS$ git add TD1 -->
<!--    ~/HTMLCSS$ git commit -m "Exercice 5 TD1" -->
<!--    ~/HTMLCSS$ git push -->
<!--    # Pour vérifier que tout est en ordre -->
<!--    ~/HTMLCSS$ git status -->
<!--    ``` -->
   
</div>

<!-- Explication orale sur l'importance de la validation : standard, uniformité -->

## Outils de développement Web

Dans la suite du TD, nous allons utiliser notre navigateur pour "inspecter"
notre page internet.  Pour cela nous conseillons Chrome ou Firefox. Appuyer sur
la touche `F12`. Les outils de développement affichent deux parties bien
distinctes, une dédiée au HTML et l'autre...aux CSS.  Ces outils sont fabuleux
pour apprendre comment se construit une page internet.

Il y a trois façons de s'intéresser à un élément en particulier :

* Un clic droit avec la souris dans la page affichée, suivi d'un
  "Inspecter/Examiner l'élément", permet de voir le code HTML correspondant dans
  l'outil de développement.
* Un clic sur ![inspecteur]({{site.baseurl}}/assets/magnifying.png) dans l'outil
de développement permet d'aller inspecter une zone d'intérêt dans la page (par
survol avec la souris).
* Quand on passe la souris au-dessus d'un élément dans l'outil de développement,
  il le colore dans la page.

<div class="exercise">

Familiarisez-vous avec ces trois techniques en inspectant la page du TD.  
Par exemple faites un clic droit sur l'élément "il y a trois façons..." puis
"inspecter l'élément".  L'outil de développement doit vous présenter le code
HTML et vous positionner directement sur `<p>Il y a ...`.

</div>

<!-- Hé ! ceci est un commentaire HTML, vous n'êtes pas censé le voir, à moins
que vous ne sachiez utiliser les outils de développeurs ? -->

## Les balises communes du HTML

### Les commentaires en HTML

Il est possible de rajouter des commentaires dans le HTML. Ces commentaires ne
sont pas interprétés par le navigateur, et ne sont donc pas affichés (mais ils
restent présents dans le code source).  Il s'agit donc d'informations laissées par
des développeurs pour des développeurs. On les place entre les balises `<!--`
et `-->` :


```html
<!--Cela est un commentaire dans un fichier HTML  -->
```

Il y a justement des commentaires dans le fichier `index.html`, comme autant de
consignes afin de les remplacer par du HTML.  Nous expliciterons ces dernières
dans les sections suivantes.

### Titres

Nous allons commencer par rajouter de la structure à notre page.  Pour ce faire
nous allons utiliser les balises à contenu `<h1>` à `<h6>` pour identifier les
différentes sections :

* `<h1>` est utilisé pour les gros titres du document
* `<h2>` est utilisé pour les sections du document
* `<h3>` est utilisé pour les sous-sections du document et ainsi de suite.

Par exemple, le titre ci-dessus est obtenu avec le code suivant :

```html
<h3>Titres</h3>
```

<div class="exercise">

1. Vérifier que le titre **Titres** juste au-dessus est bien un `<h3>` à l'aide
   des outils de développement en faisant un clic droit dessus.
1. Ajoutez la balise `<h2>` aux éléments de `index.html` marqués par les
   commentaires : `<!-- section -->`.
2. Ajoutez la balise `<h3>` aux éléments de `index.html` marqués par les
   commentaires : `<!-- sous section -->`.
3. **Retestez** la conformité de votre document.

</div>

### Éléments de regroupement

#### Paragraphes

<div class="exercise">

Utilisez maintenant les balises `<p>` et `</p>` autour des paragraphes du
document. Les paragraphes vous sont signifiés par `<!--début paragraphe -->` et
`<!--fin paragraphe -->`.

**Note :** Si vous faites un clic droit suivit de "inspecter l'élément" sur
ce paragraphe, vous verrez justement que ce texte est dans un paragraphe.

</div>

#### Listes

En HTML nous pouvons faire des listes ordonnées (numérotées) ou non ordonnées :

```html
<ul> <!-- ul pour unordered list -->
  <li>premier item non ordonné</li> <!-- li pour list item -->
  <li>deuxième item</li>
</ul>
<ol> <!-- ol pour ordered list -->
  <li>premier item ordonné</li>
  <li>deuxième item</li>
</ol>
```

Ce qui donne une fois interprété par le moteur de rendu du navigateur :

<div class="codeexample" style="margin:1em 0px;">
<ul>
  <li>premier item non ordonné</li>
  <li>deuxième item</li>
</ul>
<ol>
  <li>premier item ordonné</li>
  <li>deuxième item</li>
</ol>
</div>

<div class="exercise">
1. Utilisez les balises `<ul>` et `<li>` pour structurer la liste à puces
`<!--liste -->` dans `index.html`.  
(Ne vous souciez pas encore des commentaires `<!-- lien externe -->`)
2. Utiliser les balises `<ol>` et `<li>` pour structurer la liste numérotée
   `<!--liste numérotée -->` dans `index.html`.
3. **Retestez** la conformité de votre document. (En fait vous devriez le tester
régulièrement de vous même, mais on vous tient par la main pour ce premier TD)
</div>

### Image : un exemple d'élément embarqué

Pour insérer une image, on peut utiliser la balise

```html
<img src="adresse_image" alt="texte alternatif mais obligatoire">
```

Cette balise n'a pas de balise fermante car elle ne peut avoir de contenu
(cf. [le début du TD](#les-balises-html)).  On remarque qu'elle possède deux
champs `src` et `alt` que l'on appelle les **attributs** de la balise. Les
attributs se trouvent **toujours** dans la balise ouvrante.

<div class="exercise">
Précédemment, on avait vu une autre balise avec un attribut : quelle était cette balise ?
<!-- `<meta>` avec l'attribut `charset`. -->
</div>

L'attribut `src` doit contenir l'adresse de l'image. L'attribut `alt` permet
d'ajouter un texte alternatif pour les navigateurs ne pouvant les afficher
(navigateur textuel <a href="http://lynx.browser.org/">Lynx</a>) ou pour les
personnes ne pouvant pas bien les distinguer (aveugles ou déficits visuels
légers). **Attention**, l'attribut `alt` est obligatoire.


<div class="exercise">
1. Enregistrez l'image
[chuck-jeune.jpg]({{site.baseurl}}/assets/chuck-jeune.jpg) dans un
répertoire `images` par rapport à votre fichier `index.html`.

2. Remplacez le commentaire `<!--l'image de Chuck Young doit être positionnée
ici -->` par la balise `<img>` qui affichera l'image précédente.

   <!-- ```html -->
   <!-- <img src="./images/chuck-jeune.jpg" alt="Une photo de Chuck Jeune, la légende est en marche."> -->
   <!-- ``` -->
 
   **Note :** Vous pouvez utiliser l'adresse `./images/chuck-jeune.jpg`. C'est
     une adresse relative : le point signifie "le dossier de la page Web
     courante". Donc on va aller chercher l'image dans le dossier `images` du
     répertoire contenant la page Web `index.html`.

3. Faites de même avec l'image [beware.jpg]({{site.baseurl}}/assets/beware.jpg)
   à positionner en lieu et place du commentaire `<!--l'image de Chuck Beware
   ici -->`.

4. Devinez quoi ? Il faut **retester** la conformité de votre document.
</div>

### Éléments sémantiques

#### Liens externes

L'un des éléments les plus emblématiques du HTML est sans doute la balise
`<a>`. Elle permet de faire des liens hypertextes (le HT dans HTML).

Un lien est composé principalement d'une URL cible et d'un libellé (le texte
cliquable souvent souligné en bleu) :

```html
<a href="http://urlcible">le libellé</a>
```

On peut renseigner l'URL complète de la cible (URL en chemin absolu), par
exemple :

```html
<a href="http://lynx.browser.org/">Lynx</a>
```
   
ou donner une adresse relative à la page courante (URL en chemin relatif), par exemple :
   
```html
<a href="./images/chuck-jeune.png">Image</a>
```

<div class="exercise">

1. Remplacez les commentaires `<!-- lien externe ...` par des balises `<a>` avec la
   bonne adresse.
2. **Testez** la conformité ...
</div>

#### Liens internes

On peut rajouter à ces *liens externes* une partie *lien interne* basée sur les
ancres `#monancre`. Toutes les balises peuvent prendre un attribut `id` comme
dans l'exemple suivant. **Attention**, la valeur de cet attribut doit être
**unique** dans le document.

```html
<h2 id="un_identifiant">
```

On peut alors faire un lien vers cette balise en rajoutant `#un_identifiant` à
la fin de l'URL. Par exemple, voici un lien vers la balise d'identifiant
`un_identifiant` interne à la page Web courante `index.html` :

```html
<a href="index.html#un_identifiant">Exemple de lien interne</a>
```

On peut raccourcir l'URL comme suit. Si on n'indique pas le document, c'est que
l'on pointe vers le document courant par défaut.

```html
<a href="#un_identifiant">Exemple de lien interne</a>
```


<div class="exercise">

1. Remplacez le commentaire `<!-- lien interne ...-->` de `index.html` par une
   balise `<a>` qui pointera sur l'une des premières balises. Vous aurez donc
   besoin de rajouter un identifiant à cette balise cible.
2. Testez vos liens en cliquant dessus. Ils doivent vous emmener sur la balise
   dont l'identifiant correspond.
3. **Testez** la conformité ...

</div>

#### Emphase

La balise `<em>` permet de mettre en évidence des passages importants dans un
texte. 

<div class="exercise">

Justement, il faut mettre en exergue le fait que Chuck Norris est très fort dans
différents arts martiaux.  Pour cela il faut mettre en emphase la phrase qui
suit le commentaire : `<!-- mettre en emphase cette phrase -->` dans le fichier
`index.html`.

</div>

**Note :** Il existe un autre type d'emphase qui s'obtient avec la balise `<strong>`.

#### Citation

Voici un magnifique exemple de citation :

<blockquote> 
Un biscuit ça n'a pas de 'spirit', c'est juste un biscuit. 
Mais avant c'était du lait, des oeufs. Et dans les oeufs, il 
y a la vie potentielle.  
<cite>Jean-Claude Van Damme</cite>
</blockquote>

Les citations permettent d'identifier un court texte sur lequel on veut attirer l'attention.
Cela est utilisé notamment pour montrer qu'on a du 'spirit'.

<div class="exercise">

1. Allez voir le code source de notre citation à l'aide des outils de
développement. Quels sont les deux **nouvelles** balises utilisées ?
<!-- `<blockquote>` et `<cite>` -->

   La première balise (qui commence par un `b`) entoure la citation complète
   tandis que la deuxième (qui commence par un `c`) contient uniquement la
   référence (l'auteur, le livre, ...). 

1. Utilisez ces deux balises pour mettre en avant la citation en tout début de
   document (rechercher `<!-- utiliser blockquote ici -->`).

2. Avez-vous vérifié tout au long du TD que votre page HTML reste valide ?

<!-- 1. N'oubliez pas d'enregistrer régulièrement votre travail sous Git avec `git -->
<!--    status/add/commit/push`. -->


</div>

## Fini !

Nous en avons fini en ce qui concerne le contenu et la structure de notre site.
Nous savons ajouter de la structure à une page HTML avec des balises spécifiques.

Dans la [partie 2 de ce TD](tutorial1_2.html), nous verrons comment améliorer l'aspect
du site.

<!-- Pour afficher les extensions de fichier Dans l'explorateur : alt pour
afficher les menus, outils, options des dossiers, affichage, décocher cacher les
extentions dont le type est connu -->
