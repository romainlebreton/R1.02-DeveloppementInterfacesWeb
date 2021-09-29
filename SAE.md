---
title: Modalités du site de la SAÉ 1.6
subtitle: Planning et cahier des charges
layout: tutorial
---

## Sujet

Vous devez réaliser le site Web présentant votre controverse sociotechnique de la [SAÉ 1.6]({{site.baseurl}}/assets/Sae1-6.pdf).
Pour rendre ce site web accessible vous utiliserez le dossier public_html de l'un des membres du groupes comme vu en TD. 
La date limite de rendu est le lundi 29/11 à 23h59.

### Le contenu de votre site :

Il y aura un menu de navigation avec sous-menus commun à toutes vos pages 
(on peut par exemple imaginer une ligne du menu dédiée à chaque page avec au moins un sous-menu déroulant qui permet d'accéder directement à différents points d'ancrage de la page). 
Comme vu en TD, ce menu devra être responsive et donc être remplacé par un menu burger équivalent si la zone d'affichage est petite. 
Voici une liste minimale de pages que vous devez avoir :

1. Une page d'accueil introduisant le sujet.
1. Au moins deux autres pages regroupants chacunes certains aspects du sujets 
(ça peut être 3 ou 4 pages si cela permet un découpage plus pertinent pour couvrir les différents aspects à traiter).
1. **Contact :** Une page formulaire ”contactez nous”, avec

   1. les informations sur le demandeur (nom, prénom, adresse email, code postal, champs de sélection du pays),
   1. une question "vous avez entendu parlé de nous via ?” avec plusieurs choix possibles <!-- checkbox -->
   1. un champ "date à laquelle vous souhaitez être recontacté" 
   1. un champ texte libre de plusieurs lignes d'expression libre

   Pour chacun des champs, un exemple sera donné, une vérification du format sera
   faite à l’aide des types prédéfinis en HTML5 (l’utilisation d’expressions régulières
   est optionnelle).



### Consignes générales

Vous devrez mettre en application les techniques que vous avez apprises lors des TDs. Voici donc les critères techniques sur lesquels vous serez
notés:
<!-- **[les critères techniques sur lesquels vous serez notés:](https://docs.google.com/spreadsheets/d/1CHQ6imNxRFWHETmVZbRyPIxg8hV8nVrNcHthe1TGHxg/edit?usp=sharing)** -->


1. les codes CSS et HTML seront lisibles et correctement indentés. L’utilisation
   de CSS de style inline est interdit.
1. le visuel du site (charte graphique) doit être cohérent sur toutes les pages du site.
1. l’utilisation de framework tels que bootstrap, foundation, etc. n’est pas autorisée. 
1. l’utilisation des *float* ou des tableaux **n’est pas autorisée pour la mise
   en page**, c'est-à-dire par exemple pour mettre une colonne à côté d'une
   autre ... Par contre, on peut bien sûr se servir de *float* pour son usage
   historique : entourer une image de texte.
1. l’utilisation des `<br\>` **n’est pas autorisée pour la mise en page**. Si
   vous voulez sauter à la ligne dans un texte, cela correspond sûrement à un
   paragraphe `<p>`.  Si vous voulez espacer des blocs, il faut mettre des
   marges en bas.
1. le site sera responsive. Au minimum le menu s'adaptera à la taille de la
   page.

Quelques points suplémentaires que nous vérifierons pour l'évaluation:

1. Valider vos fichiers HTML et CSS avec les validateurs HTML5 et CSS3 déja utilisés en TD.
1. Déclarer l'encodage UTF8 des caractères.
1. Plusieurs fontes importés avec fallback.
1. Maitrise des différentes propriétés de flex.
1. Variétés des balises utilisées.

<!-- ————————————— -->
<!-- Pour nous plus tard:  éléments de la grille de notation: -->
<!-- ————————————— -->

<!-- Critères: -->

<!-- sélecteurs CSS : sélecteurs de base, combinaison et règles de priorité -->
<!-- propriétés CSS classiques (couleur, taille, fontes, text-align  -->
<!-- modèle de boite : padding, border, margin avec auto -->
<!-- float simple (image dans un texte) et clear -->
<!-- position : static, relative, absolute, fixed -->
<!-- display : -->


<!-- Notes: -->
<!-- Installer le site à la racine du public_html de l'un des membres -> prévoir un google doc -->
<!-- twitter : juste image et lien -->

<!-- Menu de navigation -->
<!-- keywords avec boite qui s'ouvre quand on passe la souris dessus -->
<!-- Pas d'animation CSS – Pas de framework CSS (bootstrap, fundation) -->

 
