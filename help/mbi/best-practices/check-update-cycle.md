---
title: Vérification de l’état du cycle de mise à jour
description: Découvrez comment vérifier l’état du cycle de mise à jour.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# Progression du cycle de mise à jour

Lorsque vous vous connectez à votre tableau de bord [!DNL Adobe Commerce Intelligence], il existe plusieurs façons de vérifier l’état de votre dernier cycle de mise à jour. Tout dépend du type de [permissions utilisateur](../administrator/user-management/user-management.md) dont vous disposez.

## Pourquoi dois-je vérifier l’état du cycle de mise à jour ?

La vérification du cycle de mise à jour du statut est utile lorsque vous contrôlez les données de votre compte [!DNL Commerce Intelligence]. Si vous voyez [résultats qui ne répondent pas à vos attentes](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), par exemple, les ventes quotidiennes dans [!DNL Commerce Intelligence] ne correspondent pas à ce que vous voyez sur votre plateforme d’e-commerce ou dans vos [[!DNL Google] recettes d’e-commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=fr), vous pouvez vérifier le dernier point de données pour voir si le problème est résolu une fois une mise à jour terminée.

## [!UICONTROL Read-Only] et [!UICONTROL Standard] utilisateurs

Les utilisateurs de `Read-only` peuvent se connecter à leur tableau de bord et voir combien de temps les données ont été mises à jour en pointant sur l’icône en haut à droite de la page. Cela indique le moment où le dernier point de données a été extrait.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] utilisateurs

Les utilisateurs de `Admin` peuvent se connecter au tableau de bord et voir le dernier point de données ci-dessus, ainsi qu’une brève icône d’état de leurs intégrations de compte.

Pour plus de détails, les utilisateurs administrateurs peuvent cliquer sur **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

Cette page présente l’état actuel de la mise à jour et l’heure de la dernière mise à jour terminée.

Si une mise à jour est en cours, un lien s’affiche pour demander une notification par courrier électronique une fois la mise à jour terminée.

Si aucune mise à jour n’est en cours, un lien s’affiche pour forcer le démarrage d’une mise à jour.

>[!NOTE]
>
>Si vous avez des heures d’interruption (heure à laquelle vous ne souhaitez pas que [!DNL Commerce Intelligence] mette à jour vos données), forcer une mise à jour déclenche un cycle de mise à jour qui ne respecte pas les limites de ces heures d’interruption.
