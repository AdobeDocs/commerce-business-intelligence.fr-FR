---
title: Connexion aux adwords Google
description: Découvrez comment mesurer le retour sur investissement de la campagne en associant le coût de la publicité et la valeur de durée de vie du client (CLV) des utilisateurs acquis de vos campagnes.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Connexion [!DNL Google Adwords]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Vous avez fait vos recherches, créé vos publicités, lancé votre campagne [!DNL Google]. Il est maintenant temps d’analyser vos données de dépenses publicitaires et de voir si votre argent est dépensé efficacement. À l&#39;aide de vos données de dépenses publicitaires, vous pouvez [mesurer le retour sur investissement de la campagne en associant votre coût de publicité et la valeur de durée de vie du client (CLV)](../../analysis/roi-ad-camp.md) des utilisateurs acquis de vos campagnes.

Commencez en saisissant vos informations d’identification [!DNL Google Adwords] dans [!DNL Commerce Intelligence].

1. Accédez à la page `Connections` sous **Gérer les données > Intégrations**.
1. Cliquez sur **Ajouter une intégration**, dans l’angle supérieur droit de l’écran.
1. Cliquez sur l’icône **[!DNL Google Adwords]** . Cela ouvre la page des informations d’identification [!DNL Google Adwords].
1. Saisissez vos informations d’identification [!DNL Google Analytics]. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. Les modifications sont enregistrées automatiquement. Cliquez donc sur **[!UICONTROL Back to Connections]** lorsque vous avez terminé.

Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier lequel, reportez-vous à la section `Connecting Multiple Google Analytics profiles` ci-dessous.

## Connexion de plusieurs profils [!DNL Google Analytics]

Plusieurs sites web peuvent être connectés à un seul compte [!DNL Google Analytics], identifié par leur propre identifiant de profil [!DNL Google Analytics]. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

**Pour identifier l’identifiant de profil Google Analytics d’un site web spécifique :**

1. Connectez-vous à [!DNL Google Analytics]
1. Accédez au tableau de bord [!DNL Google Analytics] de ce site Web spécifique.
1. Examinez l’URL : l’identifiant du profil correspond aux huit nombres qui suivent `p` à la fin de la ligne :

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Déconnexion [!DNL Google Adwords]

1. Visitez la page [!DNL Google] [paramètres du compte](https://www.google.com/account/about/?hl=en) .
1. Sous la section `Security` , cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]**.

## Associé

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Suivi de la source de référence de commande via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Suivi de la source de référence des utilisateurs dans votre base de données](../../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux](../../analysis/most-value-source-channel.md)
* [Augmentation du retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
* [Comment fonctionne l’attribution de [!DNL Google Analytics] UTM ?](../../analysis/utm-attributes.md)
