---
title: Création de graphiques Google Analytics
description: Découvrez comment créer des graphiques à partir de vos données Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Créer [!DNL Google Analytics] graphiques

(avec l’aide de la syntaxe regex)

Après avoir connecté votre [[!DNL Google Analytics] compte](../../data-analyst/importing-data/integrations/google-analytics.md), vous pouvez créer des graphiques avec vos données [!DNL Google Analytics].

## Créer [!DNL Google Analytics] graphiques

1. Cliquez sur **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Lors de la sélection d’une mesure dans le `Chart Builder`, faites défiler la liste jusqu’au bas de la liste pour trouver une section contenant vos profils [!DNL Google Analytics]. Une deuxième liste déroulante de mesures s’affiche. Vous pouvez y choisir la mesure que vous souhaitez analyser.

1. Après avoir choisi la mesure, vous pouvez poursuivre avec ce graphique comme s’il s’agissait de n’importe quel autre graphique en sélectionnant les `time period`, `interval` et les données `perspectives` que vous souhaitez voir.

1. La différence majeure ici est que `√` utilise des expressions régulières pour les filtres. Une expression régulière (expression régulière pour abréviation) est une chaîne de texte spéciale pour décrire un modèle de recherche. Voir des exemples de syntaxe regex dans le [[!DNL Google] guide sur les expressions régulières Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Les seuls caractères spéciaux qui doivent être précédés d’une séquence d’échappement à l’aide du caractère \ sont les métacaractères ci-dessous :

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
