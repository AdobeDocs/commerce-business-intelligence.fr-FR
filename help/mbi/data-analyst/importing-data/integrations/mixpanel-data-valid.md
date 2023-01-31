---
title: Validation des données dans Mixpanel
description: Découvrez comment confirmer que nous avons synchronisé toutes les mêmes données disponibles directement dans Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Validation des données dans `Mixpanel`

When [!DNL MBI] se connecte d’abord à votre [!DNL Mixpanel] , votre gestionnaire de compte ou Analyste peut vous demander de fournir des exportations de données depuis Mixpanel à des fins de validation. Cela nous permet de confirmer que nous avons synchronisé toutes les mêmes données que celles disponibles directement dans [!DNL Mixpanel].

## Processus d’exportation des données : `Events`

1. Visitez votre `Segmentation` section et affichage `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Sélectionner `Past 96 Hours` pour la période

   ![](../../../assets/past-96-hours.png)

1. Accédez à l’angle inférieur droit du rapport et exportez un `.csv` fichier :

   ![](../../../assets/export-csv-mixpanel.png)

1. Envoyez la variable `.csv` au gestionnaire de compte ou à l’analyste avec lequel vous travaillez sur ce processus de validation.
