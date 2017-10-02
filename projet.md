---
title: Modalités du projet tutoré 
subtitle: Planning et cahier des charges
layout: tutorial
---

## Sujet

Vous devez réaliser le site Web d'une entreprise fictive avec un **unique**
produit / logiciel révolutionnaire fictif.  La taille des groupes est de 4
personnes au plus. Si vous êtes moins, nous attendrons la même quantité de
travail. Si vous êtes plus, vous aurez une petite pénalité.

<!-- Pas un magasin avec plusieurs produits ! -->

### Emploi du temps prévisionnel :

<!-- 1. Semaine du 02 Octobre 2017 : -->
<!--    * [TD 4 -- Les Formulaires](tutorials/tutorial4.html) (~2h) -->
<!-- 	 ([English version](tutorials/tutorial4-en.html))  -->
<!--    * puis projet (1h) -->
<!-- 1. Semaine du 09 Octobre 2017 -- -->
<!--    * Entamer [TD 5 -- Responsive Design](tutorials/tutorial5.html) (~2h) -->
<!--    ([English version](tutorials/tutorial5-en.html))  -->
<!--    * puis projet (1h) -->
<!-- 1. Semaine du 16 Octobre 2017 -- -->
<!--    * Finir le [TD 5 -- Responsive Design](tutorials/tutorial5.html) (max 2h) -->
<!--    ([English version](tutorials/tutorial5-en.html))  -->
<!--    * puis projet (1h) -->
<!-- 1. Semaine du 06 Novembre 2017 -- projet (3h) -->
<!-- 1. Semaine du 13 Novembre 2017 -- projet (3h) -->
<!-- 1. Semaine du 08 Janvier 2018 -- Soutenances de projet -->

1. Semaine du 25 Septembre 2017 : TD 4 -- Les Formulaires puis lancement du projet
1. Semaine du 02 Octobre 2017 : Projet
1. Semaine du 09 Octobre 2017 : Début TD 5 -- Responsive Design (~2h) puis projet (1h)
1. Semaine du 16 Octobre 2017 : Fin TD 5 -- Responsive Design puis projet (1h)
1. Semaine du 23 Octobre 2017 : Cours d'Infographie
1. Semaine du 06 Novembre 2017 -- projet (3h)
1. Semaine du 13 Novembre 2017 -- projet (3h)
1. Semaines du 20 & 27 Novembre et 04 & 11 Décembre : Ergonomie

**Examen & soutenances :**

1. Semaine du 18 Décembre -- Examen écrit (2h max)
1. Semaine du 8 Janvier -- Soutenances projet tutoré (20 min/groupe)

### Architecture minimum de votre site :

Il y aura un menu de navigation avec sous-menus commun à toutes vos pages. Voici
une liste minimale de pages que vous devez avoir :

1. **Produit :** Une page qui présente le produit avec punch line, photo,
et le logo de l’entreprise (créé tel que vu dans le TD d’infographie) ;

1. **Contact :** Une page formulaire ”contactez nous”, avec

   1. les informations sur le demandeur (nom, prénom, adresse email, code postal, champs de sélection du pays),
   1. une question "vous avez entendu parlé de nous via ?” avec plusieurs choix possibles <!-- checkbox -->
   1. un champ "date à laquelle vous souhaitez être recontacté" 
   1. un champ texte libre de plusieurs lignes d'expression libre

   Pour chacun des champs, un exemple sera donné, une vérification du format sera
   faite à l’aide des types prédéfinis en HTML5 (l’utilisation d’expressions régulières
   est optionnelle) ;

1. **Équipe :** Une page qui présente toute la team du directeur au développeur
avec photo et courte biographie pour chacun. 

1. **Presse :** Une page qui donne les contacts du responsable presse ainsi qu'une liste de communiqués de presse ;

1. **Nous rejoindre :** Une page qui renvoie sur différentes fiches d'offres de
postes de l'entreprise. Chaque offre de poste aura son sous menu déroulant du type :

   1. Métier 1
   1. Métier 2
   1. Métier 3

1. **Une foire aux questions (FAQ) :** Une liste de questions en début de page qui pointe sur les différentes 
questions et réponses plus bas dans la page (utilisation des ancres).


