---
title: Connexion à Facebook Ads
description: Découvrez comment analyser vos données de dépenses publicitaires et voir si votre argent est dépensé efficacement.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Connexion [!DNL Facebook Ads]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

Vous avez fait vos recherches, créé vos publicités, lancé votre campagne sur [!DNL Facebook]. Il est maintenant temps d’analyser vos données de dépenses publicitaires et de voir si votre argent est dépensé efficacement. En utilisant vos données de dépenses publicitaires, vous pouvez : [mesurez le retour sur investissement de la campagne en associant le coût de la publicité et la valeur de durée de vie du client (CLV).](../../../data-analyst/analysis/roi-ad-camp.md) des utilisateurs acquis à partir de vos campagnes.

Connexion de vos données publicitaires Facebook à [!DNL MBI] est un processus simple en trois étapes :

1. [Ajouter [!DNL Facebook] comme source de données dans [!DNL MBI]](#stepone)
1. [Autoriser [!DNL MBI] accéder à [!DNL Facebook Ads] data](#steptwo)
1. [Sélectionner [!DNL Facebook Ads] Comptes d’extraction de données](#stepthree)

## Ajouter [!DNL Facebook] comme source de données dans [!DNL MBI] {#stepone}

1. Pour ajouter la variable [!DNL Facebook] intégration à votre compte, accédez à la `Connections` page sous **[!UICONTROL Manage Data** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add Integration]**, situé sur le côté droit de l’écran au-dessus des données `Sources` table.
1. Cliquez sur le bouton [!DNL Facebook] icône . Cela affichera la variable [!DNL Facebook] page d’autorisation.
1. Cliquez sur **[!UICONTROL Authorize]**.

## Autoriser [!DNL MBI] accéder à [!DNL Facebook Ads] data {#steptwo}

Après avoir cliqué sur **[!DNL Facebook Authorize]**, une petite fenêtre contextuelle s’affiche :

![](../../../assets/Facebook_Access_Popup.png)

Vous allez suivre une série d’étapes pour autoriser [!DNL MBI] pour accéder aux données de votre profil public, [!DNL Facebook Ads] et les statistiques connexes. Cliquez sur **[!UICONTROL OK]** sur ces étapes pour continuer.

## Sélectionner [!DNL Facebook Ads] Comptes d’extraction de données {#stepthree}

1. Une fois l’authentification terminée, vous serez invité à sélectionner la variable [!DNL Facebook Ads] Comptes à partir desquels vous souhaitez extraire des données. Sélectionnez les comptes de votre choix en cochant la case dans la variable `Connect` colonne .

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Cliquez sur **[!UICONTROL Save Connections]**.

   Si la connexion est établie, une *Connexion réussie !* s’affiche en haut de la page.

## que va-t-il se passer ensuite ? {#next}

Assurez-vous que vous effectuez le suivi [!DNL Facebook] campagnes dans [!DNL Google Analytics]. Cela permet de s’assurer que la variable `utm\_campaign` champ dans [!DNL Google Analytics] est correctement renseigné pour la variable [!DNL Facebook] campagnes.

## Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Connectez-vous à [!DNL Google Adwords] account](../integrations/google-ecommerce.md)
* [Suivi de la source de référence de commande via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../../analysis/google-track-user-acq.md)
* [Suivi des données utilisateur, navigateur et système d’exploitation dans votre base de données](../../analysis/track-usr-dev-browser.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../../analysis/most-value-source-channel.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
* [Comment [!DNL Google Analytics] Fonctionnement de l’attribution UTM ?](../../analysis/utm-attributes.md)
