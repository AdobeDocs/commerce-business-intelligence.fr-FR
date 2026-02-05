---
title: Vérification du statut du cycle de mise à jour
description: Découvrez comment vérifier l’état du cycle de mise à jour.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: d683f1362d87eee16c41ba9a8a83a9ff533b14aa
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Mettre à jour la progression du cycle

Lorsque vous vous connectez à votre tableau de bord [!DNL Adobe Commerce Intelligence], il existe plusieurs façons de vérifier le statut de votre dernier cycle de mise à jour. Tout dépend du type d’[autorisations utilisateur](../administrator/user-management/user-management.md) dont vous disposez.

## Pourquoi dois-je vérifier le statut du cycle de mise à jour ?

La vérification du cycle de mise à jour de l’état est utile lorsque vous auditez les données de votre compte [!DNL Commerce Intelligence]. Si vous constatez [résultats qui ne répondent pas à vos attentes](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md) par exemple, les ventes quotidiennes dans [!DNL Commerce Intelligence] ne correspondent pas à ce que vous voyez dans votre plateforme d’e-commerce ou dans votre [[!DNL Google] chiffre d’affaires d’e-commerce](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) vous pouvez vérifier le dernier point de données pour voir si le problème est résolu une fois une mise à jour terminée.

## [!UICONTROL Read-Only] et [!UICONTROL Standard] utilisateurs

`Read-only` utilisateurs peuvent se connecter à leur tableau de bord et voir la date de la dernière mise à jour des données en pointant sur l’icône en haut à droite de la page. Indique à quel moment le dernier point de données a été extrait.

![Date et heure de la dernière mise à jour de données réussie affichée dans l’interface](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Users

`Admin` utilisateurs peuvent se connecter au tableau de bord et voir le dernier point de données ci-dessus, ainsi qu’une brève icône de statut de leurs intégrations de compte.

Pour plus d’informations, les utilisateurs administrateurs peuvent cliquer sur **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![Page Gérer les intégrations de données affichant les détails de connexion et le statut de mise à jour](../../mbi/assets/detail-manage-data-integrations.png)

Cette page vous indique le statut actuel de la mise à jour et l&#39;heure de la dernière mise à jour terminée.

Si une mise à jour est en cours, un lien vous permet de demander une notification par e-mail une fois la mise à jour terminée.

Si aucune mise à jour n’est en cours, un lien s’affiche pour forcer le démarrage d’une mise à jour.

>[!NOTE]
>
>Si des heures d’interruption sont définies (heure à laquelle vous ne souhaitez pas que [!DNL Commerce Intelligence] mettiez à jour vos données), forcer une mise à jour lance un cycle de mise à jour qui ne respecte pas les limites de ces heures d’interruption.


## Vérifier l’état du cycle de mise à jour à l’aide de l’API

Vous pouvez récupérer le cycle de mise à jour terminé le plus récent à l’aide de l’API **Update Cycle Status**.

**Requête**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**Réponse (exemple)**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

Pour les paramètres, l’authentification, les erreurs et les limites de débit, consultez [Mise à jour de l’API Cycle Status](https://developer.adobe.com/commerce/services/reporting/update-cycle-status-api/) dans la documentation destinée aux développeurs.
