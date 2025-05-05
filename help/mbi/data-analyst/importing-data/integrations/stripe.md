---
title: Connexion au Stripe
description: Découvrez comment gérer et suivre les données de paiement et de facture de votre entreprise.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Connexion [!DNL Stripe]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] vous permet de gérer et de suivre les données de paiement et de facture de votre entreprise. La connexion de votre compte [!DNL Stripe] à [!DNL Commerce Intelligence] est un processus simple en deux étapes :

1. [Ajouter  [!DNL Stripe]  comme source de données dans [!DNL Commerce Intelligence]](#stepone)
1. [Autoriser [!DNL Commerce Intelligence] l’accès à vos  [!DNL Stripe] données](#steptwo)

## Ajouter [!DNL Stripe] en tant que source de données {#stepone}

1. Accédez à la page `Connections` sous **[!UICONTROL Admin** > **Connections]**.
1. Cliquez sur **[!UICONTROL Add a Data Source]**, situé sur le côté droit de l’écran au-dessus de la table `Data Sources`.
1. Cliquez sur l’icône [!DNL Stripe] . La page `[!DNL Stripe] authorization` s’affiche.
1. Cliquez sur **[!UICONTROL Connect with Stripe]**.

## Autoriser [!DNL Commerce Intelligence] l&#39;accès à vos données [!DNL Stripe] {#steptwo}

Après avoir cliqué sur **[!UICONTROL Connect with Stripe]**, une page de demande d’accès s’affiche.

1. Cliquez sur **[!UICONTROL Sign in with Stripe to Continue]**.

1. Saisissez vos informations d’identification et cliquez sur **[!UICONTROL Sign in to your account]**.

1. Vos informations d’identification seront validées et vous serez redirigé vers [!DNL Commerce Intelligence].

1. Si la connexion est établie, une *connexion réussie !Le message* s’affiche en haut de l’écran.

## En rapport :

La [[!DNL Stripe] documentation de l&#39;API](https://stripe.com/docs/api) peut être une ressource utile pour en savoir plus sur la façon dont [!DNL Stripe] est intégré à [!DNL Commerce Intelligence].

* [Données  [!DNL Stripe] attendues](../integrations/stripe-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
