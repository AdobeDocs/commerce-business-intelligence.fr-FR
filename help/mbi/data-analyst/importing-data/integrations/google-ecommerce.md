---
title: Connexion à Google Commerce
description: Découvrez les canaux de référence les plus précieux.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Connexion [!DNL Google ECommerce]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Vous avez un flux constant de trafic et de commandes, ce qui signifie que vous atteignez et acquérez efficacement des clients. Mais quels sont vos canaux de parrainage les plus précieux ? quelle est la valeur moyenne de durée de vie des clients acquis d’une source par rapport à une autre ? En connectant vos données source de référence de commande à partir de [!DNL Google ECommerce] to [!DNL MBI], vous pouvez créer des analyses qui vous aideront à identifier votre [canaux marketing les plus précieux](../../../data-analyst/analysis/most-value-source-channel.md).

Commençons par entrer dans notre [!DNL Google ECommerce] informations d’identification [!DNL MBI]:

1. Accédez au `Connections` page sous **[!UICONTROL Admin** > **Connections]**.
1. Cliquez sur **[!UICONTROL Add a New Source]**, situé sur le côté droit de l’écran, au-dessus de `Data Sources` table.
1. Cliquez sur le bouton [!DNL Google ECommerce] icône . Cette action ouvre la variable [!DNL Google ECommerce] informations d’identification.
1. Saisissez votre [!DNL Google Analytics] informations d’identification. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL MBI].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter. [!DNL MBI].

   Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier lequel, reportez-vous à la section **Connexion de plusieurs profils [!DNL Google Analytics] profils ci-dessous.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Les modifications sont enregistrées automatiquement. Il vous suffit donc de cliquer sur **[!UICONTROL Back to Connections]** lorsque vous avez terminé.

## Connexion de plusieurs [!DNL Google Analytics] profils vers [!DNL MBI]

Vous pouvez avoir plusieurs sites Web connectés à un seul [!DNL Google Analytics] compte, identifié par leur propre compte [!DNL Google Analytics] identifiant de profil. Dans ce cas, vous aurez la possibilité d’inclure tous vos identifiants de profil dans [!DNL MBI]. Il vous suffit de vérifier les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier les [!DNL Google Analytics] Identifiant du profil :

1. Se connecter [!DNL Google Analytics]
1. Accédez au [!DNL Google Analytics] tableau de bord
1. Examinez l’URL : l’identifiant du profil correspond aux 8 chiffres suivants : `p` à la fin de la ligne

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion [!DNL Google ECommerce] de [!DNL MBI] {#disconnect}

1. Visitez votre [!DNL Google Analytics] [paramètres du compte](https://www.google.com/accounts/) page.
1. Sous , `Security` , cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL MBI].

## En rapport :

* [Valeur attendue [!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)
* [Réauthentification des intégrations](https://support.magento.com/hc/en-us/articles/360016733151)
* [Configuration [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../../analysis/most-value-source-channel.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
