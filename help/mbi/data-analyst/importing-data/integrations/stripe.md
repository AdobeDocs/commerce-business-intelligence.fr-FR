---
title: Connexion au Stripe
description: Découvrez comment gérer et suivre les données de paiement et de facture de votre entreprise.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 1%

---

# Connexion [!DNL Stripe]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] vous permet de gérer et de suivre les données de paiement et de facture de votre entreprise. Connexion à [!DNL Stripe] compte à [!DNL Commerce Intelligence] est un processus simple en deux étapes :

1. [Ajouter [!DNL Stripe] comme source de données dans [!DNL Commerce Intelligence]](#stepone)
1. [Autoriser [!DNL Commerce Intelligence] accéder à [!DNL Stripe] Données](#steptwo)

## Ajouter [!DNL Stripe] comme source de données {#stepone}

1. Accédez au `Connections` page sous **[!UICONTROL Admin** > **Connections]**.
1. Cliquez sur **[!UICONTROL Add a Data Source]**, situé sur le côté droit de l’écran, au-dessus de `Data Sources` table.
1. Cliquez sur le bouton [!DNL Stripe] Icône Cette fenêtre affiche le `[!DNL Stripe] authorization` page.
1. Cliquez sur **[!UICONTROL Connect with Stripe]**.

## Autoriser [!DNL Commerce Intelligence] accéder à [!DNL Stripe] data {#steptwo}

Après avoir cliqué **[!UICONTROL Connect with Stripe]**, une page de demande d’accès s’affiche.

1. Cliquez sur **[!UICONTROL Sign in with Stripe to Continue]**.

1. Saisissez vos informations d’identification, puis cliquez sur **[!UICONTROL Sign in to your account]**.

1. Vos informations d’identification seront validées et vous serez redirigé vers [!DNL Commerce Intelligence].

1. Si la connexion est établie, une *Connexion réussie !* s’affiche en haut de l’écran.

## En rapport :

La variable [[!DNL Stripe] Documentation de l’API](https://stripe.com/docs/api) peut être une ressource utile pour en savoir plus sur la manière dont [!DNL Stripe] est intégré à [!DNL Commerce Intelligence].

* [Valeur attendue [!DNL Stripe] data](../integrations/stripe-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
