---
title: Création de graphiques Google Analytics
description: Découvrez comment créer des graphiques à partir de vos données Google Analytics.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 160
ht-degree: 0%

---

# Créer des graphiques [!DNL Google Analytics]

(avec l’aide de la syntaxe regex)

Après avoir connecté votre [[!DNL Google Analytics] compte](../../data-analyst/importing-data/integrations/google-analytics.md), vous pouvez créer des graphiques avec vos données [!DNL Google Analytics].

## Créer Des Graphiques [!DNL Google Analytics]

1. Cliquez sur **[!UICONTROL Add Chart** > **Create New Chart]**.

1. Lors de la sélection d’une mesure dans la `Chart Builder`, faites défiler la liste vers le bas pour trouver une section comprenant vos profils de [!DNL Google Analytics]. Une deuxième liste déroulante de mesures s’affiche. Vous pouvez y choisir la mesure à analyser.

1. Après avoir choisi la mesure, vous pouvez continuer à utiliser ce graphique comme s’il s’agissait de n’importe quel autre graphique en sélectionnant les `time period` de `interval`, de `perspectives` et de données que vous souhaitez afficher.

1. La principale différence ici est que `√` utilise des expressions régulières pour les filtres. Une expression régulière (regex pour abréger) est une chaîne de texte spéciale pour décrire un modèle de recherche. Consultez des exemples de syntaxe RegEx dans le [[!DNL Google] guide sur les expressions régulières Analytics](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>Les seuls caractères spéciaux qui doivent être placés dans une séquence d’échappement à l’aide du caractère \ sont les métacaractères ci-dessous :

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
