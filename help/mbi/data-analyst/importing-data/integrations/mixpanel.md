---
title: Connexion à Mixpanel
description: Découvrez comment analyser la manière dont les utilisateurs naviguent et utilisent vos sites web et applications.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Connexion [!DNL Mixpanel]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Avec [!DNL Mixpanel], vous pouvez analyser la manière dont les utilisateurs naviguent et utilisent vos sites web et vos applications. En examinant de près les données sur le comportement des utilisateurs, vous obtenez une conception et des décisions de développement plus intelligentes, ce qui signifie qu’un meilleur produit dans son ensemble. La connexion de [!DNL Mixpanel] à [!DNL Commerce Intelligence] vous permet d’analyser le comportement de vos utilisateurs et la manière dont ce comportement se traduit en recettes.

La connexion de vos données [!DNL Mixpanel] à [!DNL Commerce Intelligence] est un processus simple en trois étapes :

1. [Ouvrez la page [!DNL Mixpanel] credentials dans [!DNL Commerce Intelligence].](#stepone)
1. [Récupération de vos informations d’identification d’API  [!DNL Mixpanel] ](#steptwo)
1. [Entrez vos  [!DNL Mixpanel]  informations d’identification API dans [!DNL Commerce Intelligence]](#stepthree)

Pour terminer ce processus, vous devez ouvrir deux fenêtres ou onglets de navigateur, l’un pour [!DNL Commerce Intelligence] et l’autre pour votre compte [!DNL Mixpanel].

## Ouverture de la page d’informations d’identification [!DNL Mixpanel] {#stepone}

Prise en main :

1. Accédez à la page `Connections` sous **[!DNL Manage Data** > **Connections]**.

1. Cliquez sur **[!UICONTROL Add a New Source]**, situé sur le côté droit de l’écran au-dessus de la table `Data Sources`.

1. Cliquez sur l’icône [!DNL Mixpanel] et la page des informations d’identification s’ouvre.

Laissez cette page ouverte pour l’instant et passez à la fenêtre du navigateur avec votre compte [!DNL Mixpanel].

## Récupération de vos informations d’identification d’API [!DNL Mixpanel] {#steptwo}

Si vous ne vous êtes pas encore connecté à votre compte [!DNL Mixpanel], faites-le, puis procédez comme suit :

1. Cliquez sur **[!UICONTROL Account]** dans le coin supérieur droit.

1. Dans la boîte de dialogue affichée, cliquez sur **[!UICONTROL Projects]**.

1. Vos informations d’identification d’API s’affichent :

![ Récupération des informations d’identification de l’API Mixpanel](../../../assets/Mixpanel_API_creds.png)

Gardez ceci ouvert, vous avez besoin qu&#39;il termine ceci.

## Saisie de vos informations d’identification d’API [!DNL Mixpanel] dans [!DNL Commerce Intelligence] {#stepthree}

1. Copiez `API Key` et `Secret` dans la page des informations d’identification [!DNL Mixpanel] de [!DNL Commerce Intelligence].
1. Cliquez sur **[!UICONTROL Connect to Mixpanel]** pour terminer la configuration.

Si la connexion est établie, un _Succès !Le message_ s’affiche en haut de la page.

### Associé

* [Données  [!DNL Mixpanel] attendues](../integrations/mixpanel-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