<!-- Équipe : Cette page sera responsive: présentation en grille si grande page ou liste si visualisation sur mobile. -->
<!-- - une page simple de site "under construction"/"coming soon", -->

### Consignes générales

1. le site sera responsive. Au minimum le menu s'adaptera à la taille de la
   page. De plus la page **Équipe** doit être responsive : la présentation se
   fera en grille sur une grande page ou en liste quand la page est trop petite.
1. le site sera encodé en UTF8.
1. les codes CSS et HTML seront correctement indentés. 
1. Le texte LOREM IPSUM est autorisé. Ne perdez pas trop de temps à inventer du
    contenu à votre site. <!-- under construction, ne pas passer trop de temps
    sur le contenu -->
1. le site doit être valide HTML5 et CSS3, et bien structuré à l’aide des
   balises de structuration : header, nav, main, article, aside, footer, div.
1. l’utilisation de framework tels que bootstrap, foundation, etc. n’est pas autorisée. 
1. la liste des display autorisés est : block, inline, flex et none.
1. l’utilisation des float ou des tableaux n’est pas autorisée pour la mise en
   page, c'est-à-dire par exemple pour mettre une colonne à côté d'une autre
   ... Par contre, on peut bien sûr s'en servir pour son usage historique :
   entourer une image de texte.
1. le visuel du site (charte graphique) doit être cohérent sur toutes les pages du site. 
<!-- 1. Un seul fichier CSS pour toutes les pages. -->
1. Le CSS devra être synthétique: Par exemple, il devra privilégier
   l’utilisation des classes en CSS à l’usage d’identifiant et de règles qui ne
   s’appliquent qu’à un seul élément.
1. L’utilisation de CSS dans le style inline est interdit. 
1. Il est très facile de perdre des heures sur un petit détail en CSS. Il est
   important d'avoir d'abord un site grossièrement fini plutôt qu'une section de
   page parfaite.

## Modalités de contrôle

Le projet compte pour deux modules ; en effet le projet tutoré de S1 est adossé
à notre cours de "Conception documentaire". Pour information, il est prévu 60h
de travail personnel sur ce projet dans les programmes officiels.

Module 1105 - Conception de documents | Module 1106 - Projet tutoré
Coefficient 2,5                       | Coefficient 1,5
--------------------------------------|- --------------------------
Ergonomie (30%)                       | Projet (100%)
Examen écrit (40%)                    |
Projet (30%)                          | 
{:.controle}

<style scoped>
table.controle td, table.controle th {
  border:2px solid black;
}

table.controle th {
background-color:#EEE;
}

table.controle {
  margin:auto;
}

</style>

### Détails de la soutenance

La soutenance sera composée d'une série questions sur votre projet (Qu'est-ce
qui a été implémenté ? Qui a fait quoi ? Expliquez ce qui a été codé. ) et
possiblement des questions de cours à chacun des membres de votre groupe. Il n’y
a **pas** de rapport à écrire, ni de présentation à préparer.

Voici
[la grille de notation](https://docs.google.com/spreadsheets/d/1C_zVXJytwIJ9EVgveuuzpiyS7qjHLG0_BmbPLpxxdsk/edit?usp=sharing)
qui sera utilisée pour vous noter et qui est basée sur les compétences acquises
en TP. Cette grille **peut évoluer** jusqu'à la soutenance.

Le site Web devra être mis en place dans le dossier existant **public_html** de
l'un des membres de l'équipe. Un fichier compressé **sources.zip** contenant les
sources du site Web devra aussi être placé dans le dossier **public_html**.

<!-- Pour mémoire, voici -->
<!-- [les groupes de projet tutoré](https://docs.google.com/spreadsheets/d/1MPLEN5XZsSCNCMt_4FgzTS8SuXYp2lO2VmAEro4BCpo/edit) -->
<!-- et leurs produits vendus. -->

### Détails sur l'examen écrit

L'examen écrit ne demandera quasiment pas d'écrire de code HTML/CSS. L'examen
sera concentré sur le contrôle de votre compréhension de codes HTML/CSS et des
techniques employées dans les TDs : Pourquoi a-t-on vu telle notion ? Pour
répondre à quel problème ? Comment marche la solution ? ...



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

