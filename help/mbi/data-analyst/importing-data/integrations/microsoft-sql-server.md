---
title: Connexion à Microsoft SQL Server
description: Découvrez comment connecter votre base de données SQL Microsoft à  [!DNL Commerce Intelligence]  en quatre étapes.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Connexion au serveur [!DNL Microsoft SQL]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![Logo SQL Server de Microsoft](../../../assets/MicrosoftSQLServer-logo.png)

Cette rubrique explique comment connecter votre base de données [!DNL Microsoft SQL] à [!DNL Commerce Intelligence] dans un processus en quatre étapes. Ce processus nécessite une certaine expertise technique liée aux connexions au serveur et à SQL, et peut nécessiter l’assistance des développeurs de votre équipe.

[!DNL Commerce Intelligence] prend en charge [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure] et la plupart des autres fournisseurs de serveurs cloud. Si vous avez des questions sur votre hôte particulier, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) en nous demandant de fournir ces informations.

Votre système doit exécuter des requêtes SELECT sur votre base de données. Cette opération est d’abord effectuée pour obtenir un instantané de la structure de votre base de données, puis régulièrement, au fil du temps, pour maintenir vos données à jour. Vos mises à jour sont incrémentielles et Adobe limite la fréquence et l’heure des mises à jour afin d’éviter toute charge indésirable sur votre serveur.

Pour ce faire, la meilleure solution consiste à se connecter à votre serveur de base de données via TCP/IP. Créez un utilisateur qui ne peut exécuter que des requêtes SELECT (et, éventuellement, ne peut sélectionner que les données des tables que vous spécifiez). Cette opération doit être effectuée pour chacun des serveurs auxquels vous vous connectez [!DNL Commerce Intelligence].

## Connexion de `Microsoft SQL` à [!DNL Commerce Intelligence] :

1. Assurez-vous que votre serveur autorise les connexions via TCP/IP et l’authentification en mode mixte.

1. Assurez-vous que votre pare-feu autorise l’adresse IP dédiée de votre serveur à se connecter.

   L’adresse IP utilisée pour la connexion au serveur figure dans la section Connexions de la page `Settings`.

1. Créez un utilisateur à utiliser pour vous connecter à votre serveur de base de données. Deux options s’offrent à vous : via `UI` ou via un `query` :
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (deuxième exemple)

1. Saisissez l’adresse IP, le nom d’utilisateur et le mot de passe du serveur dans [!DNL Commerce Intelligence] sous **[!UICONTROL Manage Data** > **Connections]**.

   ![Page Gérer les connexions de données affichant les intégrations de bases de données](../../../assets/manage-data-connections.png)

1. Cliquez sur **[!UICONTROL Add a Data Source]**.

1. Sélectionnez cette option pour connecter une base de données `Microsoft SQL` et saisissez vos informations d&#39;identification dans les champs de la nouvelle page de `Connections`.

   Si vous utilisez `Windows Azure`, vous devez également spécifier un nom de base de données.
