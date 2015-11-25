---
title: TD5
subtitle: OverConstraint, Fluid Layout, Responsive design, Mobile first...
layout: tutorial
---

NE SUPPRIME RIEN : COMMENTE SI TU NE VEUX PAS AFFICHER UN BOUT DU TD DE L'AN
DERNIER. MERCI !

## Introduction

Vous allez aujourd'hui travailler avec le navigateur Chrome afin de recourir à
l'une de ses fonctionnalités: émuler le comportement d'un périphérique mobile
naviguant sur le web.

Commencez par ouvrir les pages suivantes et observez les:

* votre site web
* [Le Monde](http://www.lemonde.fr)
* [Facebook](https://www.facebook.com)
* [BAE Systems](http://www.baesystems.com)

Ouvrez maintenant la console de votre navigateur (F12) et cliquez sur la 2e
icône à gauche, celle qui représente un téléphone mobile (“toggle device
mode”). Une barre d'options apparaît en haut de votre navigateur.

Dans le menu de sélection, choisissez “Samsung Galaxy S, S II, W”. Au cours du
TP, vous utiliserez cette option pour émuler un téléphone mobile et “Samsung
Galaxy Tab” pour émuler une tablette.

<div class="exercise">

Que constatez-vous ?

</div>

En restant dans ce mode, rechargez maintenant chaque page (F5).


<div class="exercise">

Que constatez-vous ? Que pouvez vous conclure sur les différentes manières d'adapter un site web à un téléphone mobile ?

</div>


## Historique

Aux origines du web, les ordinateurs étaient lents et disposaient d'écrans de
petite taille. Le code se limitait par ailleurs au seul HTML avec des pages web
statiques.

Puis la taille des écrans a augmenté. Comme il n'était pas possible de
déterminer la taille de l'écran du visiteur d'une page web, c'est à cette époque
qu'est apparu la mise en page consistant à fixer une taille maximale à la page
(800x600 d'abord puis 1024x780) avec des marges latérales de taille variable
selon l'espace supplémentaire disponible sur chaque écran. Cette mise à page
qui, permet de conserver un affichage similaire quel que soit la taille de
l'écran du visiteur, est très longtemps restée la mise en page standard de la
plupart des sites webs. Elle commence seulement à disparaître progressivement au
profit d'une mise en page utilisant tout l'espace disponible.

Puis s'est fait jour le besoin de réagir dynamiquement aux entrées de
l'utilisateur. C'est alors que le langage “Javascript” (ou Jscript chez
Microsoft) a vu le jour. Il permet d'effectuer des calculs dans le navigateur et
de modifier dynamiquement la présentation d'une page web, de communiquer des
données avec le serveur en arrière plan...

Le marché du navigateur, originellement dominé par Microsoft et Netscape, s'est
diversifié progressivement pour laisser place à un nombre croissant de
navigateurs. Si aujourd'hui tous les éditeurs font un effort croissant pour
homogénéiser leur support des standards, il n'en reste pas moins qu'il existe de
nombreuses différences entre navigateurs quant à ce que chacun supporte des
standard HTML, CSS et Javascript.

Le web sur téléphone mobile a vu le jour dès 1999 mais est resté un épiphénomène
jusqu'en 2007 avec le boom des “smartphones”. Aujourd'hui, certaines études
estiment qu'entre 17 et 25% du trafic mondial sur les pages web a pour origine
les périphériques mobiles, smartphones et tablettes.

Il existe donc désormais deux marchés distincts pour les pages webs: le marché
des utilisateurs sur ordinateur de bureau/portable, et le marché des
utilisateurs sur périphérique mobile, sans oublier que les deux ensembles se
recoupent pour partie.  Ces deux marchés, quoique que complémentaires dans leur
utilisation, s'opposent sur le plan technique. Ainsi le marché de bureau est
caractérisé par des écrans de grande taille, des processeurs puissants et, en
général (en France particulièrement), des débits élevés et illimités. A
contrario et bien que cela change progressivement, les périphériques mobiles ont
une puissance de calcul plus faible, des écrans de petite taille, supportent
parfois mal le Javascript (particulièrement les 1e modèles) et chargent les
données par-dessus une connexion souvent plus lente et/ou limitée quant au
volume de données que l'utilisateur peut charger.  Il y a donc nécessité
d'adapter le comportement des pages web.

## Définition

Sont collectivement regroupées sous le nom de “responsive design” l'ensemble des
techniques qui permettent d'adapter son apparence et, éventuellement, son
contenu, au media utilisé pour la consulter. Bien que cela ne fasse pas partie
de la définition officielle et que cette méthode soit très antérieure à
l'apparition du terme de responsive design, on peut y ajouter également
l'ensemble des méthodes utilisées pour s'assurer qu'une page web reste
compatible avec tous les navigateurs.

Leur mise en place doit prendre en compte:

* les paramètres d'affichage du périphérique (taille écran, résolution, couleurs)
* les paramètres du navigateur (support Javascript, support Flash, éléments de HTML5/CSS supportés)

## Approches possibles

### Dégradation progressive

Cette approche est historiquement la 1e à avoir été développée. Son résultat
technique est souvent moins élégant et les pages web plus lentes à charger, mais
en contrepartie elle permet d'adapter des sites web existants aux périphériques
mobiles tout en retenant l'apparence d'origine du site web, apparence à laquelle
les utilisateurs sont habitués de longue date.

Dans cette approche, la disposition des éléments de la page est modifiée selon
les fonctionnalités disponibles dans le navigateur et la taille du
périphérique. Le site web est d'abord créé avec le maximum de fonctionnalité
puis, selon les disponibilités, certaines fonctions sont progressivement
retirées. Souvent, l'apparence d'origine du site web dans son meilleur état est
conservée en recourant à des images pour remplacer le contenu qui ne peut être
géré par les périphériques mobiles.

### Augmentation progressive

C'est l'approche inverse, particulièrement recommandée pour les sites à
créer. Elle ne conserve pas forcément une apparence exactement identique entre
version mobile et version de bureau, mais permet d'obtenir un résultat optimal
et léger (rappelons que la plupart des utilisateurs s'en vont s'ils doivent
attendre plus de 4s le chargement de votre site).  Selon cette approche, la page
web est d'abord produite avec un minimum de fonctionnalités et de manière aussi
proche que possible du résultat maximal attendu. Puis cette page est
décorée/augmentée à mesure que l'on détecte que le navigateur supporte les
fonctionnalités requises.

Ainsi par ex, dans la version de base, on utilisera les attributs “pattern,
required et placeholder” pour aider à remplir un formulaire tandis que dans la
version augmentée, du Javascript sera utilisé pour obtenir un rendu personnalisé
et plus convivial.

### Sites distincts

Cette dernière approche, apparue plus récemment, consiste à créer deux (ou plus)
sites web complètement distincts. Chaque site web cible un type de
périphérique. Cette approche offre les avantages suivants:

* une expérience de navigation parfaitement adaptée au périphérique utilisé
* pas besoin de faire tourner des scripts en arrière plan pour détecter, adapter... Plus rapide donc
* offre des avantages similaires à une application mobile mais reste
  indépendante de l'OS aussi n'y a-t-il qu'un seul code source à maintenir

A contrario, l'un des inconvénients de cette méthode est la difficulté qu'il y a
à partager l'expérience entre périphérique mobile et ordinateur de bureau. Le
traitement des favoris entre autre requiert une attention toute particulière
afin qu'un favori enregistré sur la version mobile et utilisé depuis un
ordinateur de bureau amène sur les deux versions de la même page.

Cette méthode est mise en place par grâce à des scripts de redirection qui
détectent la version du navigateur et redirigent l'utilisateur vers l'URL du
site mobile/bureau. Ces scripts peuvent être mis en place au niveau du serveur
lui-même (Apache mod rewrite par ex.) ou au niveau du script côté serveur qui
génère la page web.

<div class="exercise">

Pouvez-vous maintenant dire lesquelles de ces approches sont employées par les sites webs consultés en introduction ?

</div>


## Outils

Il existe toute une variété d'outils pour mettre en place le responsive
design. Toutefois, ces travaux pratiques se limitant au HTML et au CSS, nous
n'aborderons dans leur cadre qu'une seule de ces techniques, les “media
queries”.

### Javascript/Flash

Ces deux langages, utilisés pour effectuer des calculs dynamiquement dans le
navigateur, peuvent être mis à contribution pour adapter une page web au
périphérique dans le contexte du responsive design. Il existe aujourd'hui de
nombreuses librairies en Javascript qui permettent de mettre en oeuvre des sites
webs dont l'apparence varie.

En Javascript, les objets
[navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator), en
particulier le
[User agent](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorID/userAgent)
(chaîne de caractères identifiant le navigateur), et
[window.screen](https://developer.mozilla.org/en-US/docs/Web/API/Window/screen)
comportent de nombreuses propriétés qui permettent de renseigner vos scripts
quant aux fonctionnalités disponibles, la taille et l'orientation de l'écran,
etc.

Par ailleurs, afin de standardiser les sites webs et simplifier les tâches
automatisables, de nombreuses librairies JS ont vu le jour. Ainsi,
[Modernizr](https://modernizr.com/) vous renseignera directement sur ce que le
browser ne supporte pas des standards HTML, CSS... et vous permettra de charger
des modules spécifiques pour remplacer ces
manques. [Categorizr.js](http://skookum.com/blog/categorizr-js-device-detection-for-your-responsive-websites)
effectue tout le travail de détection du périphérique et vous informera de sa
nature (PC, mobile, tablette). Pour finir, [Bootstrap](http://getbootstrap.com/)
offre tout un environnement de travail destiné à adapter le plus simplement
possible l'apparence de votre page au périphérique.

Bien entendu, le recours au Javascript et à ces librairies associées requiert
que le navigateur le supporte.  Ce support est désormais généralisé sur les
smartphone modernes.

### Redirection vers site spécifique aux mobiles

Cette redirection peut-être effectuée grâce à
[Apache mod_rewrite](http://httpd.apache.org/docs/current/mod/mod_rewrite.html)
sur les serveurs apache. Il faut alors utiliser une redirection conditionnelle
se basant sur la variable “HTTP_USER_AGENT” pour détecter les périphériques
mobiles sur la base de l'identité de leur navigateur
([Ex des User agent spécifiques aux versions mobiles de Chrome](https://developer.chrome.com/multidevice/user-agent)).

### Design fluide

Au niveau de votre CSS, vous avez fixé la taille horizontale (width) d'un
certain nombre d'éléments de votre page web. Comme vous l'avez vu au cours du
TP5, la taille d'un élément peut être fixée avec plusieurs unités différentes,
entre autres en pixels (px) et en % de la taille de l'élément parent (%).

Les tailles en pixels sont statiques et les éléments ainsi configurés auront
toujours la même dimension, quitte à déborder de l'écran. A contrario, les
éléments fixés en % s'adaptent automatiquement à la taille de leur élément
parent. Par ailleurs, l'élément racine de votre page web est l'élément “body”,
dont la taille maximale est 100% de l'espace disponible dans la fenêtre du
navigateur, soit en pratique la surface d'affichage réelle.

On dit alors d'une page web qu'elle utilise un “design fluide” si les dimensions
de la totalité de ses éléments, fixées dans le CSS, sont renseignées en %. Cela
permet alors à la page d'adapter automatiquement ses dimensions à l'espace
disponible, puisque l'élément “body” occupera une proportion donnée de l'espace
d'affichage, chaque élément qu'il contient à son tour occupant une proportion
donnée du “body”, et ainsi de suite.

<div class="exercise">

Lequel des sites étudié en introduction utilise un design fluide ?

</div>

Pour tester votre page web en design fluide, vous allez maintenant basculer sous
Firefox qui fonctionne beaucoup mieux de ce point de vue. Ouvrez la console du
navigateur (F12 toujours) et cliquez sur la 5e icône depuis la droite
(responsive design mode). Une barre d'options s'affiche en haut vous permettant
de régler dynamiquement les dimensions de votre surface d'affichage.

<div class="exercise">

Vous allez maintenant convertir votre page d'accueil du TP5 en design fluide en
transformant toutes les dimensions des éléments (width, height, margin, padding)
en %. Pour la largeur du “body”, vous utiliserez 66%.

Que constatez-vous ?

</div>

Les éléments peuvent se redimensionner mais pas les polices de caractère, ce qui
produit un résultat désastreux. Pour les polices de caractère, il existe une
unité spécifique, le “vw” (pour view-port width). Une unité de 1vw correspond
plus ou moins à ceci: 1 caractère aura comme largeur maximale 1% de la largeur
maximale de la surface d'affichage. Sa hauteur sera calculée automatiquement en
fonction de sa largeur. Une règle CSS définissant la taille des polices et
écrite en “vw” permet donc aux polices de se redimensionner automatiquement et
donc d'intégrer le principe du design fluide.

<div class="exercise">

Ajoutez à l'élément “body” la règle CSS “font-size: 1.5vw”. Pensez également à
convertir en vw les autres règles de taille de police si vous avez défini des
règles CSS spécifiques à certains éléments.

Que constatez-vous ?

</div>

La règle de taille de police fixée à l'élément “body” est héritée par tous les
autres éléments de la page, exception faite des éléments disposant de leur propre
règle.

<div class="exercise">

Si votre page présente encore un aspect incorrect (éléments trop grands), pensez
à fixer toutes les images à 100% de leur container (height et width) et
n'hésitez pas à rajouter si besoin des règles pour spécifier la largeur de
certains éléments.

</div>

## Media queries

La taille des éléments et des polices s'adapte désormais en proportion de la
taille de la surface d'affichage. C'est un gros progrès mais ce n'est toutefois
pas suffisant à un design complètement réactif. On pourrait en effet souhaiter
modifier/déplacer des éléments autrement qu'en réglant leurs dimensions.

Prenons l'exemple de la largeur de la page. Sur un grand écran, on souhaite
avoir une marge importante de chaque côté afin de conserver ce format de
“page”. C'est pourquoi le “body” est fixé à 66%. Cependant, sur un petit écran,
on voudrait supprimer ces marges qui prennent de la place inutilement.

C'est là qu'entrent en jeu les
[“media queries”](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries). Les
media queries sont un jeu d'options ajoutées à la norme CSS 3 et qui permettent
de définir des règles CSS qui ne s'appliqueront que sous certaines conditions
spécifiques.

Il existe deux manières de faire appel à une media query:

* charger un fichier CSS spécifique en entier, uniquement dans certaines
  conditions. Il faut ajouter à l'élément “head” de la page web une déclaration
  de fichier CSS standard, à laquelle on rajoute l'attribut “media” et une
  condition spécifique. Cette option n'est pas disponible en XHTML. N'oubliez
  pas que le dernier CSS chargé prend le pas sur les précédents. Pensez donc à
  toujours déclarer vos media-queries en dernier, sinon elles seront
  systématiquement écrasées par votre CSS “standard”

  ~~~
  <link rel="stylesheet" media="[condition]" href="[mon css spécial].css"/>
  ~~~
  {:.html}

* au sein même d'un fichier CSS, définir certains règles qui ne s'appliqueront
  que sous certaines conditions

  ~~~
  @media ([ma condition]) {
  	[mon sélecteur css] {
      		[mes propriétés]: [mes valeurs];
    	}
  }
  ~~~
  {:.css}

Une media query fonctionne de la manière suivante: la condition est évaluée et
retourne une valeur “vrai” ou “faux”. Si la valeur est vraie, le fichier CSS/ la
règle CSS (selon la méthode employée) est appliquée.

Chaque condition est formée à partir d'une ou plusieurs conditions de base. Les
conditions de base peuvent être combinées ensemble pour former des conditions
complexes en utilisant les opérateurs logiques:

* “and” (ET): les deux conditions de base doivent être vraies pour que la
  condition soit vraie
* “,” (OU): au moins l'un des conditions de base doit être vraie pour que la
  condition soit vraie
* “not” (NON): la condition de base qui suit le not doit être fausse pour que la
  condition soit vraie

Exemple : la règle media="(min-width: 21cm), (orientation: landscape) and
(min-height: 21cm)" ne s'appliquera que si l'écran fait au moins 21cm de large
ou s'il fait au moins 21cm de haut et est en orientation paysage.  Note: vous ne
pouvez pas imbriquer plusieurs media queries différentes les unes dans les
autres.

Parmi
[l'ensemble des conditions possibles](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries#Media_features),
nous allons dans le cadre de ce TP nous intéresser particulièrement aux
suivantes:

* « width » et « heigh »: largeur et hauteur de l'écran (ou de la fenêtre du
  navigateur). Définies dans l'une des unités supportées par le CSS (px, em, cm,
  in...). Peuvent être préfixées par “min-” ou “max-” pour renseigner une
  dimension minimale/maximale à remplir pour que la condition soit vraie. Si ni
  “min” ni “max” n'est utilisé, alors la condition se réfère à une taille
  exacte.

* « color » : le nombre de bits par couleur supportés par l'écran (0 = noir et
  blanc, 8 = 256 couleurs, 16 = 65000 couleurs)

* « monochrome »: 0 si l'écran est couleur, sinon une valeur en nombre de bits
  par couleur pour les écrans supportant des niveaux de gris. Il est donc
  possible en combinant les conditions de base “color” et “monochrome” de cibler
  spécifiquement les devices “noir et blanc”, “niveau de gris” ou “couleur” pour
  adapter par exemple les couleurs de police de caractère

* « orientation »: prend les valeurs “landscape” (écran horizontal) ou
  “portrait” (écran vertical)

* « type de média »: prend l'une de ces valeurs. Vous pouvez créer avec un jeu
  de règles CSS qui ne s'appliquera que pour une impression ou un système de
  synthèse vocale pour les aveugles.

<div class="exercise">

Ajoutez à votre CSS une media query utilisant la condition (max-width: 1023px)
puis ajoutez à cette media query les règles CSS nécessaires à ce que les marges
latérales de votre page disparaissent lorsque vous réduisez trop les dimensions
de la page. Vous pouvez également augmenter la taille de votre texte par la même
occasion lorsqu'il est affiché sur petit écran de manière à ce que vos titres
restent lisibles même réduits.

</div>

<div class="exercise">

Rechargez votre page et vérifiez bien qu'au-delà d'une certaine taille, les
marges de votre apparaissent/disparaissent.

</div>

Notez qu'une petite marge peut persister autour de la page. Ceci est lié au
navigateur qui impose par défaut cette marge. Pour vous débarrasser des règles
par défaut du navigateur, vous pouvez ajouter en tête de votre CSS la règle
suivante :

~~~
* {
    margin: 0;
    padding: 0;
}
~~~
{:.css}

Le menu de navigation à droite de la page est également accessoire. En taille
réduite, on souhaite le garder mais sans qu'il encombre l'espace d'affichage
horizontal

<div class="exercise">

Où allez-vous le placer ? Disposez-vous avec le seul langage HTML d'un moyen
pour déplacer un élément d'un endroit de la page à un autre ?

</div>

Pour récupérer de l'espace d'affichage, vous allez en petit format, et
uniquement quand le téléphone est en mode “portrait”, déplacer le menu de droite
entre le corps de texte de la page et le pied-de-page, sous la forme cette
fois-ci d'un menu horizontal. Sans Javascript, il n'est pas possible de déplacer
les éléments dans la page. La méthode consiste donc à avoir dans la page
simultanément le menu de droite et le menu horizontal sous le texte, et à
n'afficher que l'un des deux en fonction du contexte.

<div class="exercise">

A l'aide des langages HTML et CSS, ajoutez un menu de navigation horizontal
entre le texte et le pied-de-page. Ce menu doit reprendre les mêmes éléments que
le menu de navigation à droite du texte.

</div>

Pour réaliser ce menu, vous pouvez reprendre les règles de mise en page étudiées
au cours du TP5 ou faire appel au mode
[“flex box"](css-tricks.com/snippets/css/a-guide-to-flexbox/) qui permet
d'organiser facilement plusieurs éléments dans un même container, sur une ou
plusieurs lignes.

<div class="exercise">

Ajoutez maintenant à votre CSS la media query “(max-width: 1023px) and
(orientation: portrait)”. Introduisez dans cette media query les règles CSS
nécessaires à ce le menu de droite n'apparaisse qu'en mode “grand écran” ou
“petit écran horizontal” et que le menu horizontal n'apparaisse qu'en mode
“petit écran vertical”.

</div>

<div class="exercise">

Que constatez-vous ? Pensez à modifier également les autres éléments pour qu'ils
prennent alors toute la place disponible.

</div>

## Conclusion :

Avec ces outils en main, vous pouvez désormais produire des pages web dont
apparence varie selon le périphérique utilisé pour les consulter. Ceci en
recourant uniquement à du HTML et du CSS, autrement dit des outils disponibles
dans 100% des navigateurs utilisés aujourd'hui.

Continuez d'adapter votre page de garde, ainsi que les autres pages de votre
projet, afin qu'elles s'affichent au mieux sur téléphone portable/tablette. Vous
pouvez par exemple disposer le menu de navigation du haut sous la forme
d'éléments empilés verticalement quand affiché sur périphérique mobile.

Choisissez bien les éléments que vous conservez, supprimez ou modifiez afin de:

* conserver les fonctionnalités importantes
* épurer l'affichage et laisser un maximum de place au contenu important (le “main”)
* conserver votre style visuel
