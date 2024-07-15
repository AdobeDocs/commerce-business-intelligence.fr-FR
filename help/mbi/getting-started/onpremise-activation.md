---
title: Activation de votre compte  [!DNL Adobe Commerce Intelligence]
description: Découvrez à qui contacter pour activer votre compte  [!DNL Commerce Intelligence] .
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: cdd2373c2b9afd85427d437c6d8450f4d4e03350
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Activation de votre compte [!DNL Commerce Intelligence] pour les abonnements On-Premise et Starter

Pour activer [!DNL Commerce Intelligence] pour les abonnements on-premise, commencez par créer un compte [!DNL Commerce Intelligence], saisissez vos informations de paramètres, puis connectez [!DNL Commerce Intelligence] à votre base de données [!DNL Commerce]. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Créer votre compte [!DNL Commerce Intelligence]

Pour créer votre compte, contactez votre équipe de compte d’Adobe ou votre conseiller technique client.

## Créer votre mot de passe

Une fois votre compte créé, recherchez dans votre courrier électronique de notification de compte provenant de [!DNL The Magento BI Team@rjmetrics.com]. Utilisez le lien fourni dans l&#39;email pour accéder à votre compte [!DNL Commerce Intelligence] et créer votre mot de passe. Accédez à votre boîte de réception et vérifiez votre adresse électronique.

Si vous n&#39;avez pas reçu de courrier électronique, [contactez le support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

![](../assets/create-account-4.png)

## Définition des préférences de stockage

Avant de configurer la connexion à la base de données, remplissez le formulaire d’informations de magasin. Ces informations sont requises pour terminer la configuration de **[!UICONTROL Connect your Database]**.

![](../assets/create-account-6.png)

## Ajouter [!DNL Commerce Intelligence] utilisateurs

Après avoir défini votre mot de passe et vous être connecté à [!DNL Commerce Intelligence], vous pouvez ajouter d’autres utilisateurs à votre compte [!DNL Commerce Intelligence]. Lors de l’ajout d’utilisateurs, ajoutez des utilisateurs administrateurs avec les autorisations appropriées pour terminer le processus d’activation.

![](../assets/create-account-5.png)

## Créez un utilisateur [!DNL Commerce Intelligence] dédié dans l&#39;administrateur [!DNL Commerce]

Pour utiliser [!DNL Commerce Intelligence], vous devez ajouter un utilisateur permanent et dédié au projet [!DNL Commerce]. Cet utilisateur dédié sert de connexion permanente à [!DNL Commerce] qui permet la récupération et le transfert de nouvelles données vers le Data Warehouse [!DNL Commerce Intelligence] du compte.

La configuration d&#39;un utilisateur [!DNL Commerce Intelligence] dédié permet de s&#39;assurer que le compte n&#39;est pas désactivé ni supprimé, arrêtant ainsi la connexion [!DNL Commerce Intelligence].


>[!NOTE]
>
>Adobe recommande l’utilisation d’un nom de compte qui indique son statut permanent (par exemple, dédié à l’ITIP, connecteur de base de données ACI, etc.).

Après avoir créé l’utilisateur dédié pour [!DNL Commerce Intelligence] dans l’administrateur, ajoutez le même utilisateur à l’environnement principal du projet [!DNL Commerce] avec un paramètre **[!UICONTROL Master]** de `Contributor`.

![](../assets/commerce-add-user-settings.png)

## Obtention de vos clés SSH Commerce Intelligence

1. Sur la page [!UICONTROL Connect your database] pour la configuration de [!DNL Commerce Intelligence], faites défiler la page vers le bas et sélectionnez **[!UICONTROL Encryption settings]**.

1. Pour **Type de chiffrement**, sélectionnez `SSH Tunnel`.

1. Dans la liste déroulante, copiez la clé publique fournie.

   ![](../assets/encryption-setting-new-account.png)

## Ajoutez votre clé publique au [!DNL Commerce Intelligence]

1. À partir de [!DNL Commerce Admin], connectez-vous à l’aide des informations de connexion de l’utilisateur [!DNL Commerce Intelligence] que vous venez de créer.

