---
title: TP n°5 &colon; HTML et CSS avancé
subtitle: Un langage de mise en page
layout: tutorial
---

Comme vous avez pu le constater au cours du TP précédent, certains éléments
peuvent cohabiter sur une même ligne et d'autres non. La spécification HTML5
propose différentes manières de classer les balises/éléments selon leurs
caractéristiques
([Liste des balises par catégorie](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Content_categories)). Nous
allons ici nous intéresser à deux types spécifiques :

* les balises de structure : elles permettent de délimiter l'articulation
  logique de la page web en la découpant en différentes sections. Par défaut,
  ces balises découpent la page web en sections horizontales qu'elles occupent
  en entier (du bord gauche au bord droit de la section). Deux balises de flux
  ne peuvent pas partager une même section horizontale aussi les espaces
  qu'elles délimitent dans la page s'enchaînent-ils verticalement. Elles peuvent
  contenir d'autres balises de structure ou des balises de contenu.

* les balises de contenu : elles permettent de délimiter le texte de la page et
  d'en altérer le formatage. Par défaut, ces balises n'occupent que l'espace
  horizontal minimum nécessaire à afficher le texte qu'elles contiennent, et
  plusieurs balises de contenu peuvent partager une même ligne
  horizontale. Lorsque le contenu d'une de ces balises est trop grand pour tenir
  sur une ligne, il se poursuit automatiquement à la ligne suivante. Les balises
  de contenu peuvent contenir d'autres balises de contenu.

Quelques exemples :

* balises de structure :

   * `<div>` : cette balise est « neutre », à savoir qu'elle permet de distinguer
une section qui ne revêt aucune signification particulière. A utiliser quand
aucune des autres balises de structure ne convient. Typiquement utilisé pour
donner à la page sa structure visuelle à l'aide de règles CSS header : section
contenant l'en-tête affiché de la page
   * `<nav>` : section contenant une série de liens hypertextes pour la navigation
     sur le site
   * `<main>` : section principale de la page, celle qui contient le contenu
     spécifique à cette page. Cette balise ne peut-être présente dans une autre
     balise présentée ici à l'exception de « div ». Elle n'est pas supportée par
     Internet Explorer <= 10 mais le support peut en être ajouté grâce à
     Javascript et en utilisant la règle css « main {display : block} ».
   * `<article>` : section contenant un document « auto-suffisant », i.e. qui peut
     être séparé du reste de la page et gardera cependant tout son sens. Une
     page peut contenir plusieurs articles, dans le cas d'un blog par exemple,
     de commentaires, d'une page listant les publications récentes ...
   * `<aside>` : section contenant du matériel périphérique au contenu
     principal. Cela peut-être par ex. une série de liens spécifique au document
     principal, un bandeau de publicités …
   * `<footer>` : section contenant le pied de page.
   * `<section>` : une section non spécifique, ou une sous-section d'un article,
     d'un menu... Doit typiquement commencer par un titre hX.
   * `<figure>` : une illustration (au sens large) « auto-suffisante » illustrant le
     document principal ou un article, et qui doit pouvoir être placée librement
     dans la page sans en altérer le déroulement (par ex. dans le texte, dans un
     appendice...)
   * `<h1>`- `<h6>` : titres de section
   * `<p>` : paragraphes du texte
   * `<address>` : coordonnées de contact de l'auteur. Il ne peut y avoir qu'un bloc
     « address » par article et un pour le restant de la page

* balises de contenu :

   * `<span>` : cette balise est neutre, sans signification particulièrement. Permet
     entre autres de créer des règles de formatage spécifiques du contenu
     textuel, par exemple une lettre plus grande pour la 1e lettre d'un
     paragraphe.
   * `<quote>` : une citation
   * `<img>` : une image
   * `<sup>` : un exposant
   * `<time>` : mise en valeur d'une date

## Mise en page

