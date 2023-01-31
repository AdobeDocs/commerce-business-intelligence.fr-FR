---
title: Création de graphiques Google Analytics
description: Découvrez comment créer des graphiques à partir de vos données Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Créer [!DNL Google Analytics] Graphiques

(avec l’aide de la syntaxe regex)

Une fois que vous avez connecté votre [[!DNL Google Analytics] account](../../data-analyst/importing-data/integrations/google-analytics.md), vous pouvez créer des graphiques à partir de vos [!DNL Google Analytics] data.

## Créer [!DNL Google Analytics] Graphiques

1. Cliquez sur **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Lorsque vous sélectionnez une mesure dans la variable `Chart Builder`, faites défiler la liste jusqu’au bas de la liste pour trouver une section comprenant votre [!DNL Google Analytics] Profils. Une deuxième liste déroulante de mesures s’affiche. Vous pouvez y choisir la mesure que vous souhaitez analyser.

1. Après avoir choisi la mesure, vous pouvez poursuivre l’utilisation de ce graphique comme s’il s’agissait d’un autre graphique en sélectionnant l’option `time period`, `interval`, et données `perspectives` que vous aimeriez voir.

1. La seule différence majeure ici est que `√` utilise des expressions régulières pour les filtres. Une expression régulière (expression régulière pour abréviation) est une chaîne de texte spéciale pour décrire un modèle de recherche. Voir des exemples de syntaxe d’expression régulière dans la section [[!DNL Google] Guide sur les expressions régulières Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Les seuls caractères spéciaux qui doivent être précédés d’une séquence d’échappement à l’aide du caractère \ sont les métacaractères ci-dessous :

|  |  |  |  |  |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style=&quot;table-layout:auto&quot;}
