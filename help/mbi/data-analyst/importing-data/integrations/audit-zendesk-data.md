---
title: Audit des données Zendesk
description: Découvrez les étapes à suivre pour exporter vos données Zendesk.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Audit des données Zendesk

Trouvez quelque chose d&#39;étrange dans votre [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? Pour déterminer le problème, nous devons explorer vos données. Pour ce faire, exportez vos [!DNL Zendesk] des données dans un fichier téléchargeable.

## Activer l&#39;export des données

L’exportation des données n’est actuellement pas activée pour tous les [!DNL Zendesk] comptes. Pour activer cette fonctionnalité, procédez comme suit : [envoi d’un ticket d’assistance](../../../guide-overview.md), en mentionnant votre [!DNL Zendesk] nom du sous-domaine.

>[!NOTE]
>
>Uniquement `Enterprise` et `Plus` les plans ont actuellement accès à cette fonctionnalité.

Une fois l’exportation des données activée, seuls les administrateurs d’un domaine de messagerie spécifique peuvent exporter des données de votre [!DNL Zendesk] compte . Ce domaine de courriel est généralement le même que votre [!DNL Zendesk]. Le domaine d’adresse électronique du propriétaire du compte est utilisé par défaut, mais vous pouvez le modifier si nécessaire.

## Export vers un fichier téléchargeable

1. Cliquez sur l’icône Admin (logo de l’engrenage) dans la barre latérale, puis sélectionnez **[!UICONTROL Manage** > **Reports]**.
1. Cliquez sur le bouton **[!UICONTROL Export]** .
1. Cliquez sur **[!UICONTROL Request file]** en regard de l’exportation XML complète, comme illustré dans l’image ci-dessous.

   À ce stade, une version commencera; vous en serez informé par e-mail une fois qu’il sera terminé.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Cliquez sur le lien de votre notification électronique pour télécharger un fichier zip contenant le rapport.

   Ce lien de téléchargement est valide pendant au moins trois jours.

Ce processus crée un fichier XML contenant toutes les informations stockées dans votre [!DNL Zendesk] , y compris les données de ticket (avec commentaires), les données utilisateur et les données de compte. À ce stade, vous pouvez [envoi d’un ticket d’assistance](../../../guide-overview.md) (veillez à joindre ce fichier !) nous pouvons donc examiner vos données de plus près. Si le fichier est trop volumineux, partagez-le avec la fonction [!DNL MBI] via [!DNL Dropbox] ou [!DNL Google Drive].

Pour plus d’informations sur [!DNL Zendesk] export de fichiers, voir à ce sujet la section officielle [[!DNL Zendesk] documentation d’exportation](https://support.zendesk.com/entries/23002207-Exporting-data-to-a-CSV-or-XML-file-Plus-and-Enterprise-).
