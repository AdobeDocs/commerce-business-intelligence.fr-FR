---
title: Créer des résumés d’e-mails automatisés
description: Découvrez comment créer des résumés d’e-mails automatisés.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Créer des résumés d’e-mails automatisés

Les résumés des e-mails sont un puissant outil de communication que vous pouvez utiliser pour partager l’état et les tendances de votre entreprise avec les principales parties prenantes. Grâce aux résumés d’e-mails, vous pouvez :

* Résumés graphiques d’e-mail contenant des rapports
* Inclure ou exclure l’auteur du résumé de l’e-mail de la réception de l’e-mail
* Planifier l’envoi de l’e-mail
* Modifier, supprimer et suspendre des résumés d’e-mails planifiés existants

## Créer un résumé d’e-mail

1. Cliquez sur **[!DNL Manage Data]** puis **[!UICONTROL Email Summary]** dans la barre latérale.

   Si c’est la première fois que vous créez un résumé d’e-mail, cette page n’affiche aucun résumé enregistré.

1. Cliquez sur **[!UICONTROL Create New Email Summary]** dans le coin supérieur droit.

1. Saisissez un nom pour le résumé.

   Choisissez un nom qui véhicule ce qui est inclus dans le résumé. Par exemple, `AOV Comparison`.

1. Dans la section `Choose Content`, sélectionnez les rapports que vous souhaitez inclure dans le résumé.

   Vous disposez de deux options pour ajouter du contenu :

   * **Sélectionner des rapports individuels** - Sélectionnez des rapports spécifiques dans vos tableaux de bord
   * **Sélectionner Tableau de bord entier** - Incluez tous les rapports d’un tableau de bord tels qu’ils apparaissent dans la disposition du tableau de bord

   Vous pouvez sélectionner jusqu’à dix rapports que vous détenez. Après avoir sélectionné un rapport, utilisez les icônes qui s’affichent pour indiquer si vous souhaitez que ce rapport soit envoyé sous la forme d’un tableau ou d’un graphique. Si vous avez enregistré le rapport sous forme de nombre, vous pouvez uniquement l’envoyer sous forme de nombre. Pour plus d’informations sur l’envoi d’un résumé des e-mails contenant un rapport avec des données obsolètes, voir [Gestion des paramètres de votre compte](../../administrator/account-management/managing-account-settings.md).

   Pour ajouter des tableaux de bord entiers, vous disposez des options de format et de suppression suivantes :

   * Remplacer le format du rapport par un graphique ou un tableau
   * Supprimer les rapports de l’e-mail
   * Sélectionnez cette option pour inclure un fichier CSV pour les rapports tabulaires. Cela permet aux destinataires d’accéder aux données brutes exportables directement depuis leur boîte de réception.

   >[!NOTE]
   >
   >`Cohort` rapports ne sont disponibles que si vous utilisez la nouvelle architecture.

   >[!NOTE]
   >
   >Les pièces jointes volumineuses au format CSV sont prises en charge jusqu’à un total combiné de 25 Mo par e-mail.

1. (Facultatif) Sélectionnez `Send Email To Me` si vous souhaitez recevoir l’e-mail.

1. Pour inclure d’autres utilisateurs et utilisatrices dans l’e-mail, saisissez leurs adresses e-mail dans le champ `Add Email Recipients` en les séparant par des virgules, des espaces, des tabulations ou des points-virgules.

## Planifier le résumé des e-mails

Dans le champ `Set when to send the Email Summary` , vous pouvez indiquer quand envoyer les résumés des e-mails. Les options sont les suivantes :

* `Manual`
* `Once`
* `Repeating`

### Enregistrer le résumé de l’e-mail pour l’envoyer ultérieurement

1. Sélectionnez `Manual` dans le champ `Set when to send the Email Summary` .

1. Cliquez sur **[!UICONTROL Save]**.

   Le résumé est ainsi enregistré dans la liste des résumés d’e-mail.

1. Lorsque vous êtes prêt à envoyer le résumé, cliquez sur l’icône d’engrenage et sélectionnez `Send Now`.

### Envoyer le résumé de l’e-mail une fois

1. Sélectionnez `Once` dans le champ `Set when to send the Email Summary` .

1. Spécifiez la date de début dans le calendrier `Select Start Date`.

1. Indiquez l’heure d’envoi de l’e-mail dans le champ `Select time to send` .

### Créer un programme de répétition

1. Sélectionnez `Repeating` dans le champ `Set when to send the Email Summary` .

1. Dans le champ `Set Frequency`, sélectionnez `Daily`, `Weekly` ou `Monthly`.

1. Spécifiez la date de début dans le calendrier `Select Start Date`.

1. Indiquez l’heure d’envoi de l’e-mail dans le champ `Select time to send` .

1. (Facultatif) Pour spécifier une date de fin, sélectionnez `End Date` et sélectionnez la date de fin dans le calendrier.

## Modifier le résumé des e-mails existants

Après avoir créé et enregistré un résumé de l’e-mail, la page `Email Summaries` affiche une liste de tous les résumés enregistrés. Vous pouvez développer (`+`) dans chaque ligne pour plus d’informations. Les colonnes de cette vue sont les suivantes :

* `Email Name` - Nom du résumé de l’e-mail
* `Content` - Type de contenu dans le résumé, tel que le nom des rapports
* `Scheduled` - Fréquence, date et heure d’envoi du résumé de l’e-mail
* `Recipients` - Destinataires du résumé de l&#39;email
* `Created Date` - Date de création du résumé de l’e-mail
* `Status` - `Paused` ou `Active`

>[!NOTE]
>
>Pour plus d’informations sur l’envoi d’un résumé des e-mails contenant un rapport avec des données obsolètes, voir [Gestion des paramètres de votre compte](../../administrator/account-management/managing-account-settings.md).

Cliquez sur l’icône en forme d’engrenage à droite de chaque ligne pour :

* `Send Now` - Envoyez immédiatement le résumé de l’e-mail à tous les destinataires spécifiés
* `Edit` - Modifier les détails du résumé de l’e-mail
* `Pause/Active` - Suspendre ou activer la diffusion du résumé de l’e-mail
* `Delete` - Supprimer le résumé de l’e-mail
