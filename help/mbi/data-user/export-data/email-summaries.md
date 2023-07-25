---
title: Création de résumés de courriers électroniques automatisés
description: Découvrez comment créer des résumés d’email automatisés.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Création de résumés de courriers électroniques automatisés

Les résumés d’emails sont un puissant outil de communication que vous pouvez utiliser pour partager l’état et les tendances de votre entreprise avec les principaux intervenants. Avec les résumés d’emails, vous pouvez :

* Résumés graphiques des emails contenant des rapports
* Inclure ou exclure l’auteur de résumé de l’email de la réception de l’email
* Planifier l’envoi de l’email
* Modifier, supprimer et suspendre des résumés d’emails planifiés existants

## Créer un résumé des courriers électroniques

1. Cliquez sur **[!DNL Manage Data]** then **[!UICONTROL Email Summary]** dans la barre latérale.

   S’il s’agit de la première fois que vous créez un résumé par courrier électronique, cette page n’affiche aucun résumé enregistré.

1. Cliquez sur **[!UICONTROL Create New Email Summary]** dans le coin supérieur droit.

1. Saisissez le nom du résumé.

   Choisissez un nom qui véhicule ce qui est inclus dans le résumé. Par exemple : `AOV Comparison`.

1. Dans le `Choose Content` , sélectionnez les rapports à inclure dans le résumé.

   Vous pouvez sélectionner jusqu’à dix rapports que vous possédez. Après avoir sélectionné un rapport, utilisez les icônes qui s&#39;affichent pour indiquer si vous souhaitez que ce rapport soit envoyé sous forme de tableau ou de graphique. Si vous avez enregistré le rapport sous forme numérique, vous pouvez uniquement l’envoyer sous forme numérique. Pour plus d’informations sur l’envoi d’un résumé d’email contenant un rapport avec des données obsolètes, voir [Gestion des paramètres de votre compte](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` ne sont disponibles que si vous utilisez la nouvelle architecture.

1. (Facultatif) Sélectionnez `Send Email To Me` si vous souhaitez recevoir l&#39;email.

1. Pour inclure d’autres utilisateurs dans le courrier électronique, saisissez leurs adresses électroniques dans la variable `Add Email Recipients` champ séparé par des virgules, des espaces, des onglets ou des points-virgules.

## Planification : résumé des emails

Dans le `Set when to send the Email Summary` vous pouvez indiquer le moment auquel envoyer les résumés des emails. Les options sont les suivantes :

* `Manual`
* `Once`
* `Repeating`

### Enregistrer le résumé des emails à envoyer ultérieurement

1. Sélectionner `Manual` de la `Set when to send the Email Summary` champ .

1. Cliquez sur **[!UICONTROL Save]**.

   Cette opération enregistre le résumé dans la liste des résumés des emails.

1. Lorsque vous êtes prêt à envoyer le résumé, cliquez sur l’icône représentant un engrenage et sélectionnez `Send Now`.

### Envoyer le résumé par courrier électronique une fois

1. Sélectionner `Once` de la `Set when to send the Email Summary` champ .

1. Indiquez la date de début dans la variable `Select Start Date` calendrier.

1. Indiquez l’heure d’envoi du courrier électronique dans la variable `Select time to send` champ .

### Créer une planification de répétition

1. Sélectionner `Repeating` de la `Set when to send the Email Summary` champ .

1. Dans le `Set Frequency` champ, sélectionnez `Daily`, `Weekly`ou `Monthly`.

1. Indiquez la date de début dans la variable `Select Start Date` calendrier.

1. Indiquez l’heure d’envoi du courrier électronique dans la variable `Select time to send` champ .

1. (Facultatif) Pour spécifier une date de fin, sélectionnez `End Date` et sélectionnez la date de fin dans le calendrier.

## Modifier le résumé des courriers électroniques existants

Une fois que vous avez créé et enregistré un résumé d’email, la variable `Email Summaries` affiche une liste de tous les résumés enregistrés. Vous pouvez développer (`+`) chaque ligne pour plus d’informations. Les colonnes de cette vue sont les suivantes :

* `Email Name` - Nom de la synthèse de l&#39;email
* `Content` - Type de contenu dans la synthèse, tel que le nom de tout rapport. Pour plus d’informations sur l’envoi d’un résumé d’email contenant un rapport avec des données obsolètes, voir [Gestion des paramètres de votre compte](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Fréquence, date et heure d’envoi du résumé du courrier électronique
* `Recipients` - Destinataires de la synthèse des emails
* `Created Date` - Date de création de la synthèse de l’email
* `Status` - `Paused` ou `Active`

Cliquez sur l’icône d’engrenage à droite de chaque ligne pour :

* `Send Now` - Envoie immédiatement la synthèse de l’email à tous les destinataires spécifiés
* `Edit` - Permet de modifier les détails de la synthèse de l&#39;email
* `Pause/Active` - Permet de suspendre la diffusion de la synthèse d&#39;un email ou d&#39;activer la synthèse en fonction de sa configuration.
* `Delete` - Supprime la synthèse de l&#39;email
