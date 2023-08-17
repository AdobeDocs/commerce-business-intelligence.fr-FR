---
title: Création d’ensembles de filtres pour les mesures
description: Découvrez comment créer des visionneuses de filtres enregistrées et les appliquer aux mesures.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Créer des jeux de filtres

Si vous avez plusieurs mesures dans [!DNL Commerce Intelligence] qui doivent être filtrées de la même manière (par exemple, filtrer les commandes de test), vous pouvez créer des visionneuses de filtres enregistrées et les appliquer aux mesures. Cela vous permet de gagner du temps, car vous n’avez pas à ajouter de filtres individuels lors de la création ou de la modification d’une mesure.

Voir [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) pour plus d’informations.

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

1. Cliquez sur **[!DNL Manage Data** > **Filter Sets]** dans la barre latérale.

   ![](../../assets/create-filter-sets.png)

1. Cliquez sur **[!UICONTROL Add Filter Set]** en haut de la page.

1. Sélectionnez le tableau contenant les mesures à filtrer.

   Par exemple, si vous souhaitez filtrer votre `Total number of orders` et repose sur la variable `orders` sélectionnez ce tableau.

1. Attribuez un nom au `Filter Set`.

1. Ajoutez tous les filtres appropriés.

   Par exemple, si vous souhaitez uniquement inclure des commandes dont l’état est Terminé dans votre `Total number of orders` , vous appliquez un filtre qui exclut toutes les commandes qui n’ont pas d’état = `complete`.

1. Vérifiez la logique de votre filtre et que les parenthèses et les opérateurs sont correctement placés : par exemple, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtre incorrect est souvent la cause d’incohérences entre les données [!DNL Commerce Intelligence] rapports et les résultats attendus.

1. Enregistrez le `Filter Set`.

Une fois un jeu de filtres enregistré, vous pouvez l’appliquer à toute mesure qui utilise le même tableau. Si vous avez créé une `Filter Set` sur le `orders` tableau, vous pouvez l’appliquer à *toute mesure* sur cette table, par exemple `Revenue`.

>[!NOTE]
>
>`Filter Sets` peut également être appliqué aux colonnes calculées dans [!DNL Commerce Intelligence]. Vous pouvez demander l’application d’un ensemble de filtres à une dimension de données créée dans [!DNL Commerce Intelligence] en contactant l’assistance.

## Associé

* [Bonnes pratiques relatives à la segmentation et au filtrage](../../best-practices/segment-filter.md)
