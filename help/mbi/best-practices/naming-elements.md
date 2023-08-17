---
title: Nommer des rapports et des éléments dans Commerce Intelligence
description: Découvrez les bonnes pratiques pour nommer les rapports et les éléments dans [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Nommer des rapports et des éléments

Avant de commencer la création dans [!DNL Adobe Commerce Intelligence], Adobe souhaite partager quelques secrets pour réussir. Il est important de savoir comment créer des mesures, des filtres, etc., mais tout votre travail peut n’avoir aucun impact si vous ne trouvez pas ce dont vous avez besoin ou s’il y a de l’ambiguïté.

## Pourquoi la nomenclature est-elle importante ? {#why}

La manière dont vous nommez vos colonnes, mesures et rapports calculés détermine la facilité avec laquelle les différents utilisateurs peuvent naviguer dans vos [!DNL Commerce Intelligence] compte . Lors de l’attribution de noms à ces fonctionnalités, gardez à l’esprit les trois Cs :

* **CLARITÉ** - Vous pouvez ainsi visualiser en un coup d’oeil ce qu’un rapport affiche, ce qu’une mesure fait, etc.
* **COHÉRENCE** - afin que vous (et l’équipe d’assistance Adobe) puissiez facilement trouver et comprendre les éléments et les rapports de votre compte.
* **CRÉDIBILITÉ** - Pour inspirer et autonomiser d&#39;autres personnes motivées par les données [!DNL Commerce Intelligence] utilisateurs, vous devez inspirer confiance dans la manière dont ils comprennent et utilisent les données !

Lisez la suite pour des conseils avisés sur la nomenclature !

## Bonnes pratiques générales {#general}

### Soyez significatif {#meaningful}

Soyez précis chaque fois que possible ! Par exemple, s’il s’agit du pays, savez-vous s’il s’agit du pays d’expédition ou de facturation ? Est-ce la ville de l&#39;utilisateur ou la ville de l&#39;accord ?

**Mauvais exemple :**
Recettes

C&#39;est vague et ça ne nous dit pas grand chose.

**Bonnes illustrations :**
Recettes (total général de base + frais) Pays d’expédition de l’utilisateur

Ces exemples sont spécifiques, ce qui réduit le risque de confusion.

### Respecter la casse {#capitalize}

[!DNL Adobe] recommande la première lettre, en majuscule, avec le reste des caractères, en minuscules, sauf si le style de majuscule approprié est le nom . Par exemple : **Numéro de commande de l’utilisateur** plutôt que **Numéro de commande de l’utilisateur.**

C&#39;est vraiment une question de préférence, mais la chose à retenir est d&#39;être cohérent avec ce que vous choisissez.

### Cohérence des entités {#entity}

Vous avez probablement déjà une nomenclature en place dans votre société. Veillez à ce que les mesures et dimensions mises en place soient cohérentes avec celles utilisées dans d’autres bases de données et outils. Par exemple :

* Utilisateur par rapport au client par rapport au membre par rapport au compte
* Société ou compte ou organisation
* Enregistrement et création

### Orthographe et grammaire {#spelling}

Assurez-vous de vérifier votre orthographe et n’oubliez pas ces possessifs agités !

## Graphiques {#charts}

Lors du nommage [Graphiques](../tutorials/using-visual-report-builder.md), il est plus utile de suivre cette formule : **(Perspective des données) + (Mesure) + (Période) + (Intervalle temporel)**

**Mauvais exemple :**
Recettes

Cela ne nous dit rien du rapport, ce qui est mauvais.

**Bon exemple :**
Chiffre d’affaires cumulé des 30 derniers jours par mois

Cela nous dit ceci : **what** ce qu&#39;il y a dans le rapport, qui est fantastique.

## Tableaux de bord {#dashboards}

Les tableaux de bord doivent être nommés de manière à représenter par thème les rapports qu’ils contiennent. Si, par exemple, votre tableau de bord contient uniquement des informations relatives aux recettes et aux commandes, pensez à nommer ce dernier par exemple. **Nom de la boutique : recettes et commandes.**

Inversement, si votre tableau de bord est un endroit où vous testez différents rapports, pensez à le nommer. **Sandbox de votre nom** vous savez donc que les rapports contenus dans sont des brouillons.

## Dimensions (colonnes calculées) {#dimensions}

Lors de l’attribution d’un nouveau nom [dimensions](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), il est plus utile de suivre cette formule : **(Entité) + (énième) + (période) + (calcul) + (commentaires)**. Par exemple :

Chiffre d’affaires des 30 premiers jours de l’utilisateur
* Numéro de commande de l’utilisateur
* Numéro de commande de l’utilisateur (en attente d’audit)

## Visionneuses de filtres {#filterset}

[Jeux de filtres](../data-user/reports/ess-manage-data-filters.md) sont généralement nommés de manière à expliquer les informations qu’ils incluent ou excluent. Par exemple, nommer un jeu de filtres **Éléments de commande que nous comptons** permet à n’importe quel utilisateur d’entrer, d’afficher la logique du jeu de filtres et de comprendre les informations de commande qui déterminent ce qui est compté dans l’ensemble de l’entreprise. N’oubliez pas que les jeux de filtres peuvent être appliqués aux colonnes calculées et aux mesures et doivent être faciles à comprendre.

## Mesures {#metrics}

[Mesures](../data-user/reports/ess-manage-data-metrics.md) sont essentiellement des questions auxquelles vous voulez des réponses régulières. Quel était le nombre de commandes au cours du dernier mois ? Quelle est la valeur de durée de vie moyenne de vos clients ? Il est recommandé de nommer les mesures en fonction de la réponse donnée aux utilisateurs. En outre, si la même mesure est filtrée pour un magasin ou un département spécifique, elle doit être étiquetée comme telle. Par exemple :

Client moyen LTV (30 premiers jours) Nom de la boutique - Recettes

Enfin, la même mesure peut parfois être organisée selon différents horodatages, selon la manière dont les utilisateurs la calculent. Si tel est le cas, veillez à inclure l’horodatage dans le nom :

Recettes (expédié\_at) Recettes (créé\_at)

## Remplissage {#wrapup}

La définition précoce des conventions de style et d’appellation vous aide à vous préparer à la réussite de votre [!DNL Commerce Intelligence] compte . Souvenez-vous des trois C : clarté, cohérence et crédibilité.