1. Sélectionnez l’onglet **Paramètres du compte** .

1. Faites défiler l’écran vers le bas et développez la liste déroulante **[!UICONTROL SSH Keys]**. Sélectionnez ensuite **[!UICONTROL Add a public key]**.

   ![](../assets/add-public-key.png)

1. Collez la clé publique que vous avez copiée à l’étape [!DNL Encryption Type] ci-dessus.

   ![](../assets/paste-public-key.png)

## Fournir les informations d’identification [!DNL Commerce Intelligence] Essentials `MySQL`

1. Mettez à jour votre `.magento/services.yaml`.

   ![](../assets/update-magento-services-yaml.png)

1. Mettez à jour votre `.magento.app.yaml`.

   ![](../assets/magento-app-yaml-relationships.png)

## Obtention des informations de connexion à la base de données

Obtention des informations de connexion à la base de données [!DNL Commerce] vers [!DNL Commerce Intelligence]

1. Pour obtenir vos informations, procédez comme suit.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Consultez les informations de la base de données, qui doivent ressembler à l’exemple suivant.

   ![](../assets/example-database-information.png)

## Connectez [!DNL Commerce Intelligence] à votre base de données [!DNL Commerce] à l’aide d’une connexion chiffrée.

>[!NOTE]
>
>Adobe recommande vivement d’utiliser un tunnel [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) pour établir la connexion à la base de données. Cependant, si cette méthode n&#39;est pas une option, vous pouvez toujours lier [!DNL Commerce Intelligence] à votre base de données à l&#39;aide d&#39;un [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Saisissez vos informations [!DNL Commerce Intelligence] dans l’écran [!UICONTROL Connect your Magento Database].

![](../assets/connect-magento-db.png)

**Entrées :**

[!UICONTROL Integration Name] : [choisissez un nom pour votre instance [!DNL Commerce Intelligence]]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL Nom d’utilisateur]: `mbi`

[!UICONTROL Password] : [mot de passe d’entrée affiché dans la section précédente]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes] : [laissez vide s’il n’y a aucun préfixe de table]

## Définissez vos paramètres [!UICONTROL **Fuseau horaire**]

![](../assets/time-zone-settings.png)

**Entrées :**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone] : [choisissez le fuseau horaire pour lequel vous souhaitez que vos données s&#39;affichent]

## Obtention des informations sur les paramètres de chiffrement

L’interface utilisateur du projet fournit une chaîne d’accès SSH. Cette chaîne peut être utilisée pour collecter les informations nécessaires pour l’ [!UICONTROL **adresse distante**] et le [!UICONTROL **nom d’utilisateur**]. Utilisez la chaîne d’accès SSH en sélectionnant le bouton du site d’accès sur la branche Principal de l’interface utilisateur de projet. Recherchez ensuite vos [!UICONTROL User Name] et [!UICONTROL Remote Address] comme illustré ci-dessous.

![](../assets/master-branch-settings.png)

## Saisissez vos paramètres [!DNL Encryption]

![](../assets/encryption-settings-2.png)

**Entrées :**

[!UICONTROL Encryption Type] : `SSH Tunnel`

[!UICONTROL Remote Address] : `ssh.us-3.magento.cloud` [de l’étape précédente]

[!UICONTROL Username] : `vfbfui4vmfez6-master-7rqtwti—mymagento` [de l’étape précédente]

[!UICONTROL Port]: `22`

## Enregistrez votre intégration.

Après avoir terminé les étapes de configuration, appliquez les modifications en sélectionnant [!UICONTROL **Enregistrer l’intégration**].

Vous avez maintenant réussi à connecter votre base de données [!DNL Commerce] à votre compte [!DNL Commerce Intelligence].

>[!NOTE]
>
>Si vous êtes un client [!DNL Adobe Commerce Intelligence Pro], contactez votre responsable du succès client ou votre conseiller technique client pour coordonner les étapes suivantes.

Une fois la configuration terminée, [connectez-vous](../getting-started/sign-in.md) à votre compte [!DNL Commerce Intelligence].

<!---# Activate your [!DNL Commerce Intelligence] Account 

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
