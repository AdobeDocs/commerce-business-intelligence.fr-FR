---
title: Connexion à Microsoft SQL Server
description: Découvrez comment connecter votre base de données SQL Microsoft à [!DNL Commerce Intelligence] dans un processus en quatre étapes.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connexion [!DNL Microsoft SQL] Serveur

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Cette rubrique explique comment connecter votre [!DNL Microsoft SQL] vers la base de données [!DNL Commerce Intelligence] dans un processus en quatre étapes. Ce processus nécessite une certaine expertise technique en ce qui concerne les connexions au serveur et SQL, et peut nécessiter l’aide des développeurs de votre équipe.

[!DNL Commerce Intelligence] prend en charge [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]et la plupart des autres fournisseurs de serveurs cloud. Si vous avez une question sur votre hôte particulier, [envoi d’un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) nous demandant de fournir cette information.

Votre système doit exécuter des requêtes SELECT sur votre base de données. Cette opération est initialement effectuée pour obtenir un instantané de la structure de votre base de données, puis effectuer régulièrement des heures supplémentaires afin de tenir vos données à jour. Vos mises à jour sont incrémentielles et les Adobes limitent la fréquence et le temps de mise à jour afin d’éviter toute charge indésirable sur votre serveur.

Pour ce faire, nous vous invitons à vous connecter à votre serveur de base de données via TCP/IP. Créez un utilisateur qui ne peut exécuter que les requêtes SELECT (et, éventuellement, ne peut sélectionner que les données des tables que vous spécifiez). Cela doit être effectué pour chacun des serveurs auxquels vous vous connectez. [!DNL Commerce Intelligence].

## Connexion `Microsoft SQL` to [!DNL Commerce Intelligence]:

1. Assurez-vous que votre serveur autorise les connexions via TCP/IP et l’authentification en mode mixte.

1. Assurez-vous que votre pare-feu permet à l’adresse IP dédiée de votre serveur de se connecter.

   Vous trouverez l’adresse IP utilisée pour la connexion à votre serveur dans la section Connexions de votre `Settings` page.

1. Créez un utilisateur à utiliser pour se connecter à votre serveur de base de données. Vous avez deux options : via `UI` ou via un `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (deuxième exemple)

1. Saisissez l’adresse IP, le nom d’utilisateur et le mot de passe du serveur dans [!DNL Commerce Intelligence] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Cliquez sur **[!UICONTROL Add a Data Source]**.

1. Sélectionnez cette option pour connecter un `Microsoft SQL` et saisissez vos informations d’identification dans les champs du nouveau `Connections` page.

   Si vous utilisez `Windows Azure`, vous devez également spécifier un nom de base de données.
