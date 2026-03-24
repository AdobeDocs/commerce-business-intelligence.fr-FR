---
title: Connecter les publicités Facebook
description: Apprenez à analyser vos données sur les dépenses publicitaires et à voir si votre argent est dépensé efficacement.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/6TR559YyeTHT3KWl3oA4Bdnpr-HCowTXTTkvmP0I0tg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 313
ht-degree: 0%

---

# Connexion [!DNL Facebook Ads]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![Logo Facebook Ads](../../../assets/facebook-ads-logo.png)

Vous avez fait vos recherches, vous avez créé vos publicités, vous avez lancé votre campagne sur [!DNL Facebook]. Il est maintenant temps d&#39;analyser vos données sur les dépenses publicitaires et de voir si votre argent est dépensé efficacement. À l’aide de vos données de dépenses publicitaires, vous pouvez [mesurer le retour sur investissement de la campagne en associant votre coût publicitaire et la valeur client à vie (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) des utilisateurs acquis à partir de vos campagnes.

La connexion de vos données [!DNL Facebook Ad] à [!DNL Commerce Intelligence] est un processus simple en trois étapes :

1. [Ajoutez [!DNL Facebook] en tant que source de données dans  [!DNL Commerce Intelligence]](#stepone)
1. [Autoriser l [!DNL Commerce Intelligence] accès à vos  [!DNL Facebook Ads] ](#steptwo)
1. [Sélectionner [!DNL Facebook Ads] Comptes pour extraire les données](#stepthree)

## Ajoutez [!DNL Facebook] comme source de données dans [!DNL Commerce Intelligence] {#stepone}

1. Pour ajouter l’intégration [!DNL Facebook] à votre compte [!DNL Commerce Intelligence], accédez à la page `Connections` sous **[!UICONTROL Manage Data** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add Integration]**, situé à droite.
1. Cliquez sur l’icône [!DNL Facebook] . La page d’autorisation de [!DNL Facebook] s’affiche.
1. Cliquez sur **[!UICONTROL Authorize]**.

## Autoriser [!DNL Commerce Intelligence] accès à vos données [!DNL Facebook Ads] {#steptwo}

Après avoir cliqué sur **[!DNL Facebook Authorize]**, une petite fenêtre pop-up s’affiche :

![Boîte de dialogue d’autorisation d’accès Facebook pour Commerce Intelligence](../../../assets/Facebook_Access_Popup.png)

Vous suivez une série d’étapes pour [!DNL Commerce Intelligence] permettre d’accéder aux données de votre profil public, de vos [!DNL Facebook Ads] et de vos statistiques connexes. Cliquez sur **[!UICONTROL OK]** sur ces étapes pour continuer.

## Sélectionner les comptes [!DNL Facebook Ads] pour extraire les données {#stepthree}

1. Une fois l’authentification terminée, vous serez invité à sélectionner les comptes [!DNL Facebook Ads] desquels vous souhaitez extraire des données. Sélectionnez les comptes souhaités en cochant la case dans la colonne `Connect` .

   ![Interface de sélection des comptes publicitaires Facebook](../../../assets/Facebook_Ad_Accounts.png)

1. Cliquez sur **[!UICONTROL Save Connections]**.

   Si la connexion est réussie, un *Connexion réussie !* message s’affiche en haut de la page.

## Quelle est la prochaine étape ? {#next}

Assurez-vous du suivi des campagnes [!DNL Facebook] dans [!DNL Google Analytics]. Cela permet de s’assurer que le champ `utm\_campaign` dans [!DNL Google Analytics] est correctement renseigné pour vos campagnes [!DNL Facebook].

## Connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connecter votre  [!DNL Google Adwords] ](../integrations/google-ecommerce.md)
* [Suivre la source de référence de commande via  [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Suivre la source de référence des utilisateurs dans votre base de données](../../analysis/google-track-user-acq.md)
* [Effectuez le suivi des données relatives aux appareils, aux navigateurs et aux systèmes d’exploitation dans votre base de données](../../analysis/track-usr-dev-browser.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux.](../../analysis/most-value-source-channel.md)
* [Augmenter le retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
* [Comment fonctionne  [!DNL Google Analytics] ’attribution UTM ?](../../analysis/utm-attributes.md)
