---
title: Connexion à Zendesk
description: Découvrez comment consolider les rapports de votre service d’assistance dans [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Connexion [!DNL Zendesk]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Connectez-vous à [!DNL Zendesk] data vous permet de consolider les rapports de votre service d’assistance dans [!DNL Commerce Intelligence]. Cela vous permet d’optimiser le service clientèle et de surveiller les performances du service d’assistance en même temps que vos recettes.

Connectez-vous à [!DNL Zendesk] data est un processus simple en trois étapes :

1. [Ouvrez le [!DNL Zendesk] page des informations d’identification [!DNL Commerce Intelligence]](#stepone)
1. [Récupérez vos [!DNL Zendesk] Jeton API](#steptwo)
1. [Saisissez votre [!DNL Zendesk] informations de connexion et jeton dans [!DNL Commerce Intelligence]](#stepthree)

Pour terminer ce processus, vous devez ouvrir deux fenêtres ou onglets de navigateur : l’un pour [!DNL Commerce Intelligence], l’autre pour votre [!DNL Zendesk] compte .

## Ouvrez le [!DNL Zendesk] page des informations d’identification [!DNL Commerce Intelligence] {#stepone}

1. Accédez au `Integrations` page sous **[!UICONTROL Manage Data** > ** Sources de données **> **Intégrations]**.
1. Cliquez sur **[!UICONTROL Add Integration]**, situé sur le côté droit de l’écran.
1. Cliquez sur le bouton [!DNL Zendesk] icône . Cela ouvre la fenêtre [!DNL Zendesk] informations d’identification.

## Récupérez vos [!DNL Zendesk] Jeton API {#steptwo}

1. Dans la fenêtre ou l’onglet dans lequel vous êtes connecté [!DNL Zendesk] , cliquez sur l’icône Paramètres (engrenage) dans le coin inférieur gauche de l’écran.
1. Lorsque la variable `Settings` s’affiche, recherchez `Channels` . Cliquez sur **[!UICONTROL API]** dans cette section.
1. Dans le `Token Access` de cette page, cochez la case en regard de `Enabled`. Une liste des Principaux jetons API s’affiche.
1. Cliquez sur **[!UICONTROL Add New Token]**.
1. Lorsque vous y êtes invité, saisissez le libellé du jeton. Adobe recommande d’utiliser `Commerce Intelligence`, vous savez donc en un coup d’oeil quelle application utilise le jeton.
1. Cliquez sur **[!UICONTROL Create]**.
1. Un jeton API est créé. Copiez ce jeton ; il sera utilisé à l’étape suivante.

## Entrée [!DNL Zendesk] informations de connexion et jeton API dans [!DNL Commerce Intelligence] {#stepthree}

1. Saisissez votre [!DNL Zendesk] préfixe du site et courrier électronique de connexion dans [!DNL Zendesk] page des informations d’identification [!DNL Commerce Intelligence].
1. Saisissez votre jeton API.
1. Cliquez sur **[!UICONTROL Save & Connect]**. Si la connexion est établie, une *Connexion réussie !* s’affiche en haut de l’écran.

## En rapport :

* [Valeur attendue [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
