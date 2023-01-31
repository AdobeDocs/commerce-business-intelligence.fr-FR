---
title: Création d’ensembles de filtres pour les mesures
description: Découvrez comment créer des visionneuses de filtres enregistrées et les appliquer aux mesures.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Créer des jeux de filtres

Si vous avez plusieurs mesures dans [!DNL MBI] qui doivent être filtrées de la même manière (par exemple, filtrer les commandes de test), vous pouvez créer des visionneuses de filtres enregistrées et les appliquer aux mesures. Cela vous permet de gagner du temps, car vous n’avez pas à ajouter de filtres individuels lors de la création ou de la modification d’une mesure.

Voir notre [vidéo de formation](https://support.magento.com/hc/en-us/articles/360016730151) pour en savoir plus.

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

   Par exemple, si nous ne voulions inclure que les commandes dont le statut est Terminé dans notre `Total number of orders` , nous appliquons un filtre qui exclut toutes les commandes qui n’ont pas d’état = `complete`.

1. Vérifiez la logique de votre filtre et assurez-vous que les parenthèses et les opérateurs sont correctement placés : par exemple, `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Un filtre incorrect est souvent la cause d’incohérences entre les données [!DNL MBI] rapports et les résultats attendus.

1. Enregistrez le `Filter Set`.

Une fois un jeu de filtres enregistré, vous pouvez l’appliquer à toute mesure qui utilise le même tableau. Par exemple, si vous avez créé une `Filter Set` sur le `orders` tableau, vous pouvez l’appliquer à *toute mesure* sur cette table, par exemple `Revenue`.

>[!NOTE]
>
>`Filter Sets` peut également être appliqué aux colonnes calculées dans [!DNL MBI]. Vous pouvez demander l’application d’un ensemble de filtres à une dimension de données créée dans [!DNL MBI] en contactant l’assistance.

## Associé

* [Bonnes pratiques relatives à la segmentation et au filtrage](../../best-practices/segment-filter.md)
