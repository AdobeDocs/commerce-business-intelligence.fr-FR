---
title: Auditer les données Zendesk
description: Découvrez les étapes à suivre pour exporter vos données Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 306
ht-degree: 0%

---

# Auditer les données Zendesk

Vous avez trouvé quelque chose d’étrange dans vos [[!DNL Zendesk] données](../integrations/exp-zendesk-data.md) ? Pour identifier le problème, vous devez explorer vos données. Pour ce faire, exportez vos données [!DNL Zendesk] dans un fichier téléchargeable.

## Activer l&#39;export de données

L’exportation des données n’est actuellement pas activée pour tous les comptes [!DNL Zendesk]. Pour activer cette fonctionnalité, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) en mentionnant votre nom de sous-domaine [!DNL Zendesk].

>[!NOTE]
>
>Seuls les plans `Enterprise` et `Plus` ont actuellement accès à cette fonctionnalité.

Une fois l’exportation des données activée, seuls les administrateurs d’un domaine d’e-mail spécifique peuvent exporter les données de votre compte [!DNL Zendesk]. Ce domaine de messagerie est généralement le même que celui de votre [!DNL Zendesk]. Le domaine de messagerie du propriétaire du compte est utilisé par défaut, mais vous pouvez modifier le domaine si nécessaire.

## Exporter vers un fichier téléchargeable

1. Cliquez sur l’icône Administration (logo de l’engrenage) dans la barre latérale et sélectionnez **[!UICONTROL Manage** > **Reports]**.
1. Cliquez sur l’onglet **[!UICONTROL Export]** .
1. Cliquez sur **[!UICONTROL Request file]** en regard de Exportation XML complète comme illustré dans l’image ci-dessous.

   À ce stade, une version commence ; vous êtes averti par e-mail lorsqu’elle est terminée.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Cliquez sur le lien de votre notification par e-mail pour télécharger un fichier zip contenant le rapport.

   Ce lien de téléchargement est valide pendant au moins trois jours.

Ce processus crée un fichier XML contenant toutes les informations stockées dans votre compte [!DNL Zendesk] actuel, y compris les données de ticket (avec commentaires), les données utilisateur et les données de compte. À ce stade, vous pouvez [soumettre un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (veillez à joindre ce fichier !) vous pouvez ainsi examiner vos données de plus près. Si le fichier est trop volumineux, partagez-le avec l’équipe [!DNL Commerce Intelligence] via [!DNL Dropbox] ou [!DNL Google Drive].

Pour plus d’informations sur les exportations de fichiers [!DNL Zendesk], consultez la documentation officielle [[!DNL Zendesk] export](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
