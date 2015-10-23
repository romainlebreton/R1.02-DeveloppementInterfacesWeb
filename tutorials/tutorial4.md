---
title: TD4
subtitle: formulaires ?
layout: tutorial
---

Eric : exercices optionnels autour de solvedbyflex

Lionel : exercices optionnels sur les expressions régulières ?

# Formulaires

**Note de Romain :** Il y a deux documents joints
  [formulaire.pdf]({{site.baseurl}}/assets/formulaire.pdf) [TP6
  Maquette]({{site.baseurl}}/assets/TP_n°6_Maquette_PDF).

## Introduction

Les systèmes informatiques sont des systèmes destinés à traiter de
l'information. Pour traiter une information, il faut avant tout commencer par en
disposer. Le navigateur web est ainsi un système conçu pour communiquer avec un
serveur distant, c'est-à-dire lui fournir des informations sur les intentions de
l'utilisateur et, en contrepartie, en récupérer d'autres données utilisées pour
afficher la page web.

Il existe de nombreux canaux permettant de transférer de l'information entre
navigateur et serveur. Ils varient par le protocole utilisé (HTTP, Ajax,
WebSocket), l'emploi de l'une ou l'autre des méthodes disponibles dans le
protocole (GET, POST... pour HTTP), et la nature des informations transmises
(texte plein, cookies, JSON, HTML...). Cette liste loin d'être exhaustive est
destinée à vous donner quelques noms comme points d'entrée si vous souhaitez
poursuivre les recherches par vous-même.

Au cours du TP1, vous avez déjà appris une méthode pour communiquer avec un
serveur: la balise “`<a>`”. Cette balise est un moyen d' informer le serveur que
l'utilisateur souhaite consulter la page web dont l'URL est renseignée dans le
champ “href”. Lorsque l'utilisateur clique dessus, le navigateur la converti en
un message HTTP – GET.

Vous allez aujourd'hui apprendre à utiliser une autre méthode pour faire
parvenir des données au serveur: le formulaire HTML. Parmi tous les moyens pour
échanger de l'information, le formulaire occupe une place particulière. C'est en
effet le moyen privilégié pour échanger des données dont la nature est inconnue
ou seulement partiellement connue à l'avance par le serveur. Il offre donc à
l'utilisateur une relative liberté d'expression et permet au programmeur du
serveur d'obtenir des renseignements spécifiques connus du seul utilisateur.

*Réfléchissez à votre usage quotidien d'Internet. Pouvez-vous citer un exemple
très commun où vous entrez des informations (supposément) connues de vous seul
sur une page web ?*

## Bases

Le coeur du formulaire est constitué par deux types de balises: `<form>` et
`<input>`.

La balise `<form>` délimite le contenu du formulaire et renseigne plusieurs
attributs nécessaires au fonctionnement du formulaire:

* `method` : nom de la méthode HTTP utilisée pour envoyer les données. Peut prendre pour valeur “post” ou “get”.

   *Pour voir la différence, lorsque vous aurez un formulaire fonctionnel,
   ouvrez la console de votre navigateur (F12) à l'onglet “Réseau/Network” et
   postez le formulaire en post et en get. Que constatez-vous ?*

   La méthode “get” envoie les données comme composantes de l'URL du serveur et
   requiert par conséquent que: 1/ les données soient encodée pour être compatibles
   avec les spécifications URL, 2/ l'ensemble des données du formulaire + l'URL du
   serveur forment une chaîne de caractères de moins de 2000 caractères (limite
   imposée par certains navigateurs).

   La méthode “post” envoie les données dans le corps de la requête HTTP et ne
   présente pas la limitation de taille. Elle est donc à privilégier et sera la
   seule utilisée dans ce TP après le test ci-dessus.

* `action` : URL du serveur où les donnée du formulaire doivent être
  adressées. Deux URL vous seront fournies pendant le TP.

