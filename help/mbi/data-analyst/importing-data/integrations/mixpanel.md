---
title: Connecter Mixpanel
description: Découvrez comment analyser la manière dont les utilisateurs naviguent sur vos sites web et utilisent vos applications.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Connexion [!DNL Mixpanel]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![Logo Mixpanel](../../../assets/Mixpanel_logo.png)

Avec [!DNL Mixpanel], vous pouvez analyser la manière dont les utilisateurs naviguent sur vos sites web et utilisent vos applications. En examinant de près les données de comportement des utilisateurs, vous pouvez prendre des décisions de conception et de développement plus intelligentes, ce qui signifie un meilleur produit dans l’ensemble. La connexion de [!DNL Mixpanel] à [!DNL Commerce Intelligence] vous permet d’analyser le comportement de vos utilisateurs et la manière dont ce comportement se traduit en chiffre d’affaires.

La connexion de vos données [!DNL Mixpanel] pour [!DNL Commerce Intelligence] un processus simple en trois étapes :

1. [Ouvrez la page  [!DNL Mixpanel]  informations d’identification dans  [!DNL Commerce Intelligence]](#stepone)
1. [Récupérer vos informations  [!DNL Mixpanel] ’identification API](#steptwo)
1. [Saisissez vos informations  [!DNL Mixpanel] ’identification API dans  [!DNL Commerce Intelligence]](#stepthree)

Pour terminer ce processus, vous devez ouvrir deux fenêtres ou onglets de navigateur, l’un pour [!DNL Commerce Intelligence] et l’autre pour votre compte [!DNL Mixpanel].

## Ouverture de la page des informations d’identification du [!DNL Mixpanel] {#stepone}

Prise en main :

1. Accédez à la page `Connections` sous **[!DNL Manage Data** > **Connections]**.

1. Cliquez sur **[!UICONTROL Add a New Source]**, situé sur le côté droit de l’écran, au-dessus du tableau `Data Sources`.

1. Cliquez sur l’icône [!DNL Mixpanel] et la page d’informations d’identification s’ouvre.

Laissez cette page ouverte pour l’instant et passez à la fenêtre du navigateur avec votre compte [!DNL Mixpanel].

## Récupération de vos informations d’identification d’API [!DNL Mixpanel] {#steptwo}

Si vous ne vous êtes pas encore connecté à votre compte [!DNL Mixpanel], procédez comme suit :

1. Cliquez sur **[!UICONTROL Account]** dans le coin supérieur droit.

1. Dans la boîte de dialogue affichée, cliquez sur **[!UICONTROL Projects]**.

1. Vos informations d’identification d’API s’affichent :

![Récupération des informations d’identification de l’API Mixpanel](../../../assets/Mixpanel_API_creds.png)

Gardez ça ouvert, vous en avez besoin pour l&#39;emballer.

## Saisie des informations d’identification d’API [!DNL Mixpanel] dans [!DNL Commerce Intelligence] {#stepthree}

1. Copiez les `API Key` et les `Secret` dans la page des informations d’identification [!DNL Mixpanel] dans [!DNL Commerce Intelligence].
1. Cliquez sur **[!UICONTROL Connect to Mixpanel]** pour terminer la configuration.

Si la connexion est établie, un _Succès !_ message s’affiche en haut de la page.

### Connexe

* [Données  [!DNL Mixpanel] &#x200B;](../integrations/mixpanel-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
