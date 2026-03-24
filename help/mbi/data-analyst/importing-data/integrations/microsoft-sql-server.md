---
title: Connexion à Microsoft SQL Server
description: Découvrez comment connecter votre base de données SQL Microsoft à  [!DNL Commerce Intelligence]  en quatre étapes.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/mJFBPJE334m7V8klJk-1xKAfsU4u4ObcwWDZzylJohM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 306
ht-degree: 0%

---

# Connexion au serveur [!DNL Microsoft SQL]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![Logo SQL Server de &#x200B;](../../../assets/MicrosoftSQLServer-logo.png)

Cette rubrique explique comment connecter votre base de données [!DNL Microsoft SQL] à [!DNL Commerce Intelligence] dans un processus en quatre étapes. Ce processus nécessite une certaine expertise technique liée aux connexions au serveur et à SQL, et peut nécessiter l’assistance des développeurs de votre équipe.

[!DNL Commerce Intelligence] prend en charge [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure] et la plupart des autres fournisseurs de serveurs cloud. Si vous avez des questions sur votre hôte particulier, [envoyez un ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) en nous demandant de fournir ces informations.

Votre système doit exécuter des requêtes SELECT sur votre base de données. Cette opération est d’abord effectuée pour obtenir un instantané de la structure de votre base de données, puis régulièrement, au fil du temps, pour maintenir vos données à jour. Vos mises à jour sont incrémentielles et Adobe limite la fréquence et l’heure des mises à jour afin d’éviter toute charge indésirable sur votre serveur.

Pour ce faire, la meilleure solution consiste à se connecter à votre serveur de base de données via TCP/IP. Créez un utilisateur qui ne peut exécuter que des requêtes SELECT (et, éventuellement, ne peut sélectionner que les données des tables que vous spécifiez). Cette opération doit être effectuée pour chacun des serveurs auxquels vous vous connectez [!DNL Commerce Intelligence].

## Connexion de `Microsoft SQL` à [!DNL Commerce Intelligence] :

1. Assurez-vous que votre serveur autorise les connexions via TCP/IP et l’authentification en mode mixte.

1. Assurez-vous que votre pare-feu autorise l’adresse IP dédiée de votre serveur à se connecter.

   L’adresse IP utilisée pour la connexion au serveur figure dans la section Connexions de la page `Settings`.

1. Créez un utilisateur pour vous connecter à votre serveur de base de données. Deux options s’offrent à vous : via `UI` ou via un `query` :
   * `UI`
   * `Query`

1. Saisissez l’adresse IP, le nom d’utilisateur et le mot de passe du serveur dans [!DNL Commerce Intelligence] sous **[!UICONTROL Manage Data** > **Connections]**.

   ![Page Gérer les connexions de données affichant les intégrations de bases de données](../../../assets/manage-data-connections.png)

1. Cliquez sur **[!UICONTROL Add a Data Source]**.

1. Sélectionnez cette option pour connecter une base de données `Microsoft SQL` et saisissez vos informations d&#39;identification dans les champs de la nouvelle page de `Connections`.

   Si vous utilisez `Windows Azure`, vous devez également spécifier un nom de base de données.
