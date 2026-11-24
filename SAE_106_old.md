---
title: Modalités du site de la SAÉ 1.06
subtitle: Planning et cahier des charges
layout: tutorial
lang: fr
---

## Sujet

Vous devez réaliser le site Web présentant votre controverse sociotechnique de la SAÉ 1.06.
Pour rendre ce site web accessible, vous utiliserez le dossier `public_html` de l'un des membres du groupe comme vu en TD.
La date limite de rendu est le vendredi 18/12. Le rendu se fera sur [l'espace Moodle du cours](https://moodle.umontpellier.fr/course/view.php?id=28316). 

Il faudra rendre dans un dossier compressé :
- les fichiers sources du site,
- un fichier `readme.md` précisant:
   - les membres du groupe, leurs parts d'implication dans le projet,
   - le lien vers votre site web.
   - le lien vers le dépôt gitlab comportant les fichiers sources du site, attention à ajouter votre enseignant en tant que 'developer', vous y ajouterez aussi ce fichier `readme.md`.

### Héberger le site

Le site devra être hébergé sur le serveur webinfo. Les indications se trouvent dans les [consignes de la SAÉ 1.05](SAE_105.html)

### Le contenu de votre site :

Il y aura un menu de navigation avec sous-menus commun à toutes vos pages :
une entrée du menu dédiée à chaque page avec au moins un sous-menu déroulant qui permet d'accéder directement à différents points d'ancrage de la page. 
Comme vu en TD, ce menu devra être responsive et donc être remplacé par un menu burger équivalent si la zone d'affichage est petite. 

On demandera aussi de distinguer l'entrée du menu correspondant à la page actuellement affichée (par exemple, en utilisant des couleurs).
Pour cela, on pourra simplement modifier légèrement le code HTML du menu d'une page à l'autre en donnant une classe à certains éléments.

Voici une liste minimale de pages que vous devez avoir :

1. Une page d'accueil introduisant le sujet.
1. Au moins deux autres pages regroupant chacune certains aspects du sujet
(vous pouvez aller jusqu'à 3 ou 4 pages si cela permet un découpage plus pertinent pour couvrir les différents aspects à traiter).
Vous pourrez vous baser sur votre analyse de la controverse selon la méthode PESTEL pour le contenu de votre site. Si besoin, vous pourrez compléter avec du *Lorem Ipsum*.
1. **Contact :** Une page formulaire ”contactez nous”, avec

   1. les informations sur le demandeur (nom, prénom, adresse email, code postal, champs de sélection du pays),
   1. une question "vous avez entendu parler de nous via ?” avec plusieurs choix possibles <!-- checkbox -->
   1. un champ "date à laquelle vous souhaitez être recontacté" 
   1. un champ texte libre de plusieurs lignes d'expression libre

   Pour chacun des champs, un exemple sera donné, une vérification du format sera
   faite à l’aide des types prédéfinis en HTML5 (l’utilisation d’expressions régulières
   est optionnelle). Le formulaire devra envoyer les données à la page [https://webinfo.iutmontp.univ-montp2.fr/~eturosenfeld/php_pour_TD5/exempleTraitement.php](https://webinfo.iutmontp.univ-montp2.fr/~eturosenfeld/php_pour_TD5/exempleTraitement.php). Vous vérifierez notamment que le formulaire envoie correctement les informations de la question à réponses multiples quand plusieurs réponses sont sélectionnées.



### Consignes générales

Vous devrez mettre en application les techniques que vous avez apprises lors des TDs. Voici donc les critères techniques sur lesquels vous serez
notés :
<!-- **[les critères techniques sur lesquels vous serez notés:](https://docs.google.com/spreadsheets/d/1CHQ6imNxRFWHETmVZbRyPIxg8hV8nVrNcHthe1TGHxg/edit?usp=sharing)** -->


1. les codes CSS et HTML seront lisibles et correctement indentés. L’utilisation
   de CSS de style *inline* est interdit.
1. le visuel du site (charte graphique) doit être cohérent sur toutes les pages du site.
1. l’utilisation de framework tels que *bootstrap*, *foundation*, etc. n’est pas autorisée. 
1. l’utilisation des *float* ou des tableaux **n’est pas autorisée pour la mise
   en page**, c'est-à-dire par exemple pour mettre une colonne à côté d'une
   autre ... Par contre, on peut se servir de *float* pour son usage
   historique : entourer une image de texte.
1. l’utilisation des `<br\>` **n’est pas autorisée pour la mise en page**. 
1. le site sera responsive. En particulier, le menu s'adaptera à la taille de la
   page. Le site doit s'afficher correctement sur ordinateur, tablette et petit smartphone (pas besoin de se soucier des smartwatch).
1. Le site doit fonctionner aussi bien sous Chrome, Edge, Firefox, Safari...

Quelques points supplémentaires que nous vérifierons pour l'évaluation :

1. Valider vos fichiers HTML et CSS avec les validateurs HTML5 et CSS3 déjà utilisés en TD.
1. Déclarer l'encodage UTF8 des caractères.
1. Plusieurs fontes importées avec fonte de secours (*fallback*).
1. Maîtrise des différentes propriétés de *flex*.
1. Variété des balises utilisées.

Pour l'évaluation, nous serons particulièrement attentifs aux critères que nous n'avons pas évalués pour le site précédent (en particulier responsive design et formulaires).


 
