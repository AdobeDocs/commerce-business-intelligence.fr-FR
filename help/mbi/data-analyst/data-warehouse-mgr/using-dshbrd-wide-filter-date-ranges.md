---
title: Filtrage à l’échelle du tableau de bord
description: Découvrez comment apporter des modifications en masse à tous les rapports d’un tableau de bord spécifique.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Filtrage à l’échelle du tableau de bord

Le filtrage à l’échelle du tableau de bord vous permet d’apporter des modifications en masse à tous les rapports d’un tableau de bord spécifique. Vous pouvez afficher rapidement la même analyse sur différentes périodes ou pour différents magasins. Vous pouvez facilement comparer les performances d’une année, d’un mois ou d’une semaine précédents par magasin. Vous pouvez mettre à jour un tableau de bord entier pour l’adapter à une nouvelle campagne lancée.

## Filtres de date

Pour modifier la période ou l’intervalle des rapports sur un tableau de bord, cliquez sur l’icône de calendrier dans le coin supérieur droit (![calendrier](../../assets/calendar-button.png)).

Vous pouvez choisir d&#39;afficher les données à l&#39;aide d&#39;un `Fixed Date Range` ou de plusieurs `Moving Date Ranges` précalculés :

![déplacement de plages de dates](../../assets/moving_date_ranges.png)

Les options de plage de déplacement `Last Full...` représentent la plage la plus récemment entièrement terminée, tandis que `This...` est la plage actuelle en cours. Par exemple, si nous sommes en juin, le `Last Full Month` est _1er mai - 31 mai_, tandis que `This Month` est _1er juin - Maintenant_.

Ou créez votre propre `Custom Moving Range`\ :

![plage de déplacement personnalisée](../../assets/custom-moving-range.png)

Choisissez également de modifier l’intervalle. La sélection du bouton par défaut (![valeur par défaut de l’intervalle de temps](../../assets/time_interval_default.png)) signifie que seule la plage de dates change :

![intervalle de temps](../../assets/time_interval.png)

Pour restaurer tous les rapports sur leur période et leur intervalle initiaux, cliquez sur **[!UICONTROL Restore Defaults]** ou sur **[!UICONTROL Cancel]**.

Lorsque vous spécifiez un filtre de date pour un tableau de bord, celui-ci s’applique uniquement à ce tableau de bord. Elle n’est pas appliquée lorsque vous accédez à d’autres tableaux de bord.

>[!NOTE]
>
>Actuellement, `Cohort Reports` et `SQL Reports` ne sont pas inclus lors de l’application des modifications au niveau du tableau de bord.

## Filtres de magasin

Pour analyser les performances d’un magasin spécifique, cliquez sur l’icône de magasins dans le coin supérieur droit (![Filtre de magasin](../../assets/store-filter.png)). Par défaut, `Store Filter` est défini sur `All Stores`, ce qui affiche les données de toutes les [ vues de magasin ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html?lang=fr) disponibles dans votre site Commerce.

>[!NOTE]
>
>Un filtre de magasin est activé ou désactivé pour un compte [!DNL Commerce Intelligence] entier. Si un tableau de bord contient des rapports qui ne sont pas affectés par le filtre (tels que des rapports qui ne sont construits sur aucune donnée [!DNL Adobe Commerce]), ces rapports ne sont pas mis à jour lorsque le filtre de magasin est appliqué. Vous pouvez [contacter l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) si vous pensez qu’un rapport doit être mis à jour en fonction de la sélection du magasin ou si vous pensez que le filtre de la boutique de comptes est désactivé par erreur.

Lorsque vous sélectionnez un magasin dans le `Store Filter`, le filtre conserve votre sélection lorsque vous naviguez entre les tableaux de bord. Le fait de conserver votre sélection vous permet d’afficher partout les données de votre magasin sélectionné jusqu’à ce que vous sélectionniez `All Stores`.

## Filtres des tableaux de bord partagés

Pour les tableaux de bord partagés, si un utilisateur configure le filtre de date, les autres utilisateurs ayant accès au tableau de bord voient le même filtre appliqué. Toutefois, le filtre de magasin ne s’applique pas dans ce cas. Si le propriétaire du tableau de bord configure le filtre de magasin et partage le tableau de bord, le filtre de magasin configuré n’est pas conservé pour un autre utilisateur. Un utilisateur doit disposer de l’accès [ à un tableau de bord pour ajuster les filtres du tableau de bord.](../../data-user/dashboards/share-dashboard-with-users.md)
