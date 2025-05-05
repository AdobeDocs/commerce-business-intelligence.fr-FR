---
title: Audit des données des mots-clés Google
description: Découvrez les étapes à suivre pour exporter vos données Google AdWords.
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Données d&#39;audit [!DNL Google Adwords]

Vous avez trouvé quelque chose d&#39;étrange dans [[!DNL Google Adwords]](../integrations/google-adwords.md) ? Pour déterminer le problème, vous devez explorer vos données. Pour ce faire, exportez vos données [!DNL Google Adwords] vers un fichier `.csv`.

1. Téléchargez et installez l&#39;application gratuite [[!DNL Google Adwords] Editor](https://ads.google.com/home/tools/ads-editor/).

1. Une fois l’installation terminée, sélectionnez `Add Count` dans le panneau `Add/manage accounts`.

1. Saisissez les informations de votre compte [!DNL Google Adwords].

1. Une fois votre compte ajouté à l’éditeur [!DNL Google Adwords], sélectionnez **[!UICONTROL File** > **&#x200B; Exporter la feuille de calcul (CSV)**> **Exporter tout le compte]**

Cela crée un fichier `.csv` contenant toutes les informations stockées dans votre compte [!DNL Google Adwords] actuel. À ce stade, envoyez un [ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) (veillez à joindre ce fichier !) afin que vous puissiez examiner de plus près vos données. Si le fichier est trop volumineux, partagez-le avec l&#39;équipe [!DNL Commerce Intelligence] via [!DNL Dropbox] ou [!DNL Google Drive].

Pour plus d&#39;informations sur les [!DNL Google Adwords] `.csv` exports de fichiers, consultez la [[!DNL Google Adwords] documentation](https://support.google.com/google-ads/editor/answer/38657?hl=en) officielle.
