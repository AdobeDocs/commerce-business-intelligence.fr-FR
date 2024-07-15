---
title: Connexion à Google Commerce
description: Découvrez les canaux de référence les plus précieux.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Connexion [!DNL Google ECommerce]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Vous avez un flux constant de trafic et de commandes, ce qui signifie que vous atteignez et acquérez efficacement des clients. Mais quels sont vos canaux de parrainage les plus précieux ? Quelle est la valeur moyenne de durée de vie des clients acquis d’une source par rapport à une autre ? En connectant vos données de source de référence de commande de [!DNL Google ECommerce] à [!DNL Commerce Intelligence], vous pouvez créer des analyses qui vous aident à identifier vos [ canaux marketing les plus précieux](../../../data-analyst/analysis/most-value-source-channel.md).

Commencez en saisissant vos informations d’identification [!DNL Google ECommerce] dans [!DNL Commerce Intelligence] :

1. Accédez à la page `Connections` sous **[!UICONTROL Admin** > **Connections]**.

1. Cliquez sur **[!UICONTROL Add a New Source]**, situé sur le côté droit de l’écran au-dessus de la table `Data Sources`.

1. Cliquez sur l’icône [!DNL Google ECommerce] . Cela ouvre la page des informations d’identification [!DNL Google ECommerce].

1. Saisissez vos informations d’identification [!DNL Google Analytics]. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].

1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter [!DNL Commerce Intelligence].

   Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier celui qui est, reportez-vous à la section **Connexion de plusieurs profils [!DNL Google Analytics] ci-dessous.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Les modifications sont enregistrées automatiquement. Cliquez donc sur **[!UICONTROL Back to Connections]** lorsque vous avez terminé.

## Connexion de plusieurs profils [!DNL Google Analytics] à [!DNL Commerce Intelligence]

Plusieurs sites web peuvent être connectés à un seul compte [!DNL Google Analytics], identifié par leur propre identifiant de profil [!DNL Google Analytics]. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier l’identifiant de profil [!DNL Google Analytics] d’un site web spécifique :

1. Connectez-vous à [!DNL Google Analytics].
1. Accédez au tableau de bord [!DNL Google Analytics] de ce site Web particulier.
1. Examinez l’URL : l’identifiant du profil correspond aux huit nombres qui suivent `p` à la fin de la ligne.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion de [!DNL Google ECommerce] de [!DNL Commerce Intelligence] {#disconnect}

1. Visitez la page [!DNL Google Analytics] [paramètres du compte](https://www.google.com/account/about/?hl=en) .
1. Sous la section `Security` , cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL Commerce Intelligence].

## En rapport :

* [Données  [!DNL Google ECommerce] attendues](../integrations/google-ecommerce-data.md)
* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Configuration [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../../analysis/most-value-source-channel.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
