---
title: Audit des données des mots-clés Google
description: Découvrez les étapes à suivre pour exporter vos données Google AdWords.
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Audit [!DNL Google Adwords] data

J&#39;ai trouvé quelque chose d&#39;étrange dans [[!DNL Google Adwords]](../integrations/google-adwords.md)? Pour déterminer le problème, vous devez explorer vos données. Pour ce faire, exportez vos [!DNL Google Adwords] données à un `.csv` fichier .

1. Téléchargez et installez le fichier gratuit [[!DNL Google Adwords] Éditeur](https://ads.google.com/home/tools/ads-editor/) application.

1. Une fois l’installation terminée, sélectionnez `Add Count` dans le `Add/manage accounts` du panneau.

1. Saisissez votre [!DNL Google Adwords] informations du compte.

1. Une fois votre compte ajouté à [!DNL Google Adwords] Éditeur, sélectionnez **[!UICONTROL File** > ** Exporter une feuille de calcul (CSV)**> **Exporter le compte entier]**

Cette version crée une `.csv` fichier contenant toutes les informations stockées dans votre [!DNL Google Adwords] compte . À ce stade, envoyez une [ticket de support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (veillez à joindre ce fichier !) afin que vous puissiez examiner de plus près vos données. Si le fichier est trop volumineux, partagez-le avec la fonction [!DNL Commerce Intelligence] l’équipe via [!DNL Dropbox] ou [!DNL Google Drive].

Pour plus d’informations sur [!DNL Google Adwords] `.csv` export de fichiers, voir à ce sujet la section officielle [[!DNL Google Adwords] documentation](https://support.google.com/google-ads/editor/answer/38657?hl=en).