* `enctype` : le codage à utiliser pour envoyer les informations. Dans le cadre de
  ce TP, nous n'utiliserons pas cet attribut, qui prendra alors par défaut la
  valeur
  [“application/x-www-urlencoded”](http://www.w3.org/TR/html401/interact/forms.html#h-17.13.4.1).

La balise `<input>` permet de définir différents champs dans lesquels
l'utilisateur peut entrer des données. Ces champs offrent plus ou moins de
liberté d'expression selon le type utilisé. Elle a pour attributs:

* [`type`](http://www.w3schools.com/tags/att_input_type.asp) : défini
  l'apparence visuelle du champ et la nature des données qui peuvent y être
  renseignées.

* [`name`](http://www.w3schools.com/tags/att_input_name.asp) : le nom que
  prendra la donnée renseignée dans ce champ côté serveur. Vous comprendrez
  l'importance de ce paramètre quand vous aborderez la programmation
  serveur. Pour le TP, les valeurs seront fixées. Attention: il est important
  pour les types “checkbox” et “radio”d'utiliser le même nom pour les
  différentes options possibles !

* [`value`](http://www.w3schools.com/tags/att_input_value) : la valeur envoyée
  au serveur. Cet attribut n'est pas défini dans les champs libres et prend des
  valeurs fixées dont la liste des possibles est connue par le serveur pour les
  champs de type “checkbox” et “radio” et la balise `<option>`. Les valeurs
  seront fixées pour le TP.

Afin de pouvoir être envoyé, votre formulaire doit obligatoirement contenir une
balise `<input>` avec l'attribut `type=“submit”`. Cette balise définit le
bouton qui, cliqué, déclenchera l'envoi des données au serveur. (note: la balise
“submit” peut être remplacée par une balise “button” pour une utilisation
avancée, notamment en conjugaison avec Javascript).

*Sans plus attendre, créez une page HTML vierge et ajoutez-lui un formulaire
 basique comprenant une balise de type “text”. L'URL à renseigner dans “action”
 est indiquée au tableau. Pour tester votre formulaire, tapez un texte
 quelconque dans la zone de texte et envoyez le. Que constatez-vous ?*

## Formattage

*Vous allez à présent réaliser le formulaire de contact auquel le visiteur doit
pouvoir accéder depuis la page d'accueil de votre site web afin de poser une
question ou de formuler une demande.*

*Vous vous baserez sur la maquette disponible sur Moodle qu'il s'agira de
reproduire de la manière la plus fidèle possible.*

Remarquez que les informations du formulaire sont réparties en trois groupes
logiques :

* informations personnelles
* formation
* demande

Pour vous aider, vous trouverez sur le site de [w3schools](http://www.w3schools.com/html/html_forms.asp) une liste des balises
utilisables dans le contexte d'un formulaire. Notez les balises:

* [`<fieldset>`](http://www.w3schools.com/tags/tag_fieldset.asp): permet de
  regrouper plusieurs balises du formulaire. Elle comprend par ailleurs une
  sous-balise balise `<legend>` qui permet de fixer le nom apparaissant en haut du
  cadre.
* [`<label>`](http://www.w3schools.com/tags/tag_label.asp): permet de renseigner
  le nom associé à un champ `<input>`, `<select>`, etc. et visible sur le formulaire
  dans le navigateur. Cette balise comporte un attribut “for” qui doit prendre
  pour valeur la valeur de l'attribut “id” du champ auquel est associée
  l'étiquette (il faut donc penser à donner un “id” aux autres balises).
* [`<textarea>`](http://www.w3schools.com/tags/tag_textarea.asp): permet de
  définir une grande zone de texte
* [`<select>`](http://www.w3schools.com/tags/tag_select.asp): permet de définir
  une liste déroulante. Les différentes valeurs possibles de la liste déroulante
  sont définies dans une succession balises `<option>` inclues dans la balise
  `<select>`

*Par convention d'usage, le nom des champs obligatoires est suivi d'une *.*

*Le formulaire doit être lisible et élégant. Pensez donc à attribuer des “id” ou
“class” aux différentes éléments et faire usage de vos acquis en CSS du TP2 pour
formatter l'aspect visuel de votre formulaire. Contrairement à l'exemple donné
dans “formulaire.pdf”, les différents champs d'entrée doivent tous avoir leur
bord gauche aligné verticalement quand ils sont sur la même ligne que leur
légende.*

<!-- Comment fait-on pour avoir les champs texte alignés à gauche ?
Proposition : le label devient un inline-block (ou le père un flex) dont on spécifié la largeur
Besoin sûrement de box-sizing : border-box 
-->

Valeurs à utiliser pour les attributs (respectez les si vous voulez que le
serveur vous aide):

* sexe:
   * name: “sex”
   * values: féminin: “sex_fem”, masculin: “sex_male”
* nom: name: “lastname”
* prénom: name: “firstname”
* email: name: “email”
* formation en cours:
   * name: “cur_training”
   * values: 2nd: “2”, 1st: “1”, term: “0”, sup: “3”, autre: “4”
* bac:
   * name: “bac”,
   * values: S: “0”, ES: “1”, L: “2”, STI2D: “3”, techno: “4”, pro: “5”, autre: “6”
* option ISN:
   * name: “isn”
   * values: oui: “1”, non: “0”
* formation requête:
   * name: “req-training[]” (le [] indique que plusieurs valeurs peuvent être fournies)
   * values: DUT: “0”, DUT AS: “1”, LP: “2”
* question: name: “request”
* action du formulaire: voir au tableau

*Commencez par définir la balise `<form>` et ajouter un bouton pour soumettre le
formulaire. N'hésitez pas dès lors à tester régulièrement vos progrès en
soumettant votre formulaire au serveur.*

## Différence entre les types de champs

Les boutons radio permettent de ne sélectionner qu'une seule des options
possibles. Les cases à cocher permettent de sélectionner autant d'options que
l'utilisateur le souhaite. La liste déroulante permet de base de ne sélectionner
qu'une option. Plusieurs options peuvent être sélectionnées si l'attribut
“multiple” est ajouté à la balise `<select>`.

Les différences ci-dessus mises à part, la différence entre ces 3 types est
purement cosmétique.

Le type “password” masque automatiquement les caractères entrés.

Le type “hidden” n'est pas affiché visuellement par le navigateur, ce qui permet
vous permet d'envoyer au serveur des informations dont il aura besoin mais dont
vous ne souhaitez pas encombrer l'utilisateur (ex: un état de la page).

Les types “email”, “url”, “tel”, “date”, “time” et “number” permettent d'adapter
le clavier virtuel quand la page est affichée sur un smartphone.

## Ergonomie et convivialité

Au-delà du simple aspect visuel du formulaire, le langage HTML met à votre
disposition de nombreux moyens pour le rendre plus ergonomique et convivial.

### Navigation

Pour les utilisateurs avancés, la navigation à l'aide de la touche “tabulation”
permet de parcourir très vite le formulaire. L'attribut “autofocus” permet de
spécifier au navigateur quel élément du formulaire doit avoir le focus en 1e
quand la page est chargée. L'attribut “tabindex” permet de spécifier l'ordre
dans lequel les éléments sont parcourus en appuyant sur “tabulation”.

*Nous n'en ferons pas usage ici.*

### Contrôle du contenu

La sécurité de votre serveur et de vos utilisateur imposent que vous contrôliez
toujours les données entrées, au niveau du serveur (vous verrez cela plus
tard). Toutefois, le contrôle par le serveur demande à ce que les données soient
envoyée, que le serveur teste, puis réponde. L'opération peut être longue.

Afin d'éviter une attente inutile aux utilisateurs de votre formulaire, vous
pouvez demander au navigateur d'effectuer directement certains tests avant
l'envoi du formulaire, afin de prévenir les erreurs courantes (ex: mauvais
numéro de téléphone, mauvaise date...). Attention: cela ne vous dispense quand
même pas de procéder aux vérifications côté serveur !  Deux attributs permettent
de vérifier le contenu du formulaire:

* required: spécifie que le champ doit être obligatoirement rempli. Attribut à
  ajouter à tous les champs dont la légende comporte une *
* pattern: attribut spécifique aux champs “libres”, il permet de spécifier une
  [expression régulière](http://www.rexegg.com/). Cette chaîne de caractère au
  [format particulier](http://www.rexegg.com/regex-quickstart.html#ref) indique
  au navigateur tous les formats d'entrée autorisés pour le champ et le
  navigateur refusera d'envoyer le formulaire si un champ n'est pas correctement
  rempli. Par exemple, un “pattern” égal à “0[1-9](\.\d{2}){4}” permettra de
  s'assurer qu'un numéro de téléphone respecte bien les règles de numérotation
  françaises, tandis que le pattern “[a-z0-9._-]+@[a-z0-9.-]+\.[a-z]{2,4}”
  bloquera les erreurs d'adresse email les plus grossières. Vous trouverez de
  nombreux exemples de patterns utilisables dans ce cas du
  [HTML5pattern](http://html5pattern.com/). Note: les patterns HTML sont
  automatiquement évalués contre la totalité de l'entrée. Il est donc inutiles
  de les encadrer entre ^ et $ comme une expression régulière classique.

*Ajoutez au champ “question” de votre formulaire un pattern qui permette de vous
 assurer que les caractères “<”, “>”, “=”, “ ' ”, “ '' ”, “(” et “)” sont
 interdits. Cela peut fournir une protection (très primitive et en aucun cas
 suffisante) contre certaines formes d'attaques contre le serveur.*

### Convivialité

Quelques attributs permettent d'améliorer la convivialité des champs de votre formulaire:

* placeholder: permet d'afficher une ligne de texte dans le champ qui disparaît
  dès lors que l'utilisateur tape une information. Cela permet de donner à
  l'utilisateur des renseignements sur le contenu attendu. A utiliser
  impérativement avec les champs pour lesquels vous avez spécifié un “pattern”,
  sous peine de cause une extrême frustration à l'utilisateur. Vous devez alors
  utiliser l'attribut “placeholder” pour spécifier le format attendu, les
  caractères interdits/autorisés, etc.

   ex:  placeholder=“abcd@gmail.com”

* checked / selected: pour les types “radio” et “checkbox”, et pour `<option>`
respectivement. Cet attribut permet de spécifier que l'option en question est
sélectionnée/cochée par défaut. Utile quand vous savez que l'une des options
sera utilisée beaucoup plus fréquemment que les autres. Vous épargnez alors du
temps à l'utilisateur.

*Faites usage de ces options dans votre formulaire pour le rendre plus
convivial.*

Auteur du TD : Benjamin Faivre-Vuillin

**Note de Romain:** Est-ce qu'il parle de disabled, input type=hidden, readonly ? Que le traitement des formulaires est fait en S3 dans le cours ProgWeb Coté Serveur ?

## Autres Idées 

Parler rapidement des caractères spéciaux en HTML &lt; < ... et peut-être aussi
de l'encodage des caractères dans l'URL quand on fait les formulaires
-> Ecrire le texte : la balise <a>

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



### holy grail layout

Nous sommes en 2015, et jusquà peu il n'est toujours pas évident de faire ce layout (d'où son nom).

https://philipwalton.github.io/solved-by-flexbox/

### sticky footer ?

en flex ?

### Media Object

### le model par défaut

### le border-layout

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
