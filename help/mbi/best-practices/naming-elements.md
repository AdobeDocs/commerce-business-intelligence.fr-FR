---
title: Nommer des rapports et des éléments dans Commerce Intelligence
description: Découvrez les bonnes pratiques pour nommer les rapports et les éléments dans  [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Nommer des rapports et des éléments

Avant de commencer à créer dans [!DNL Adobe Commerce Intelligence], Adobe souhaite partager quelques secrets pour réussir. Savoir comment créer des mesures, des filtres, etc. est important, mais tout votre travail peut ne servir à rien si vous ne trouvez pas ce dont vous avez besoin ou s’il y a une ambiguïté.

## Pourquoi la nomenclature est-elle importante ? {#why}

La manière dont vous nommez vos colonnes calculées, mesures et rapports détermine la facilité avec laquelle différents utilisateurs peuvent naviguer dans votre compte [!DNL Commerce Intelligence]. Lorsque vous nommez ces fonctionnalités, gardez à l’esprit les trois C :

* **CLARTÉ** - Vous pouvez ainsi savoir en un coup d’œil ce qu’un rapport affiche, ce que fait une mesure, etc.
* **COHÉRENCE** - De sorte que vous (et l’équipe d’assistance Adobe) puissiez facilement rechercher et comprendre les éléments et les rapports dans votre compte .
* **CRÉDIBILITÉ** - Afin d’inspirer et d’autonomiser les autres utilisateurs de [!DNL Commerce Intelligence] axés sur les données, vous devez leur inculquer la confiance dans leur compréhension et leur utilisation des données !

Lisez la suite pour des conseils de nomenclature éprouvés !

## Bonnes pratiques générales {#general}

### Sois significatif {#meaningful}

Soyez précis dès que possible ! Par exemple, si c&#39;est le pays, savez-vous si c&#39;est le pays d&#39;expédition ou le pays de facturation? S’agit-il de la ville de l’utilisateur ou de la ville de l’accord ?

**Mauvais exemple :**
Chiffre d’affaires

C&#39;est vague et cela ne nous dit pas grand-chose.

**Bons exemples :**
Chiffre d’affaires (total général de base + frais)
Pays d’expédition de l’utilisateur

Ces exemples sont spécifiques, ce qui réduit le risque de confusion.

### Respecter la casse {#capitalize}

[!DNL Adobe] recommande de mettre la première lettre en majuscule et le reste des caractères en minuscules, sauf si le style de nom approprié de la majuscule est appliqué. Par exemple, **Numéro de commande de l’utilisateur** plutôt que **Numéro de commande de l’utilisateur.**

C&#39;est vraiment une question de préférence, mais il ne faut pas oublier d&#39;être cohérent avec ce que l&#39;on choisit.

### Cohérence de l’entité {#entity}

Vous avez probablement déjà une nomenclature en place dans votre entreprise. Veillez à ce que les mesures et dimensions mises en place soient cohérentes avec celles utilisées dans d’autres bases de données et outils. Par exemple :

* Utilisateur ou client ou membre ou compte
* Société ou compte ou organisation
* Enregistrement ou création

### Orthographe et grammaire {#spelling}

Assurez-vous de revérifier votre orthographe et n&#39;oubliez pas ces possessifs ennuyeux !

## Graphiques {#charts}

Lorsque vous nommez des [graphiques](../tutorials/using-visual-report-builder.md), il est très utile de suivre cette formule : **(Perspective de données) + (Mesure) + (Période) + (Intervalle de temps)**

**Mauvais exemple :**
Chiffre d’affaires

Cela ne nous apprend rien sur le rapport, ce qui est mauvais.

**Bon exemple :**
Chiffre d’affaires cumulé sur 30 derniers jours par mois

Cela nous indique **exactement** ce qui se trouve dans le rapport, ce qui est fantastique.

## Tableaux de bord {#dashboards}

Les tableaux de bord doivent être nommés de manière à représenter de manière thématique les rapports qu’ils contiennent. Par exemple, si votre tableau de bord contient uniquement des informations relatives aux recettes et aux commandes, pensez à lui donner un nom du type **Nom de la boutique - Recettes et commandes**.

À l’inverse, si votre tableau de bord vous permet de tester différents rapports, pensez à lui donner le nom **Sandbox de votre nom** pour que vous sachiez que les rapports qu’il contient sont des brouillons.

## Dimensions (colonnes calculées) {#dimensions}

Lorsque vous nommez de nouvelles [dimensions](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), il est très utile d’utiliser la formule suivante : **(Entité) + (Nème) + (intervalle) + (calcul) + (commentaires)**. Par exemple :

Chiffre d’affaires de 30 premiers jours de l’utilisateur
* Numéro de commande de l&#39;utilisateur
* Numéro de commande de l&#39;utilisateur (en attente d&#39;audit)

## Jeux de filtres {#filterset}

Les [ensembles de filtres](../data-user/reports/ess-manage-data-filters.md) sont généralement nommés de manière à expliquer les informations qu’ils incluent ou excluent. Par exemple, le fait de nommer un jeu de filtres **éléments de commande que nous comptons** permet à n’importe quel utilisateur d’y accéder, de voir la logique du jeu de filtres et de comprendre quelles informations de commande déterminent ce qui est comptabilisé dans l’ensemble de l’entreprise. N’oubliez pas que les jeux de filtres peuvent être appliqués à la fois aux colonnes calculées et aux mesures. Ils doivent être faciles à comprendre.

## Mesures {#metrics}

[Mesures](../data-user/reports/ess-manage-data-metrics.md) sont essentiellement des questions auxquelles vous souhaitez obtenir régulièrement des réponses. Quel a été le nombre de commandes au cours du dernier mois ? Quelle est la valeur moyenne sur toute la durée de vie de vos clients ? Il est recommandé de nommer les mesures en fonction de la réponse qu’elles donnent aux utilisateurs. En outre, si la même mesure est filtrée pour un magasin ou un service spécifique, elle doit être étiquetée comme telle. Par exemple :

LTV client moyen (30 premiers jours)
Nom de la boutique - Chiffre d’affaires

Enfin, une même mesure peut parfois être organisée par horodatages différents, selon la manière dont les utilisateurs individuels la calculent. Si tel est le cas, veillez à inclure la date et l’heure dans le nom :

Chiffre d’affaires (expédié\_at)
Chiffre d’affaires (créé\_at)

## Conclusion {#wrapup}

L’établissement précoce des conventions de style et de dénomination vous aide à configurer le succès de votre compte [!DNL Commerce Intelligence]. Souvenez-vous des trois C : clarté, cohérence et crédibilité.
