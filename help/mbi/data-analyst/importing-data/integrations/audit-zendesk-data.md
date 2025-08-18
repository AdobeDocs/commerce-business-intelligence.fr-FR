---
title: Auditer les données Zendesk
description: Découvrez les étapes à suivre pour exporter vos données Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Auditer les données Zendesk

Vous avez trouvé quelque chose d’étrange dans vos [[!DNL Zendesk] données](../integrations/exp-zendesk-data.md) ? Pour identifier le problème, vous devez explorer vos données. Pour ce faire, exportez vos données [!DNL Zendesk] dans un fichier téléchargeable.

## Activer l&#39;export de données

L’exportation des données n’est actuellement pas activée pour tous les comptes [!DNL Zendesk]. Pour activer cette fonctionnalité, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) en mentionnant votre nom de sous-domaine [!DNL Zendesk].

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

Ce processus crée un fichier XML contenant toutes les informations stockées dans votre compte [!DNL Zendesk] actuel, y compris les données de ticket (avec commentaires), les données utilisateur et les données de compte. À ce stade, vous pouvez [envoyer un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) (veillez à joindre ce fichier) afin de pouvoir examiner de plus près vos données. Si le fichier est trop volumineux, partagez-le avec l’équipe [!DNL Commerce Intelligence] via [!DNL Dropbox] ou [!DNL Google Drive].

Pour plus d’informations sur les exportations de fichiers [!DNL Zendesk], consultez la documentation officielle [[!DNL Zendesk] export](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
