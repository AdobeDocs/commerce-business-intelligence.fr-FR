---
title: Création de jeux de filtres pour les mesures
description: Découvrez comment créer des jeux de filtres enregistrés et les appliquer aux mesures.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Création de jeux de filtres

Si plusieurs mesures dans [!DNL Commerce Intelligence] doivent être filtrées de la même manière (en filtrant les ordres de test, par exemple), vous pouvez créer des ensembles de filtres enregistrés et les appliquer aux mesures. Cela vous permet de gagner du temps, car vous n’avez pas à ajouter de filtres individuels lors de la création ou de la modification d’une mesure.

Voir la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=fr) pour plus d’informations.

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md).

1. Cliquez sur **[!DNL Manage Data** > **Filter Sets]** dans la barre latérale.

   ![](../../assets/create-filter-sets.png)

1. Cliquez sur **[!UICONTROL Add Filter Set]** en haut de la page.

1. Sélectionnez le tableau contenant les mesures à filtrer.

   Par exemple, si vous souhaitez filtrer votre mesure `Total number of orders` et qu’elle est créée sur le tableau `orders`, sélectionnez ce tableau.

1. Nommez le `Filter Set` .

1. Ajoutez tous les filtres pertinents.

   Par exemple, si vous souhaitez uniquement inclure les commandes dont le statut est défini sur terminé dans votre mesure de `Total number of orders`, appliquez un filtre qui exclut toutes les commandes dont le statut n’est pas défini sur = `complete`.

1. Vérifiez votre logique de filtre et que les parenthèses et les opérateurs sont correctement placés : par exemple, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtre incorrect est souvent la cause des incohérences de données entre les rapports [!DNL Commerce Intelligence] et les résultats attendus.

1. Enregistrez le `Filter Set`.

Une fois qu’un jeu de filtres est enregistré, vous pouvez l’appliquer à n’importe quelle mesure utilisant le même tableau. Par exemple, si vous avez créé une `Filter Set` sur la table `orders`, vous pouvez l’appliquer à *toutes les mesures* créées sur cette table, comme `Revenue`.

>[!NOTE]
>
>`Filter Sets` peut également être appliqué aux colonnes calculées dans [!DNL Commerce Intelligence]. Vous pouvez demander à appliquer un jeu de filtres à une dimension de données créée dans [!DNL Commerce Intelligence] via en contactant l’assistance.

## Connexe

* [Bonnes pratiques relatives à la segmentation et au filtrage](../../best-practices/segment-filter.md)
