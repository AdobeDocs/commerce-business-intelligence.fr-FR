---
title: Audit des données Zendesk
description: Découvrez les étapes à suivre pour exporter vos données Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Audit des données Zendesk

Trouvez quelque chose d&#39;étrange dans votre [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? Pour déterminer le problème, vous devez explorer vos données. Pour ce faire, exportez vos [!DNL Zendesk] des données dans un fichier téléchargeable.

## Activer l&#39;export des données

L’exportation des données n’est actuellement pas activée pour tous les [!DNL Zendesk] comptes. Pour activer cette fonctionnalité, procédez comme suit : [envoyer un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html), en mentionnant votre [!DNL Zendesk] nom du sous-domaine.

>[!NOTE]
>
>Uniquement `Enterprise` et `Plus` les plans ont actuellement accès à cette fonctionnalité.

Une fois l’exportation des données activée, seuls les administrateurs d’un domaine de messagerie spécifique peuvent exporter des données de votre [!DNL Zendesk] compte . Ce domaine de courriel est généralement le même que votre [!DNL Zendesk]. Le domaine d’adresse électronique du propriétaire du compte est utilisé par défaut, mais vous pouvez le modifier si nécessaire.

## Export vers un fichier téléchargeable

1. Cliquez sur l’icône Admin (logo de l’engrenage) dans la barre latérale, puis sélectionnez **[!UICONTROL Manage** > **Reports]**.
1. Cliquez sur le bouton **[!UICONTROL Export]** .
1. Cliquez sur **[!UICONTROL Request file]** en regard de l’exportation XML complète, comme illustré dans l’image ci-dessous.

   À ce stade, une version commence ; vous êtes averti par courrier électronique lorsqu’elle est terminée.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Cliquez sur le lien de votre notification électronique pour télécharger un fichier zip contenant le rapport.

   Ce lien de téléchargement est valide pendant au moins trois jours.

Ce processus crée un fichier XML contenant toutes les informations stockées dans votre [!DNL Zendesk] , y compris les données de ticket (avec commentaires), les données utilisateur et les données de compte. À ce stade, vous pouvez [envoyer un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (veillez à joindre ce fichier !) afin que vous puissiez examiner de plus près vos données. Si le fichier est trop volumineux, partagez-le avec la fonction [!DNL Commerce Intelligence] l’équipe via [!DNL Dropbox] ou [!DNL Google Drive].

Pour plus d’informations sur [!DNL Zendesk] export de fichiers, voir à ce sujet la section officielle [[!DNL Zendesk] documentation d’exportation](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
