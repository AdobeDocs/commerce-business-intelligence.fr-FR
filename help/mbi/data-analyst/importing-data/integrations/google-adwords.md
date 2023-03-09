---
title: Connexion aux adwords Google
description: Découvrez comment mesurer le retour sur investissement de la campagne en associant le coût de la publicité et la valeur de durée de vie du client (CLV) des utilisateurs acquis de vos campagnes.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Connexion [!DNL Google Adwords]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Vous avez fait vos recherches, créé vos publicités, lancé votre campagne. Il est maintenant temps d’analyser vos données de dépenses publicitaires et de voir si votre argent est dépensé efficacement. En utilisant vos données de dépenses publicitaires, vous pouvez : [mesurez le retour sur investissement de la campagne en associant le coût de la publicité et la valeur de durée de vie du client (CLV).](../../analysis/roi-ad-camp.md) des utilisateurs acquis à partir de vos campagnes.

Commencez en saisissant [!DNL Google Adwords] informations d’identification [!DNL MBI]:

1. Accédez à la page Connexions sous **Gérer les données > Intégrations**.
1. Cliquez sur **Ajouter une intégration**, situé dans le coin supérieur droit de l’écran.
1. Cliquez sur le bouton **[!DNL Google Adwords]** icône . Cela ouvre la fenêtre [!DNL Google Adwords] informations d’identification.
1. Saisissez votre [!DNL Google Analytics] informations d’identification. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL MBI].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter. [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. Les modifications sont enregistrées automatiquement, donc cliquez sur **[!UICONTROL Back to Connections]** lorsque vous avez terminé.

Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier lequel, reportez-vous à la section `Connecting Multiple Google Analytics profiles` ci-dessous.

## `Connecting multiple Google Analytics profiles`

Vous pouvez avoir plusieurs sites Web connectés à un seul [!DNL Google Analytics] compte, identifié par leur propre compte [!DNL Google Analytics] Identifiant du profil. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL MBI]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

**Pour identifier l’identifiant de profil Google Analytics d’un site web spécifique :**

1. Se connecter [!DNL Google Analytics]
1. Accédez au [!DNL Google Analytics] tableau de bord
1. Examinez l’URL : l’identifiant du profil correspond aux huit chiffres suivants : `p` à la fin de la ligne :

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Déconnexion [!DNL Google Adwords]

1. Visitez votre [!DNL Google] [paramètres du compte](https://www.google.com/account/about/?hl=en) page.
1. Sous , `Security` , puis cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL MBI].

## Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Suivi de la source de référence de commande via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../../analysis/most-value-source-channel.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
* [Comment [!DNL Google Analytics] Fonctionnement de l’attribution UTM ?](../../analysis/utm-attributes.md)
