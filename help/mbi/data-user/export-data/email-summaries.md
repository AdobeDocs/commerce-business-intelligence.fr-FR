---
title: Créer des résumés d’e-mails automatisés
description: Découvrez comment créer des résumés d’e-mails automatisés.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Créer des résumés d’e-mails automatisés

Les résumés des e-mails sont un puissant outil de communication que vous pouvez utiliser pour partager l’état et les tendances de votre entreprise avec les principales parties prenantes. Grâce aux résumés d’e-mails, vous pouvez :

* Résumés graphiques d’e-mail contenant des rapports
* Inclure ou exclure l’auteur du résumé de l’e-mail de la réception de l’e-mail
* Planifier l’envoi de l’e-mail
* Modifier, supprimer et suspendre des résumés d’e-mails planifiés existants

## Créer un résumé d&#39;e-mail

1. Cliquez sur **[!DNL Manage Data]** puis **[!UICONTROL Email Summary]** dans la barre latérale.

   Si c’est la première fois que vous créez un résumé d’e-mail, cette page n’affiche aucun résumé enregistré.

1. Cliquez sur **[!UICONTROL Create New Email Summary]** dans le coin supérieur droit.

1. Saisissez un nom pour le résumé.

   Choisissez un nom qui véhicule ce qui est inclus dans le résumé. Par exemple, `AOV Comparison`.

1. Dans la section `Choose Content`, sélectionnez les rapports que vous souhaitez inclure dans le résumé.

   Vous pouvez sélectionner jusqu’à dix rapports que vous détenez. Après avoir sélectionné un rapport, utilisez les icônes qui s’affichent pour indiquer si vous souhaitez que ce rapport soit envoyé sous la forme d’un tableau ou d’un graphique. Si vous avez enregistré le rapport sous forme de nombre, vous pouvez uniquement l’envoyer sous forme de nombre. Pour plus d’informations sur l’envoi d’un résumé des e-mails contenant un rapport avec des données obsolètes, voir [Gestion des paramètres de votre compte](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` rapports ne sont disponibles que si vous utilisez la nouvelle architecture.

1. (Facultatif) Sélectionnez `Send Email To Me` si vous souhaitez recevoir l’e-mail.

1. Pour inclure d’autres utilisateurs et utilisatrices dans l’e-mail, saisissez leurs adresses e-mail dans le champ `Add Email Recipients` en les séparant par des virgules, des espaces, des tabulations ou des points-virgules.

## Planifier le résumé des e-mails

Dans le champ `Set when to send the Email Summary` , vous pouvez indiquer quand envoyer les résumés des e-mails. Les options sont les suivantes :

* `Manual`
* `Once`
* `Repeating`

### Enregistrer le résumé de l’e-mail pour un envoi à une date ultérieure

1. Sélectionnez `Manual` dans le champ `Set when to send the Email Summary` .

1. Cliquez sur **[!UICONTROL Save]**.

   Le résumé est ainsi enregistré dans la liste des résumés d’e-mail.

1. Lorsque vous êtes prêt à envoyer le résumé, cliquez sur l’icône d’engrenage et sélectionnez `Send Now`.

### Envoyer le résumé de l&#39;e-mail une fois

1. Sélectionnez `Once` dans le champ `Set when to send the Email Summary` .

1. Spécifiez la date de début dans le calendrier `Select Start Date`.

1. Indiquez l’heure d’envoi de l’e-mail dans le champ `Select time to send` .

### Créer une planification répétée

1. Sélectionnez `Repeating` dans le champ `Set when to send the Email Summary` .

1. Dans le champ `Set Frequency`, sélectionnez `Daily`, `Weekly` ou `Monthly`.

1. Spécifiez la date de début dans le calendrier `Select Start Date`.

1. Indiquez l’heure d’envoi de l’e-mail dans le champ `Select time to send` .

1. (Facultatif) Pour spécifier une date de fin, sélectionnez `End Date` et sélectionnez la date de fin dans le calendrier.

## Modifier le résumé de l&#39;e-mail existant

Après avoir créé et enregistré un résumé de l’e-mail, la page `Email Summaries` affiche une liste de tous les résumés enregistrés. Vous pouvez développer (`+`) chaque ligne pour plus d’informations. Les colonnes de cette vue sont les suivantes :

* `Email Name` - Nom du résumé de l’e-mail
* `Content` - Type de contenu dans le résumé, tel que le nom des rapports. Pour plus d’informations sur l’envoi d’un résumé des e-mails contenant un rapport avec des données obsolètes, voir [Gestion des paramètres de votre compte](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Fréquence, date et heure d’envoi du résumé de l’e-mail
* `Recipients` - Destinataires du résumé de l&#39;email
* `Created Date` - Date de création du résumé de l’e-mail
* `Status` - `Paused` ou `Active`

Cliquez sur l’icône en forme d’engrenage à droite de chaque ligne pour :

* `Send Now` - Envoie immédiatement le résumé de l’e-mail à tous les destinataires spécifiés
* `Edit` : permet de modifier les détails du résumé de l’e-mail.
* `Pause/Active` - Permet de suspendre la diffusion du résumé de l’e-mail ou d’activer le résumé en fonction de sa configuration
* `Delete` - Supprime le résumé de l’e-mail
