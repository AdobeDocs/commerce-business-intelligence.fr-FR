---
title: Création d’ensembles de filtres pour les mesures
description: Découvrez comment créer des visionneuses de filtres enregistrées et les appliquer aux mesures.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Créer des jeux de filtres

Si plusieurs mesures de [!DNL Commerce Intelligence] doivent être filtrées de la même manière (par exemple, filtrer les commandes de test), vous pouvez créer des visionneuses de filtres enregistrées et les appliquer aux mesures. Cela vous permet de gagner du temps, car vous n’avez pas à ajouter de filtres individuels lors de la création ou de la modification d’une mesure.

Pour plus d’informations, consultez la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=fr) .

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../administrator/user-management/user-management.md).

1. Cliquez sur **[!DNL Manage Data** > **Filter Sets]** dans la barre latérale.

   ![](../../assets/create-filter-sets.png)

1. Cliquez sur **[!UICONTROL Add Filter Set]** en haut de la page.

1. Sélectionnez le tableau contenant les mesures à filtrer.

   Par exemple, si vous souhaitez filtrer votre mesure `Total number of orders` créée sur la table `orders`, sélectionnez cette table.

1. Nommez le `Filter Set`.

1. Ajoutez tous les filtres appropriés.

   Par exemple, si vous souhaitez uniquement inclure des commandes dont l’état est terminé dans votre mesure `Total number of orders`, vous appliquez un filtre qui exclut toutes les commandes qui n’ont pas d’état = `complete`.

1. Vérifiez la logique de votre filtre et assurez-vous que les parenthèses et les opérateurs sont correctement placés : par exemple, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtre incorrect est souvent la cause d’incohérences de données entre les rapports [!DNL Commerce Intelligence] et les résultats attendus.

1. Enregistrez le `Filter Set`.

Une fois un jeu de filtres enregistré, vous pouvez l’appliquer à toute mesure qui utilise le même tableau. Par exemple, si vous avez créé un `Filter Set` sur la table `orders`, vous pouvez l’appliquer à *toute mesure* créée sur cette table, par exemple `Revenue`.

>[!NOTE]
>
>`Filter Sets` peut également être appliqué aux colonnes calculées dans [!DNL Commerce Intelligence]. Vous pouvez demander d’appliquer un ensemble de filtres à une dimension de données créée dans [!DNL Commerce Intelligence] en contactant l’assistance technique.

## Associé

* [Bonnes pratiques relatives à la segmentation et au filtrage](../../best-practices/segment-filter.md)
