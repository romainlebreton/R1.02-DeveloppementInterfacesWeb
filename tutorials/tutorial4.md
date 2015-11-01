---
title: TD4
subtitle: Les formulaires.
layout: tutorial
---

## Introduction

Nous allons ajouter un formulaire d'inscription à notre site de fans de <strong>Chuck Norris</strong>, en utilisant la balise `form`.
Cette balise `<form>` nous permettra d'avoir des réponses à des questions ouvertes ("Que voulez vous dire à Chuck ?") 
au plus fermées ("Parmis ces trois choix quel est votre sport favoris ?", "Quel est votre sexe ?" ..." ).
Il y a beaucoup de type de questions, correspondant chacune à un type de balises `<input>` ou `<textarea>`.

## La balise  `<form>` et les balises `<input>`

Le coeur du formulaire est constitué par deux types de balises: `<form>` et `<input>`.


La balise `<form>` délimite le contenu du formulaire et renseigne plusieurs
attributs nécessaires au fonctionnement du formulaire:

* `method`: nom de la méthode HTTP utilisée pour envoyer les données. Peut prendre pour valeur “post” ou “get”.

   * `get` envoie les données comme composantes de l'URL du serveur et
   requiert par conséquent que: 1/ les données soient encodée pour être compatibles
   avec les spécifications URL, 2/ l'ensemble des données du formulaire + l'URL du
   serveur forment une chaîne de caractères de moins de 2000 caractères (limite
   imposée par certains navigateurs).

   * `post` envoie les données dans le corps de la requête HTTP et ne
   présente pas la limitation de taille, elle est donc à privilégier.

* `action` : URL du serveur où les donnée du formulaire doivent être
  envoyées. 

La balise `<input>` permet de définir différents champs dans lesquels
l'utilisateur peut entrer des données. Ces champs offrent plus ou moins de
liberté d'expression selon le type utilisé. Elle a pour attributs:

* [type](http://www.w3schools.com/tags/att_input_type.asp): défini l'apparence
  visuelle du champ et la nature des données qui peuvent y être renseignées.

* `name` : le nom que prendra la donnée envoyée au server. Par exemple si l'input a pour `name` firstname et pour valeur "Éric". L'envoit du formulaire contiendra une association "name-->Éric" que le serveur devra interprété et traiter.

* `value` : la valeur envoyée au serveur. Cet attribut n'est pas défini dans les
  champs libres et prend des valeurs fixées dont la liste des possibles est
  connue par le serveur pour les champs de type “checkbox” et “radio” et la
  balise `<option>`.

Afin de pouvoir être envoyé, votre formulaire doit obligatoirement contenir une
balise `<input>` avec l'attribut “type” fixé à “submit”. Cette balise définit le
bouton qui, cliqué, déclenchera l'envoi des données au serveur.

<div class="exercise" id="start">

Nous allons voir comment est envoyé la valeur d'un `<input>` lorsque l'on soumet un formulaire.

 1. Créez une nouvelle page inscription.html au site de Chuck Norris. Cette page va contenir le formulaire d'inscription 
 aux fan club de Chuck que nous allons construire dans ce TD.

 1. Ajoutez à la page inscription.html le formulaire suivant : <br> <br>
`<form action="sendtoMySecondYearInIut.php" method="post">`<br>&nbsp;
	`<input name="uname" type="text" >`<br>&nbsp;
		`<input type="submit" value="Envoyer">`<br>
	`</form>`

  1. Affichez la page et ouvrez la console (F12) pour aller sur l'onglet 'Réseau',
  Donnez la valeur `dupont` au champ texte, puis cliquez sur le bouton "Envoyer" du formulaire. 
  Vous devez voir une requête contenant `sendToMySecondYearInIut` dans la console. Cliquez sur cette ligne et cherchez la valeur `dupont` dans les détails de la transaction.
 1. Donnez à l'attribut `method` du formulaire la valeur `get`. Cliquez sur le bouton "Envoyer" du formulaire, l'url doit maintenant finir par "sendToMySecondYearInIut.php?uname=dupont". 

</div>

<strong>Note</strong> : il est normal que l'adresse `sendToMySecondYearInIut.php` n'existe pas (le fameux code de retour HTTP <strong>404</strong> apparaît dans la console), puisque vous êtes en première année. Nous verrons en deuxième année dans le cours ProgWeb Coté Serveur comment le serveur récupère les données envoyées par notre formulaire. 


## `label`

Il nous faut informer maintenant par un label à quoi noter champ `<input>` fait référence. La balise [`<label>`](http://www.w3schools.com/tags/tag_label.asp) permet d'associer la question sous-tendu ("Nom? ") à l'input. Cette balise comporte un attribut `for` qui doit prendre pour valeur la valeur de l'attribut `id` du champ auquel est associée le `label`  (il faut donc penser à donner un `id` à notre `<input>`).


<div class="exercise" id="exlabel">

 1. Remplacez le code de votre champs input par le code suivant : <br>
 			`<label for="surname">Nom</label>`<br>
				`<input id="surname" name="uname" type="text" >`

 1. Rajoutez au formulaire une entrée qui correspondra au prénom (calqué sur le précédent).
 1. Validez ce dernier et vérifiez que vos deux champs font bien présents dans l'url du navigateur (l'url doit finir par `sendToMySecondYearInIut.php?uname=dupont&firstname=super`).
 1. Les deux champs apparaissent les uns à la suite des autres. Avec quelle balise vue dans le Td précédent doit on les mettre pour qu'il y est un saut de ligne entre les deux ?

</div>

## Les princpaux type de balises `<input>`

Il existe un assez grand nombre de type d'input.

 * Le type `radio` permet de ne sélectionner qu'une seule des options
possibles.
 * Le type `checkbox` (Les cases à cocher) permettent de sélectionner autant des options que l'utilisateur le souhaite.
 * Le type `password` masque automatiquement les caractères entrés.
 * Les types `email`, `url`, `tel`, `date`, `time` et `number` permettent d'adapter le clavier virtuel quand la page est affichée sur un smartphone. 
 Suivant le navigateur, une présentation différente peut-être associée. Des validateurs sont associés à ces champs (nous le verrons plus loin), 
 ils vérifient pas exemple qu'une adresse mail contient bien un "@".


<strong>Note :</strong> Certains de ces inputs sont issus de la norme HTML5. De fait leurs adoptions au sein des navigateurs n'est pas uniforme. Les développeurs web peuvent être amenés à demander la nature du parc informatique cible du site web qu'ils doivent implémenter (en clair ils demandent : "quel est la version d'Internet Explorer encore en cours sur votre parc ?"). Le site [caniuse](http://caniuse.com/) permet ensuite de savoir si nous pouvons utiliser tel ou tel aspect pour la réalisation d'un site. Les types date et time par exemple sont [plus ou moins bien supportés](http://caniuse.com/#search=date) par les navigateurs. Le type number l'est [un peu plus](http://caniuse.com/#search=number). 


<div class="exercise" id="exinput">
 
Ajoutez dans le formulaire les `<input>` libellés :

 1. "Sexe" avec les deux valeurs que vous connaissez.
 1. "Date de naissance" avec le type d'input `date`.
 1. "Mot de passe" avec le type d'input `password`.
 1. "Email" avec le type d'input de type ... `email`.
 1. "Niveau en Karaté" avec le type d'input `number` allant de 0 à 5.
 1. "Message à Chuck" avec un `<textarea>`.
 1. "Niveau d'engagement" avec trois valeurs comme autant de case à cocher libellées "Basique (5€) ", "Gold (15€)" et "Tatane in your face (50€)".
 1. "J'ai bien lu les clauses que j'ai pas lu" associé à une case à cocher. 
 1. Vérifier par envoi du formulaire que tous les champs sont bien renseignés, on rappelle que c'est l'attribut `name` de l'input qui est utilisé.
 1. (optionnel) rendre la coche obligatoire avec l'attribut `required`. Vérifiez si l'envoi du formulaire est bien impossible alors.
 
</div>

<string>Note :</string>strong>

 * A propos du mot de passe, remarquez que ce dernier apparait en clair dans l'url si vous êtes en `get` lors  de l'envoi via `sendToMySecondYearInIut`. 
Définitivement donc, un envoi avec `post` doit être privilégié.
 * Il doit y avoir un saut de ligne entre chaque `<input>` comme dans le dernier exercice de la section précédente.

## `<select>`

Voyons mantenant un autre élmement important d'un formulaire, correspondant à la balise `<select>`.
Il permet de choisir parmis un ensemble de choix imposées une ou plusieurs valeurs présentées par un menu déroulant.
Tout comme `<input>`, cet élément peut aussi être libellé via un `label`. La liste déroulante permet de base de ne sélectionner
qu'une option. Plusieurs options peuvent être sélectionnées si l'attribut `multiple` est ajouté à la balise `<select>`. Des groupes de choix peuvent être proposés 

<div class="exercise" id="exlabel">
 1. Ajoutez un `<select>` libellé "Pays d'origine" qui prend comme valeur de pays `U.S.A` , `France`, `Chine` et `Viêt Nam`, les clées associées ne doivent pas dépendre de la langue du formulaire (la cléé associée à `France` doit être `fr` par exemple). L'utilisateur ne peut pas sélectionner plusieurs valeurs.

 1. Ajoutez à la suite de ce champ un aute sélecteur libellé "Arts martiaux préférés". Les valeurs sont "Kung fu" , "Karaté" et "Full-contact". L'utilisateur peut sélectionner plusieurs valeurs.
</div>

## `<textarea>`
* [`<textarea>`](http://www.w3schools.com/tags/tag_textarea.asp): permet de
  définir une grande zone de texte

<div class="exercise" id="exlabel">

 1. Ajoutez un champs libellé "Message pour Chuck" associé à un `<textarea>` sur lequel l'utilisateur peut s'épancher.
</div>



## `<fieldset>`



<div class="exercise" id="exlabel">
Remarquez que les informations du formulaire sont réparties en trois groupes
logiques :

* informations personnelles (Nom, Prénom, mail, etc.),
* Les sports de combats ("Sport de combat préféré"" et "Niveau en Karaté"),
* des infos relatives à l'inscription ("Message personel à Chuck", mot de passe, la coche "J'ai bien lu..", "Niveau d'engagement', etc.).

Regroupez les champs sur ces trois grands axes avec la balise `filedset`.
</div>


## Ergonomie et convivialité

<div class="exercise" >
 1. Par convention d'usage, le nom des champs obligatoires est suivi d'une "*". Ajoutez le aux champs Nom mail et à la coche "J'ai bien lu....".
</div>


### Navigation

Pour les utilisateurs avancés, la navigation à l'aide de la touche “tabulation”
permet de parcourir très vite le formulaire. L'attribut “autofocus” permet de
spécifier au navigateur quel élément du formulaire doit avoir le focus quand la page est chargée. L'attribut “tabindex” permet de spécifier l'ordre
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

* `required`: spécifie que le champ doit être obligatoirement rempli. Attribut à
  ajouter à tous les champs dont la légende comporte une *
* `pattern`: attribut spécifique aux champs “libres”, il permet de spécifier une
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

<div class="exercise" id="regulex" >




 1. Ajoutez un pattern au champ mot de passe afin que celui ci contienne obligatoirement 8 ou plus caractères avec au moins un chiffre, une lettre majuscule et une lettre minuscule.

</div>

<strong> Note : </strong> Pour être toujours protégé contre les bugs lorque vous cogiter une expression régulière, ne sortez jamais sans votre [Regulex](https://jex.im/regulex). Regulex, le visualisateur de machine d'état qu'il vous faut pour vos expressions régulières.

### Convivialité

Quelques attributs permettent d'améliorer la convivialité des champs de votre formulaire:

* `placeholder`: permet d'afficher une ligne de texte dans le champ qui disparaît
  dès lors que l'utilisateur tape une information. Cela permet de donner à
  l'utilisateur des renseignements sur le contenu attendu. A utiliser
  impérativement avec les champs pour lesquels vous avez spécifié un “pattern”,
  sous peine de cause une extrême frustration à l'utilisateur. Vous devez alors
  utiliser l'attribut `placeholder` pour spéficier le format attendu, les
  caractères interdits/autorisés, etc.

   ex:  placeholder=“Entrez votre nom ici."

* `checked` / `selected` : pour les types “radio” et “checkbox”, et pour `<option>`
respectivement. Cet attribut permet de spécifier que l'option en question est
sélectionnée/cochée par défaut. Utile quand vous savez que l'une des options
sera utilisée beaucoup plus fréquemment que les autres. Vous épargnez alors du
temps à l'utilisateur.

<div class="exercise" >

 1. Ajouter placeholder=“abcd@gmail.com” au champ mail.
 1. Ajoutez un attribut `placeholder` dans le textarea avec le texte suivant "Un inscrit sera tiré au sort pour voir son message transmis à Chuck Norris"

</div>


<strong>Note : </strong> Il existe depuis peu un pseudo attribut css `::placeholder`, mais celui-ci et [moins](http://caniuse.com/#search=placeholder%20css) bien supporté que 
l'[attribut](http://caniuse.com/#search=placeholder%20attribute).


## Style 


*Faites usage de ces options dans votre formulaire pour le rendre plus
convivial.*


**Note de Romain:** Est-ce qu'il parle de disabled, readonly ?  

integrer l'exo sur les expressions régulières.