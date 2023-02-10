---
title: Filtrage à l’échelle du tableau de bord
description: Découvrez comment apporter des modifications en masse à tous les rapports d’un tableau de bord spécifique.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Filtrage à l’échelle du tableau de bord

Le filtrage à l’échelle du tableau de bord vous permet d’apporter des modifications en masse à tous les rapports d’un tableau de bord spécifique. Vous pouvez afficher rapidement la même analyse sur différentes périodes ou pour différents magasins. Vous pouvez facilement comparer les performances d’une année, d’un mois ou d’une semaine précédents par magasin. De plus, vous pouvez mettre à jour un tableau de bord entier pour l’adapter à une nouvelle campagne lancée.

## Filtres de date

Pour modifier la période ou l’intervalle des rapports sur un tableau de bord, cliquez sur l’icône Calendrier dans le coin supérieur droit (![calendar](../../assets/calendar-button.png)).

Vous pouvez choisir d’afficher les données à l’aide d’une `Fixed Date Range` ou une variété de `Moving Date Ranges`:

![déplacement de périodes](../../assets/moving_date_ranges.png)

Le `Last Full...` les options de plage de déplacement représentent la plage la plus récemment terminée, tandis que `This...` sera la plage en cours actuelle. Si, par exemple, nous sommes actuellement en juin, la variable `Last Full Month` is _1er mai au 31 mai_, tandis que `This Month` is _1er juin - Maintenant_.

Vous pouvez également créer les vôtres `Custom Moving Range`\:

![portée personnalisée](../../assets/custom-moving-range.png)

Choisissez également de modifier l’intervalle. Sélection du bouton par défaut (![valeur par défaut de l’intervalle de temps](../../assets/time_interval_default.png)) signifie que seule la période sera modifiée :

![intervalle](../../assets/time_interval.png)

Pour rétablir tous les rapports sur leur période et leur intervalle initiaux, cliquez sur **[!UICONTROL Restore Defaults]** ou cliquez sur **[!UICONTROL Cancel]**.

Lorsque vous spécifiez un filtre de date pour un tableau de bord, celui-ci s’applique uniquement à ce tableau de bord. Elle n’est pas appliquée lorsque vous accédez à d’autres tableaux de bord.

>[!NOTE]
>
>À l’heure actuelle, `Cohort Reports` et `SQL Reports` ne sont pas inclus lors de l’application des modifications au niveau du tableau de bord.

## Filtres de magasin

Pour analyser les performances d’un magasin spécifique, cliquez sur l’icône de magasins dans le coin supérieur droit (![Filtre de magasin](../../assets/store-filter.png)). Par défaut, `Store Filter` est défini sur `All Stores`, qui affiche les données de tous les [vues du magasin](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) disponible sur votre site Commerce.

>[!NOTE]
>
>Un filtre de magasin est activé ou désactivé pour l’ensemble d’un [!DNL MBI] compte . Si un tableau de bord contient des rapports qui ne sont pas affectés par le filtre, tels que des rapports qui ne sont créés sur aucune donnée de commerce, ces rapports ne sont pas mis à jour lorsque le filtre de magasin est appliqué. Vous pouvez [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) si vous pensez qu’un rapport doit être mis à jour en fonction de la sélection du magasin ou si vous pensez que votre filtre de magasin de comptes est désactivé par erreur.

Lorsque vous sélectionnez un magasin dans la variable `Store Filter`, le filtre conserve votre sélection lorsque vous naviguez entre les tableaux de bord. Le fait de conserver votre sélection vous permet d’afficher partout les données de votre magasin sélectionné jusqu’à ce que vous sélectionniez `All Stores`.

## Filtres des tableaux de bord partagés

Pour les tableaux de bord partagés, si un utilisateur configure le filtre de date, les autres utilisateurs ayant accès au tableau de bord verront le même filtre appliqué. Toutefois, le filtre de magasin ne s’applique pas dans ce cas. Si le propriétaire du tableau de bord configure le filtre de magasin et partage le tableau de bord, le filtre de magasin configuré ne sera pas conservé pour un autre utilisateur. Un utilisateur doit avoir [modifier l’accès](../../data-user/dashboards/share-dashboard-with-users.md) à un tableau de bord afin d’ajuster les filtres du tableau de bord.
