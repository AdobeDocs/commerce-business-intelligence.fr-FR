---
title: Connecter Zendesk
description: Découvrez comment consolider les rapports du Help Desk dans  [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Connexion [!DNL Zendesk]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![Logo Zendesk](../../../assets/Zendesk_logo.png)

La connexion de vos données [!DNL Zendesk] vous permet de consolider les rapports du Help Desk dans [!DNL Commerce Intelligence]. Vous pouvez ainsi optimiser le service clientèle et surveiller les performances du Help Desk parallèlement à vos recettes.

La connexion de vos données [!DNL Zendesk] est un processus simple en trois étapes :

1. [Ouvrez la page  [!DNL Zendesk]  informations d’identification dans  [!DNL Commerce Intelligence]](#stepone)
1. [Récupération de votre jeton  [!DNL Zendesk] ’API](#steptwo)
1. [Saisissez vos informations  [!DNL Zendesk]  connexion et jeton dans [!DNL Commerce Intelligence]](#stepthree)

Pour terminer ce processus, vous devez ouvrir deux fenêtres ou onglets de navigateur, l’un pour [!DNL Commerce Intelligence], l’autre pour votre compte [!DNL Zendesk].

## Ouvrez la page des informations d’identification de [!DNL Zendesk] dans [!DNL Commerce Intelligence] {#stepone}

1. Accédez à la page `Integrations` sous **[!UICONTROL Manage Data** > ** Sources de données **> **Intégrations]**.
1. Cliquez sur **[!UICONTROL Add Integration]**, situé dans la partie droite de l’écran.
1. Cliquez sur l’icône [!DNL Zendesk] . La page des informations d’identification de [!DNL Zendesk] s’ouvre.

## Récupérer votre jeton API [!DNL Zendesk] {#steptwo}

1. Dans la fenêtre/l’onglet où vous êtes connecté(e) à votre compte [!DNL Zendesk], cliquez sur l’icône Paramètres (engrenage) dans le coin inférieur gauche de l’écran.
1. Lorsque le menu `Settings` s’affiche, recherchez la section `Channels` . Cliquez sur **[!UICONTROL API]** dans cette section.
1. Dans la section `Token Access` de cette page, cochez la case en regard de `Enabled`. Une liste des jetons API actifs s’affiche.
1. Cliquez sur **[!UICONTROL Add New Token]**.
1. À l’invite, saisissez un libellé pour le jeton. Adobe recommande d’utiliser `Commerce Intelligence` afin que vous sachiez en un coup d’œil quelle application utilise le jeton .
1. Cliquez sur **[!UICONTROL Create]**.
1. Un jeton API est créé. Copiez ce jeton ; il sera utilisé à l’étape suivante.

## Saisissez [!DNL Zendesk] informations de connexion et le jeton API dans [!DNL Commerce Intelligence] {#stepthree}

1. Saisissez le préfixe de votre site [!DNL Zendesk] et l’adresse e-mail de connexion dans la page des informations d’identification [!DNL Zendesk] de [!DNL Commerce Intelligence].
1. Saisissez votre jeton API.
1. Cliquez sur **[!UICONTROL Save & Connect]**. Si la connexion est réussie, un *Connexion réussie !* message s’affiche en haut de l’écran.

## Connexe :

* [Données  [!DNL Zendesk] ](../integrations/exp-zendesk-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
