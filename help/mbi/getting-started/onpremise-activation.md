---
title: Activez votre [!DNL MBI] Compte pour les abonnements On-Premise
description: En savoir plus sur l’activation de [!DNL MBI] Compte pour les abonnements On-Premise.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Activez votre [!DNL MBI] Compte pour les abonnements On-Premise

Pour activer [!DNL MBI] pour les abonnements on-premise, commencez par créer un [!DNL MBI] compte, puis connectez-vous [!DNL MBI] à votre base de données Commerce. Pour plus d’informations sur l’activation dans `Cloud Starter` projets, voir [Activez votre [!DNL MBI] Compte pour `Cloud Starter` Abonnements](../getting-started/cloud-activation.md).

1. Créez votre [!DNL MBI] Compte.

   - Accédez à [Connexion au compte Adobe Commerce](https://account.magento.com/customer/account/login)

   - Accédez à **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Cliquez sur **[!UICONTROL Create Instance]**. Si vous ne voyez pas ce bouton, contactez votre équipe de compte d’Adobe ou votre conseiller technique du client.

   - Renseignez les informations pour créer votre compte.

   ![](../assets/create-account-2.png)

   - Accédez à votre boîte de réception et vérifiez votre adresse électronique. Si vous n’avez pas reçu d’e-mail, [support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - Créez votre mot de passe.

   ![](../assets/create-account-4.png)

   - Après avoir créé votre compte, vous avez la possibilité d’ajouter des utilisateurs à votre nouveau compte. Vous pouvez désormais ajouter des administrateurs techniques pour réaliser les étapes suivantes.

   ![](../assets/create-account-5.png)

1. Saisissez des informations sur votre boutique pour définir vos préférences.

   ![](../assets/create-account-6.png)

1. Connexion [!DNL MBI] à votre base de données Commerce à l’aide d’une connexion chiffrée.

   Commerce recommande vivement de vous connecter à l’aide d’une [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). Cependant, s’il ne s’agit pas d’une option, vous pouvez toujours lier [!DNL MBI] à votre base de données à l’aide d’un [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. Une fois que vous êtes connecté [!DNL MBI] dans votre base de données Commerce, contactez votre équipe de compte d’Adobe pour coordonner les étapes suivantes, telles que la configuration des intégrations et d’autres étapes de configuration.

1. Une fois la configuration terminée, vous pouvez [connexion](../getting-started/sign-in.md) à [!DNL MBI] compte .
