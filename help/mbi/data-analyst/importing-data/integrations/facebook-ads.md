---
title: Connexion à Facebook Ads
description: Découvrez comment analyser vos données de dépenses publicitaires et voir si votre argent est dépensé efficacement.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Connexion [!DNL Facebook Ads]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

Vous avez fait vos recherches, créé vos publicités, lancé votre campagne sur [!DNL Facebook]. Il est maintenant temps d’analyser vos données de dépenses publicitaires et de voir si votre argent est dépensé efficacement. À l&#39;aide de vos données de dépenses publicitaires, vous pouvez [mesurer le retour sur investissement de la campagne en associant votre coût de publicité et la valeur de durée de vie du client (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) des utilisateurs acquis de vos campagnes.

La connexion de vos données [!DNL Facebook Ad] à [!DNL Commerce Intelligence] est un processus simple en trois étapes :

1. [Ajouter  [!DNL Facebook]  comme source de données dans [!DNL Commerce Intelligence]](#stepone)
1. [Autoriser [!DNL Commerce Intelligence] l&#39;accès à vos  [!DNL Facebook Ads] données](#steptwo)
1. [Sélectionner les  [!DNL Facebook Ads] comptes pour extraire des données](#stepthree)

## Ajouter [!DNL Facebook] comme source de données dans [!DNL Commerce Intelligence] {#stepone}

1. Pour ajouter l&#39;intégration [!DNL Facebook] à votre compte [!DNL Commerce Intelligence], accédez à la page `Connections` sous **[!UICONTROL Manage Data** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add Integration]**, situé à droite.
1. Cliquez sur l’icône [!DNL Facebook] . Cela affiche la page d’autorisation [!DNL Facebook].
1. Cliquez sur **[!UICONTROL Authorize]**.

## Autoriser [!DNL Commerce Intelligence] l&#39;accès à vos données [!DNL Facebook Ads] {#steptwo}

Après avoir cliqué sur **[!DNL Facebook Authorize]**, une petite fenêtre contextuelle s’affiche :

![](../../../assets/Facebook_Access_Popup.png)

Vous suivez une série d’étapes pour permettre à [!DNL Commerce Intelligence] d’accéder aux données de votre profil public, [!DNL Facebook Ads] et les statistiques associées. Cliquez sur **[!UICONTROL OK]** sur ces étapes pour continuer.

## Sélectionner [!DNL Facebook Ads] comptes pour extraire des données {#stepthree}

1. Une fois l’authentification terminée, vous serez invité à sélectionner les comptes [!DNL Facebook Ads] à partir desquels vous souhaitez extraire des données. Sélectionnez les comptes de votre choix en cochant la case dans la colonne `Connect`.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Cliquez sur **[!UICONTROL Save Connections]**.

   Si la connexion est établie, une *connexion réussie !Le message* s’affiche en haut de la page.

## Quelle sera la suite ? {#next}

Assurez-vous que vous effectuez le suivi des campagnes [!DNL Facebook] dans [!DNL Google Analytics]. Cela garantit que le champ `utm\_campaign` de [!DNL Google Analytics] est correctement renseigné pour vos campagnes [!DNL Facebook].

## Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
* [Connectez-vous à votre compte  [!DNL Google Adwords] ](../integrations/google-ecommerce.md)
* [Suivi de la source de référence de commande via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../../analysis/google-track-user-acq.md)
* [Suivi des données de périphérique, de navigateur et de système d’exploitation utilisateur dans votre base de données](../../analysis/track-usr-dev-browser.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../../analysis/most-value-source-channel.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
* [Comment fonctionne l’attribution de [!DNL Google Analytics] UTM ?](../../analysis/utm-attributes.md)