Comme expliqué ci-dessus, les balises dites « de structure » permettent de
produire un premier découpage logique de la page en différentes sections
horizontales. Toutefois, ce n'est pas suffisant par exemple pour produire des
pages contenant plusieurs colonnes puisque chaque section occupe exclusivement
tout l'espace horizontal qu'elle crée (autrement dit on ne peut avoir de base
qu'une page à une colonne).

Nous allons maintenant voir au travers d'un exemple complexe abordé pas à pas
comment utiliser les règles CSS pour obtenir l'apparence visuelle qui vous
convient.

### Contenu de base

Créez le contenu de base de la page tel que décrit dans le document « Maquette
site webA1 - Commentaires.pdf ». Vous ajouterez successivement les différents
éléments formant le contenu de la page en commençant en haut à gauche et en
procédant ligne par ligne (éléments approximativement à la même position
verticale dans la page). Vous introduirez les éléments de la colonne de droite
(liens) après ceux du contenu principal et avant ceux du pied de page.

* Pour créer des images qui peuvent être cliquées pour naviguer vers un autre
  site, procédez comme suit : `<a href="lien vers ma page"><img src="lien vers
  mon image" alt="mon texte alternatif"></a>`

* Pour créer le menu de navigation en haut de la page, utilisez une liste non
  ordonnée (« ul ») dont chaque élément sera un lien.

* Les titres utiliseront « h1 » (textes en gras ou bleu) et « h2 » (texte en
  vert).

* Les autres textes sont délimités par des balides « p ».

### Structuration logique du contenu

Vous allez d'abord sectionner logiquement le contenu que vous venez de créer à
l'aide des balises de structure introduites ci-dessus.

Encapsulez :

* les deux images et les deux titre d'en-tête dans une balise « header ». Ils
  forment l'en-tête de site.
* le menu de navigation dans une balise « nav »
* la colonne de gauche dans une balise « main » et celle de droit dans une
  balise « aside »
* le pied de page dans une balise « footer »

finalement, à l'intérieur de la balise « main », distinguez deux articles
différents au moyen de la balise « article » (chaque article commence par un
titre et se finit par une ou plusieurs images).

Que constatez-vous ?

A ce point, le travail de division de la page n'a pas encore de résultat visuel
marquant. C'est avant tout un travail de structuration logique qui permet au
navigateur, à un moteur de recherche de mieux comprendre votre page web.

### Style global de la page

Associez votre page web à un fichier CSS comme vu lors du 1e TP. Dans ce
fichier, créez la règle suivante :

~~~
body {
    width: 1024px;
    margin: auto;
    margin-top: 10px;
    margin-bottom: 10px;
    padding: 35px;
    border-style: solid;
    border-width: 1px;
    border-color: #000000;
    background-color: white;
}
~~~
{:.css}

Que constatez-vous ?

### Changer le comportement d'une balise

Comme énoncé plus haut, les balises de structure ne partagent pas leur espace
tandis que celles de contenu peuvent occuper une même ligne que d'autres. Ce
comportement par défaut peut être changer à l'aide de la règle CSS « display »
([Spécifications règle "display"](https://developer.mozilla.org/en-US/docs/Web/CSS/display)). Display
peut prendre une série de valeurs :

* inline : la balise se comporte comme une balise de contenu et partage son
  espace horizontal
* block : la balise se comporte comme une balise de structure et ne partage pas
  son espace horizontal
* inline-block : comme inline, mais la balise définira une boîte pour son
  contenu. C'est ce style que nous utiliserons le plus car il a des conséquences
  au niveau graphique : la boîte permet d'utiliser une couleur de fond pour tout
  l'espace défini par la balise
* table : le contenu de la balise se comportera visuellement comme une table (vu
  ci-dessus). Utile notamment pour la propriété CSS « vertical-align »
* table-cell : la balise se comporte comme la cellule d'un tableau (« td ») si
  elles est encapsulée dans une autre balise utilisant la propriété
  « display:table »

Ajoutez à votre CSS les deux règles suivantes :

~~~
main {
	display: inline-block;
	width : 300px ;
}
aside {
	display: inline-block;
	width : 300px ;
}
~~~
{:.css}

Rechargez la page. Que constatez-vous ? Pourquoi ?

### Créer une règle CSS qui affecte plusieurs balises

D'après le modèle que vous devez réaliser, un grand nombre de balises doivent
partager le même espace horizontal. Créer pour chacune d'elles une règle comme
celles ci-dessus serait long et rendrait confus le CSS. Vous allez créer une
règle s'appliquant à toutes.

Toutes les balises HTML supportent deux attributs particuliers qui peuvent être
utilisés pour créer des règles CSS :

* id : un identifiant unique propre à cette balise, qui ne sera présent sur
  aucune autre balise. Cet attribut permet par exemple de distinguer entre
  plusieurs « div » différentes si l'on veut créer une règle spécifique à l'une
  d'entre elles seulement. Une fois qu'une balise comporte un attribut
  « id="identifiant" », il est possible d'y faire référence dans le CSS avec la
  règle « #identifiant ».

* class : un identifiant unique qui peut être partagé par plusieurs balises
  différentes. Cet attribut permet d'appliquer une même règle CSS à plusieurs
  balises différentes à la fois. Une balise donnée peut avoir plusieurs classes
  différentes en écrivant dans l'attribut « class » les noms des différentes
  classes séparés par espace. Une fois qu'une ou plusieurs balises comportent un
  attribut « class="classe1 classeX" », il est possible de faire références à
  toutes celles comportant la classe1 dans le CSS avec la règle « .classe1 ».

Dans votre CSS, créez la règle :

~~~
.inline {
	display: inline-block;
}
~~~
{:.css}

Supprimez « display: inline-block; » des règles CSS « main » et « aside ».

Dans votre fichier HTML, ajoutez l'attribut « class="inline" » à toutes les
balises qui vont devoir partager une même ligne, à l'exception du contenu de la
balise « nav » (les images et titres de l'en-tête, les 3 images en ?, main,
aside).

Que constatez-vous ? Pourquoi ?

### Aligner les balises à gauche/droite

Suivant le modèle qui vous est fourni, la balise « aside » doit s'aligner sur le
côté droit de la page. La propriété CSS « float » permet d'indiquer si une
balise doit s'aligner sur le bord gauche ou droit de la balise qui la
contient. Notez que toute balise de type structure qui possède une règle CSS
contenant « float » devient automatiquement une balise « inline », même si cette
balise n'a pas de règle CSS « display: inline; » ou « display: inline-block; »

Créez les règles CSS suivantes :

~~~
.left {
	float: left;
}
.right {
	float: right;
}
~~~
{:.css}

Ajoutez à la page HTML la class « left » à toutes les balises qui doivent
s'aligner à gauche de la page, et la classe « right » à celles devant s'aligner
à droite.

Rechargez la page. Que constatez-vous ? Pourquoi ?

### Contrôler la mobilité des float

Une balise qui a la propriété CSS « float » va s'aligner le plus à gauche/droite
possible, sans prendre en considération la place de la balise dans le code
HTML. C'est pour cela qu'à l'étape précédente l'ordre de votre page web est
apparu complètement changé. Quand plusieurs balises portent « float left », la
1e dans le HTML sera la plus à gauche, suivie par les autres « float left » dans
leur ordre d'apparition dans le HTML, puis les autres balises non « floatées »,
puis celles « floatées » à droite dans l'ordre inverse.

Pour éviter cet effet indésirable, il faut encapsuler dans une balise « div »
les différentes balises qui doivent rester groupées ensemble.

Dans votre page HTML, ajoutez une balise « div » qui encapsule les balises
« main » et « aside ». Ajoutez une autre balise « div » qui encapsule les 3
images-lien en forme de « ? ».

Rechargez votre page. Que constatez-vous ?

### Corriger un bug de mise en page

A l'étape précédente, vous avez pu constater que, malgré l'encapsulation dans
des « div », le pied de page restait mal placé. Ceci est lié à un comportement
étrange et contre-intuitif des navigateurs web qui veut que, lorsqu'une balise
encapsule des balises « floatées », le navigateur la force à passer elle-même en
mode « display: inline ».

Il est impossible d'y remédier en tentant de forcer dans le CSS « display:
block » pour la balise qui encapsule. Il existe à date différentes manières de
remédier à ce « bug ». La plus élégante consiste à déclarer une règle CSS
spécifique pour la balise qui encapsule, cette règle forçant le navigateur à la
traiter à nouveau en mode « block ».

Créez la règle CSS suivante :

~~~
.inline-containe {
	overflow: auto;
}
~~~
{:.css}

Dans le HTML, ajoutez la class « inline-container » aux trois balises destinées
à contenir des balises « floatées » : les deux « div » ajoutées à l'étape
précédente et la balise « header ».

Rechargez votre page. Que constatez-vous ?

Dans le CSS, augmentez la taille (width) de votre règle « main ».
Rechargez votre page. Que constatez-vous ? Pourquoi ?

### Mise en forme display: tableau

Nous allons maintenant procéder à la mise en forme du menu de navigation au
moyen de la règle « display: table »

Créez les règles CSS suivantes :

~~~
nav ul {
    display: table;
    table-layout: fixed;
}
nav li {
    display: table-cell;
    background-color: grey;
}
~~~
{:.css}

Rechargez la page. Que constatez-vous ?

Que pouvez-vous dire du sélecteur CSS utilisé ? Quelle est la fonction de la
règle « table-layout: fixed; » ?

### Propriétés CSS des boîtes générées par les balises de structure

Comme vous l'avez vu précédemment, les balises de type structure définissent des
boîtes. Ces boîtes disposent toutes des propriétés suivantes en CSS :

* padding : marge entre le contenu est la bordure de la boîte. Le padding est de
  la couleur de la boîte, donc il a le même background que la boîte.
* border : bordure qui entoure le contenu.
* margin : marge à l’extérieur de la bordure, entre cette boîte et la
  suivante. La margin est de la même couleur que la balise mère qui encapsule
  celui pour lequel la marge est définie.
* width : la largeur du contenu
* height : la hauteur du contenu

<img alt="Box model" src="{{site.baseurl}}/assets/boxmodel.png" style="margin:0
auto;display: block;">

A noter que la taille réelle d'une boîte est égale à la taille du content
(width, height) additionnée de l'épaisseur du padding, du bord et de la marge.

Transformez vos règles précédentes pour qu'elles ressemblent à ceci :

~~~
nav ul {
    display: table;
    table-layout: fixed;
    width: 100%;
    margin: 0px;
    padding: 0px;
}
nav li {
    display: table-cell;
    vertical-align: middle;
    padding: 10px;
    color: grey;
}
~~~
{:.css}

Que constatez-vous ? Pourquoi ?

Essayez de fixer une marge de 10px à « nav li ». Que constatez-vous ? Pourquoi ?

### Interactivité


Vous allez maintenant ajouter un peu d'interactivité au menu de navigation. Vous
allez devoir changer la couleur de l'élément « nav li » correspondant à la page
actuellement affichée (dans ce cas-ci, l'Accueil) et faire en sorte que, lorsque
l'on passe la souris sur l'un des boutons du menu, celui-ci s'illumine. Pour
cela, vous allez utiliser les pseudoclasses CSS. Les pseudoclasses permettent de
créer des sélecteurs CSS qui affectent les éléments HTML uniquement lorsque des
conditions particulières sont remplies. Ce peut-être : souris survolant la
balise, balise est le 1e élément de son élément père...

Créez la règle CSS suivant :

~~~
nav li:hover {
    text-decoration: underline;
    color: green;
}
~~~
{:.css}

Que constatez-vous ? Une règle CSS peut-elle en remplacer une autre ? Dans
quelle condition ?

### Finalisation

Vous avez désormais tous les outils en main pour finaliser votre page web :

* ajustez les marges, paddings, hauteur et largeur des différents éléments (en
  particulier images)
* ajoutez des bordures là où demandé
* ajoutez les couleurs

Note : il est nettement préférable de définir un padding sur une balise mère que
de définir une marge équivalent sur chacune des ses balises filles. Le résultat
sera visuellement équivalent mais le nombre d'instructions passées sera
nettement réduit.

Note2 : vous rencontrerez un problème au moment de définir la couleur de
l'arrière plan de la page web. Vous devriez avoir les cartes en main pour
comprendre ce qui se passe mal avec le HTML/CSS actuel. Si tel n'est pas le cas,
interrogez votre encadrant.

Si vous êtes en avance : trouvez comment faire un menu qui reste visible lorsque
la page défile, des superpositions de div (popup inline), testez des mises en
page originales.

Quelques informations utiles :

* alignement de texte : text-align: justify \| center
* types de bordures : border-style: solid \| outset
* couleur de bordure : border-color: .....
* texte souligné ou non : text-decoration: none \| underline
* taille texte : font-size: ...
* texte gras : font-weight: bold
* couleur de texte : color: ...
* gradient de couleur : background: linear-gradient(couleur1, couleur2)

Couleurs :

* arrière plan : #AAAAAA
* page : white
* titres :
   * en-tête1 : #008BCE
   * en-tête1 : #BDCF00
* gradients (haut, bas, bord):
   * base : #EEEEEE, #888888, #DDDDDD
   * page active : #00acff, #006798, #00acff
   * survol souris, pied de page : #e9ff00, #747f00, #e9ff00

Pour centrer le contenu d'une balise :

* si le contenu occupe toute la largeur de la balise : text-align: center
* si le contenu est lui-même dans une balise moins large que la balise parent :
  margin : auto sur la balise du contenu, sans oublier après de fixer margin-top
  et margin-bottom aux valeurs souhaitées

Note : la propriété « text-align » est héritée. Vous pouvez ainsi la définir sur
« body » à la valeur la plus couramment utilisée et celle-ci sera appliquée à
tous les autres éléments de la page. Vous n'avez alors qu'à définir les valeurs
spécifiques à certains éléments de la page dans des règles spécifiques à ces
éléments
