---
title: TD4
subtitle: Les formulaires.
layout: tutorial
---

## Introduction

Nous allons ajouter un formulaire d'inscription à notre site de fans de <strong>Chuck Norris</strong>, en utilisant la balise `form`.
Cette balise `form` nous permettra d'avoir des réponses à des questions ouvertes ("Que voulez vous dire à Chuck ?") 
au plus fermées ("Parmis ces trois choix quel est votre sport favoris ?", "Quel est votre sexe ?" ..." ).

Il y a beaucoup de type de questions, correspondant chacune à un type de balises `input` ou `textarea`.

## La balise  `<form>` et les balises `input`

Le coeur du formulaire est constitué par deux types de balises: `<form>` et
`<input>`.


La balise `<form>` délimite le contenu du formulaire et renseigne plusieurs
attributs nécessaires au fonctionnement du formulaire:

* `method`: nom de la méthode HTTP utilisée pour envoyer les données. Peut prendre pour valeur “post” ou “get”.

   *Pour voir la différence, lorsque vous aurez un formulaire fonctionnel,
   ouvrez la console de votre navigateur (F12) à l'onglet “Réseau/Network” et
   postez le formulaire en post et en get. Que constatez-vous ?*

   La méthode `get` envoie les données comme composantes de l'URL du serveur et
   requiert par conséquent que: 1/ les données soient encodée pour être compatibles
   avec les spécifications URL, 2/ l'ensemble des données du formulaire + l'URL du
   serveur forment une chaîne de caractères de moins de 2000 caractères (limite
   imposée par certains navigateurs).

   La méthode `post` envoie les données dans le corps de la requête HTTP et ne
   présente pas la limitation de taille. 
   Elle est donc à privilégier, cela dit pour des raisons de tests nous serons amenés à utiliser `get`.
   seule utilisée dans ce TP après le test ci-dessus.

* `action` : URL du serveur où les donnée du formulaire doivent être
  adressées. 

La balise `<input>` permet de définir différents champs dans lesquels
l'utilisateur peut entrer des données. Ces champs offrent plus ou moins de
liberté d'expression selon le type utilisé. Elle a pour attributs:

* [type](http://www.w3schools.com/tags/att_input_type.asp): défini l'apparence
  visuelle du champ et la nature des données qui peuvent y être renseignées.

* `name` : le nom que prendra la donnée renseignée dans ce champ côté serveur. Vous
  comprendrez l'importance de ce paramètre quand vous aborderez la programmation
  serveur. Pour le TP, les valeurs seront fixées. Attention: il est important
  pour les types “checkbox” et “radio”d'utiliser le même nom pour les
  différentes options possibles !

* `value` : la valeur envoyée au serveur. Cet attribut n'est pas défini dans les
  champs libres et prend des valeurs fixées dont la liste des possibles est
  connue par le serveur pour les champs de type “checkbox” et “radio” et la
  balise `<option>`. Les valeurs seront fixées pour le TP.

Afin de pouvoir être envoyé, votre formulaire doit obligatoirement contenir une
balise `<input>` avec l'attribut “type” fixé à “submit”. Cette balise définit le
bouton qui, cliqué, déclenchera l'envoi des données au serveur. (note: la balise
“submit” peut être remplacée par une balise “button” pour une utilisation
avancée, notamment en conjugaison avec Javascript).



<div class="exercise" id="start">

Le but de cet exercice est de voir succinctement est envoyé un champ lorsque l'on soumet un formulaire.

 1. Créez une nouvelle du site Chuck Norris libellé "Faire parti du club" qui renvoit à une page inscription.html.
Elle va contenir le formulaire d'inscription aux fan club de Chuck que nous allons construire dans ce TD.

 1. Ajoutez à la page inscription.html le formulaire suivant : <br> <br>
`<form action="sendtoMySecondYearInIut.php" method="post">`<br>&nbsp;
	`<input name="uname" type="text" ></input>`<br>&nbsp;
		`<input type="submit" value="Envoyer">`<br>
	`</form>`

  1. Affichez la page et ouvrez la console (F12) pour aller sur l'onglet 'Réseau',
  Donnez la valeur `dupont` au champ texte, puis cliquez sur le bouton "Envoyer" du formulaire. 
  Vous devez voir une requête contenant `sendToMySecondYearInIut` dans la console. Cliquez sur cette ligne et cherchez la valeur `dupont` dans les détails de la transaction.
 1. Donnez à l'attribut `method` du formulaire la valeur `get`. Cliquez sur le bouton "Envoyer" du formulaire, l'url doit maintenant finir par "sendToMySecondYearInIut.php?uname=dupont". 

</div>

Notes :

 * S'il est tout indiqué d'utiliser dans le formulaire qui va suivre la valeur de method `post`, on va utiliser juste pour les tests la valeur `get` de manière à pouvoir valider via l'url dans le navigateur que nos champs sont bien envoyés.
 
 * Il est normal que l'adresse `sendToMySecondYearInIut.php` n'existe pas (le fameux code de retour HTTP 404), puisque vous êtes en première année. Nous verrons en deuxième année dans le cours ProgWeb Coté Serveur comment le serveur récupère les données envoyées par notre formulaire.


## `label`

Notre formulaire n'est pas très explicite : on ne sait pas ce que l'on doit rentrer dans le champs texte.

La balise [`<label>`](http://www.w3schools.com/tags/tag_label.asp) permet d'associer la question sous-tendu ("Nom? ") à l'input (on utilisera le label "Nom"). 
Cette balise comporte un attribut `for` qui doit prendre pour valeur la valeur de l'attribut `id` du champ auquel est associée l'étiquette 
(il faut donc penser à donner un `id` aux autres balises).


<div class="exercise" id="exlabel">

 1. Remplacez le code de votre champs input par le code suivant : <br>
 			`<label for="surname">Nom</label>`<br>
				`<input id="surname" name="uname" type="text" ></input>`

 1. Rajoutez au formulaire une entrée qui correspondra au prénom (calqué sur le précédent, avec un `label` et un champ `input`).
 1. Vérifiez après avoir remplis le formulaire et valider ce dernier que vos deux champs font bien parti de l'url du navigateur `sendToMySecondYearInIut.php?uname=dupont&firstname=super`.
 1. Les deux champs apparaissent les uns à la suite des autres. Avec quelle balise vue dans le Td précédent doit on les mettre pour qu'il y est un saut de ligne entre les deux ?

</div>

## Les princpaux type d'`input`

 * Le type `radio` permet de ne sélectionner qu'une seule des options
possibles.
 * Le type `checkbox` (Les cases à cocher) permettent de sélectionner autant des options que l'utilisateur le souhaite. 
 * Le type `password` masque automatiquement les caractères entrés.
 * Le type `hidden` n'est pas affiché visuellement par le navigateur, ce qui permet
vous permet d'envoyer au serveur des informations dont il aura besoin mais dont
vous ne souhaitez pas encombrer l'utilisateur (ex: un état de la page).
 * Les types “email”, “url”, “tel”, “date”, “time” et “number” permettent d'adapter
le clavier virtuel quand la page est affichée sur un smartphone. Suivant le navigateur, une présentation différente peut-être associée.
 Des validateurs sont associés à ces champs (nous le verrons plus loin), ils vérifient pas exemple qu'une adresse mail contient bien un @.

<div class="exercise" id="exlabel">
 
 1. Ajoutez un input libellé "Sexe" avec les deux valeurs que vous connaissez.
 1. Ajoutez un input libellé "Date de naissance" avec le type d'input `date`.
 1. Ajoutez un input libellé "Mot de passe" avec le type d'input `password`.
 1. Ajoutez un input libellé "Email" avec le type d'input `email`.
 1. Ajoutez un input libellé "Niveau en Karaté"" avec le type d'input `number` allant de 0 à 5.
 1. Ajoutez un input libellé "Message à Chuck" avec le textlabeltype d'input `email`.
 1. Ajoutez un input libellé "Niveau d'engagement" avec trois valeurs comme autant de case à cocher libéllées "Basique (5€) ", "Gold (15€)" et "Tatane premier (50€)".
 1. Ajoutez un input libellé "J'ai bien lu les clauses que j'ai pas lu" associé à une coche.
 1. (optionel) rendre la coche obligatoire avec l'attribut `required`.


</div>

Note 

 * A propos du mot de passe, remarquez que ce dernier apprait en clair dans l'url lors  de l'envoi via `sendToMySecondYearInIut`. 
Définitivement ici un envoi avec `post` devrait être privilégié s'il s'agit d'un vrai site.
 * Il doit y avoir un saut de ligne entre chaque input comme dans le dernier exercice de la section précédente.

## `select`

Voyons mantenant un autre élmement important d'un formulaire,  correspondant à la balise `select`.
Il permet de choisir parmis un ensemble de choix imposées une ou plusieurs valeurs présentées par un menu déroulant.
Tout comme `input`, cet élément peut aussi être libellé via un `label`.

La liste déroulante permet de base de ne sélectionner
qu'une option. Plusieurs options peuvent être sélectionnées si l'attribut
`multiple` est ajouté à la balise `<select>`.

<div class="exercise" id="exlabel">
 1. Ajoutez un select libellé "Pays d'origine" qui prend comme valeur de pays `U.S.A` , `France`, `Chine` et `Viêt Nam`, les clées associées ne doivent pas dépendre de la langue du formulaire (la cléé associée à `France` doit être `fr` par exemple). L'utilisateur ne peut pas sélectionner plusieurs valeurs.

 1. Ajoutez à la suite de ce champs un aute sélécteur libéllé "Arts martiaux préférés". Les valeurs sont "Kun fu" , "Karaté" et "Full-contact". L'utilisateur peut sélectionner plusieurs valeurs.
</div>

## `textarea`
* [`<textarea>`](http://www.w3schools.com/tags/tag_textarea.asp): permet de
  définir une grande zone de texte

<div class="exercise" id="exlabel">

 1. Ajoutez un champs libellé "Message pour Chuck" associé à un textarea sur lequel l'utilisateur peut s'épancher.
</div>



## `fieldset`


Remarquez que les informations du formulaire sont réparties en trois groupes
logiques :

* informations personnelles (nom, prénom, mail,...),
* "Sport de combat préféré"" et "Niveau en Karaté",
* Message personel à Chuck, mot de passe pour le compte, la coche "J'ai bien lu.." et "Niveau d'engagement'.

Regouper les champs sur ces trois grands axes avec la balise `filedset`.


## Ergonomie et convivialité

<div class="exercise" >
 1. Par convention d'usage, le nom des champs obligatoires est suivi d'une "*". Ajoutez le aux champs Nom mail et à la coche "J'ai bien lu....".

</div>


### Navigation

Pour les utilisateurs avancés, la navigation à l'aide de la touche “tabulation”
permet de parcourir très vite le formulaire. L'attribut “autofocus” permet de
spécifier au navigateur quel élément du formulaire doit avoir le focus en 1e
quand la page est chargée. L'attribut “tabindex” permet de spécifier l'ordre
dans lequel les éléments sont parcouris en appuyant sur “tabulation”.


### Contrôle du contenu

La sécurité de votre serveur et de vos utilisateur imposent que vous contrôlliez
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

* `placeholder`: permet d'afficher une ligne de texte dans le champ qui disparaît
  dès lors que l'utilisateur tape une information. Cela permet de donner à
  l'utilisateur des renseignements sur le contenu attendu. A utiliser
  impérativement avec les champs pour lesquels vous avez spécifié un “pattern”,
  sous peine de cause une extrême frustration à l'utilisateur. Vous devez alors
  utiliser l'attribut `placeholder` pour spéficier le format attendu, les
  caractères interdits/autorisés, etc.

   ex:  placeholder=“abcd@gmail.com”

* checked / selected: pour les types “radio” et “checkbox”, et pour `<option>`
respectivement. Cet attribut permet de spécifier que l'option en question est
sélectionnée/cochée par défaut. Utile quand vous savez que l'une des options
sera utilisée beaucoup plus fréquemment que les autres. Vous épargnez alors du
temps à l'utilisateur.

<div class="exercise" >

 1. Ajoutez un attribut `placeholder` dans le textarea avec le texte suivant "Un inscrit sera tiré au sort pour voir son message transmis à Chuck Norris"

</div>

## Style 


*Faites usage de ces options dans votre formulaire pour le rendre plus
convivial.*


**Note de Romain:** Est-ce qu'il parle de disabled, readonly ?  

