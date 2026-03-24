---
title: Création de jeux de filtres pour les mesures
description: Découvrez comment créer des jeux de filtres enregistrés et les appliquer aux mesures.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Y3SA-ypB62c0mwZ6uqAOQUyrISc5Tu8yqClrGwXspoU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 0%

---

# Création de jeux de filtres

Si plusieurs mesures dans [!DNL Commerce Intelligence] doivent être filtrées de la même manière (en filtrant les ordres de test, par exemple), vous pouvez créer des ensembles de filtres enregistrés et les appliquer aux mesures. Cela vous permet de gagner du temps, car vous n’avez pas à ajouter de filtres individuels lors de la création ou de la modification d’une mesure.

Voir la [vidéo de formation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) pour plus d’informations.

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../administrator/user-management/user-management.md).

1. Cliquez sur **[!DNL Manage Data** > **Filter Sets]** dans la barre latérale.

   ![Interface de création de jeux de filtres avec l’option Ajouter un jeu de filtres](../../assets/create-filter-sets.png)

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
