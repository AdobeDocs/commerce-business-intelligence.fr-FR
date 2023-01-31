---
title: Connexion à Mixpanel
description: Découvrez comment analyser la manière dont les utilisateurs naviguent et utilisent vos sites web et applications.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Connexion [!DNL Mixpanel]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Avec [!DNL Mixpanel], vous pouvez analyser la manière dont les utilisateurs naviguent et utilisent vos sites web et vos applications. En examinant de près les données sur le comportement des utilisateurs, vous obtenez une conception et des décisions de développement plus intelligentes, ce qui signifie qu’un meilleur produit dans son ensemble. Connexion [!DNL Mixpanel] to [!DNL MBI] vous permet d’analyser le comportement de vos utilisateurs et la manière dont ce comportement se traduit en recettes.

Connectez-vous à [!DNL Mixpanel] data to [!DNL MBI] un processus simple en trois étapes :

1. [Ouvrez le [!DNL Mixpanel] page des informations d’identification [!DNL MBI]](#stepone)
1. [Récupérez vos [!DNL Mixpanel] Informations d’identification de l’API](#steptwo)
1. [Saisissez votre [!DNL Mixpanel] Informations d’identification de l’API dans MBI](#stepthree)

Pour terminer ce processus, vous devez ouvrir deux fenêtres ou onglets de navigateur : l’un pour [!DNL MBI], l’autre pour votre [!DNL Mixpanel] compte .

## Ouverture de la [!DNL Mixpanel] page des informations d’identification {#stepone}

Commençons :

1. Accédez au `Connections` page sous **[!DNL Manage Data** > **Connections]**.
1. Cliquez sur **[!UICONTROL Add a New Source]**, situé sur le côté droit de l’écran, au-dessus de `Data Sources` table.
1. Cliquez sur le bouton [!DNL Mixpanel] et la page des informations d’identification s’ouvre.

Laissez cette page ouverte pour l’instant et passez à la fenêtre du navigateur avec votre [!DNL Mixpanel] compte .

## Récupération de votre [!DNL Mixpanel] Informations d’identification de l’API {#steptwo}

Si vous n’êtes pas connecté à votre [!DNL Mixpanel] mais, faites-le, puis procédez comme suit :

1. Cliquez sur **[!UICONTROL Account]** dans le coin supérieur droit.
1. Dans la boîte de dialogue affichée, cliquez sur **[!UICONTROL Projects]**.
1. Vos informations d’identification d’API s’affichent :

![Récupération des informations d’identification de l’API Mixpanel](../../../assets/Mixpanel_API_creds.png)

Gardez ceci ouvert - nous en avons besoin pour résumer ceci.

## Saisissez votre [!DNL Mixpanel] Informations d’identification de l’API dans [!DNL MBI] {#stepthree}

1. Copiez le `API Key` et `Secret` dans la [!DNL Mixpanel] page des informations d’identification [!DNL MBI].
1. Cliquez sur **[!UICONTROL Connect to Mixpanel]** pour terminer la configuration.

C&#39;est tout ! Si la connexion est établie, une _Succès !_ s’affiche en haut de la page.

### Associé

* [Valeur attendue [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [Réauthentification des intégrations](https://support.magento.com/hc/en-us/articles/360016733151)
