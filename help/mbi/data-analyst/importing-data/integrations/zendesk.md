---
title: Connexion à Zendesk
description: Découvrez comment consolider le reporting de votre service d’assistance dans  [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Connexion [!DNL Zendesk]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

La connexion de vos données [!DNL Zendesk] vous permet de consolider les rapports de votre centre d’assistance dans [!DNL Commerce Intelligence]. Cela vous permet d’optimiser le service clientèle et de surveiller les performances du service d’assistance en même temps que vos recettes.

La connexion de vos données [!DNL Zendesk] est un processus simple en trois étapes :

1. [Ouvrez la page [!DNL Zendesk] credentials dans [!DNL Commerce Intelligence].](#stepone)
1. [Récupération de votre  [!DNL Zendesk] jeton API](#steptwo)
1. [Saisissez vos  [!DNL Zendesk] informations de connexion et jeton dans [!DNL Commerce Intelligence]](#stepthree)

Pour terminer ce processus, vous devez ouvrir deux fenêtres ou onglets de navigateur : l’un pour [!DNL Commerce Intelligence], l’autre pour votre compte [!DNL Zendesk].

## Ouvrez la page [!DNL Zendesk] des informations d’identification dans [!DNL Commerce Intelligence]. {#stepone}

1. Accédez à la page `Integrations` sous **[!UICONTROL Manage Data** > ** Sources de données **> **Intégrations]**.
1. Cliquez sur **[!UICONTROL Add Integration]**, situé sur le côté droit de l’écran.
1. Cliquez sur l’icône [!DNL Zendesk] . Cela ouvre la page des informations d’identification [!DNL Zendesk].

## Récupération de votre jeton d’API [!DNL Zendesk] {#steptwo}

1. Dans la fenêtre/l’onglet dans lequel vous êtes connecté à votre compte [!DNL Zendesk], cliquez sur l’icône Paramètres (engrenage) dans le coin inférieur gauche de l’écran.
1. Lorsque le menu `Settings` s’affiche, recherchez la section `Channels`. Cliquez sur **[!UICONTROL API]** dans cette section.
1. Dans la section `Token Access` de cette page, cochez la case en regard de `Enabled`. Une liste des jetons d’API actifs s’affiche.
1. Cliquez sur **[!UICONTROL Add New Token]**.
1. Lorsque vous y êtes invité, saisissez le libellé du jeton. Adobe recommande d’utiliser `Commerce Intelligence`. Vous savez donc en un coup d’oeil quelle application utilise le jeton.
1. Cliquez sur **[!UICONTROL Create]**.
1. Un jeton API est créé. Copiez ce jeton ; il sera utilisé à l’étape suivante.

## Saisissez les informations de connexion [!DNL Zendesk] et le jeton API dans [!DNL Commerce Intelligence]. {#stepthree}

1. Saisissez votre préfixe de site [!DNL Zendesk] et votre adresse électronique de connexion dans la page des informations d’identification [!DNL Zendesk] de [!DNL Commerce Intelligence].
1. Saisissez votre jeton API.
1. Cliquez sur **[!UICONTROL Save & Connect]**. Si la connexion est établie, une *connexion réussie !Le message* s’affiche en haut de l’écran.

## En rapport :

* [Données  [!DNL Zendesk] attendues](../integrations/exp-zendesk-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
