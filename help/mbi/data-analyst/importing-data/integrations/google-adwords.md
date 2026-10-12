---
title: Connecter Google Adwords
description: Découvrez comment mesurer le ROI de la campagne en associant votre coût publicitaire et la valeur client à vie (CLV) des utilisateurs acquise à partir de vos campagnes.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/mZ8R2vPyFy8pGpYi4KhqocVnP-OlgMPGU3KJ4C9vsTo'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%
---
# Connexion [!DNL Google Adwords]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

Logo ![Google AdWords](../../../assets/Google_Adwords_logo.png)

Vous avez fait vos recherches, vous avez créé vos publicités, vous avez lancé votre campagne [!DNL Google]. Il est maintenant temps d&#39;analyser vos données sur les dépenses publicitaires et de voir si votre argent est dépensé efficacement. À l’aide de vos données de dépenses publicitaires, vous pouvez [mesurer le retour sur investissement de la campagne en associant votre coût publicitaire et la valeur client à vie (CLV)](../../analysis/roi-ad-camp.md) des utilisateurs acquis à partir de vos campagnes.

Commencez par saisir vos informations d’identification [!DNL Google Adwords] dans [!DNL Commerce Intelligence].

1. Accédez à la page `Connections` sous **Gérer les données > Intégrations**.
1. Cliquez sur **Ajouter une intégration**, en haut à droite de l’écran.
1. Cliquez sur l’icône **[!DNL Google Adwords]** . La page des informations d’identification de [!DNL Google Adwords] s’ouvre.
1. Saisissez vos informations d’identification [!DNL Google Analytics]. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter [!DNL Commerce Intelligence].

   Boîte de dialogue de connexion à ![Google AdWords affichant la sélection du profil](../../../assets/cnnct-profile.png)

1. Les modifications sont enregistrées automatiquement. Cliquez donc sur **[!UICONTROL Back to Connections]** lorsque vous avez terminé.

Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier lequel, reportez-vous à la section `Connecting Multiple Google Analytics profiles` ci-dessous.

## Connexion de plusieurs profils [!DNL Google Analytics]

Plusieurs sites web peuvent être connectés à un seul compte [!DNL Google Analytics], identifié par son propre identifiant de profil [!DNL Google Analytics]. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

**Pour identifier l’identifiant de profil Google Analytics d’un site web particulier, procédez comme suit**

1. Connexion à [!DNL Google Analytics]
1. Accéder au tableau de bord de [!DNL Google Analytics] du site web spécifique
1. Examinez l’URL : l’identifiant de profil correspond aux huit numéros `p` à la fin de la ligne :

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Déconnexion de [!DNL Google Adwords]

1. Consultez votre page [!DNL Google] [paramètres du compte](https://www.google.com/account/about/?hl=en).
1. Dans la section `Security` , cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]**.

## Connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
* [Suivre la source de référence de commande via  [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Suivre la source de référence des utilisateurs dans votre base de données](../../analysis/google-track-user-acq.md)
* [Découvrez vos sources et canaux d’acquisition les plus précieux.](../../analysis/most-value-source-channel.md)
* [Augmenter le retour sur investissement de vos campagnes publicitaires](../../analysis/roi-ad-camp.md)
* [Comment fonctionne  [!DNL Google Analytics] ’attribution UTM ?](../../analysis/utm-attributes.md)
