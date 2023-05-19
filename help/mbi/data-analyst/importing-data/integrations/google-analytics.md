---
title: Connexion des Google Analytics
description: Découvrez comment connecter des Google Analytics à [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Connexion [!DNL Google Analytics]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] est le service d’analyse web le plus utilisé sur Internet. Implémentation [!DNL Google Analytics] sur votre site web vous permet de suivre la manière dont les visiteurs utilisent votre site, quel contenu est attrayant, où les visiteurs quittent, etc. Analyser ces mesures dans [!DNL Commerce Intelligence], ainsi que d’autres données, améliorent l’intégrité globale et la convivialité de votre site.

Commencez en saisissant [!DNL Google Analytics] informations d’identification [!DNL Commerce Intelligence]:

1. Accédez à **[!UICONTROL Manage Data** > **Integrations]**.

1. Cliquez sur **[!UICONTROL Add Integration]**, situé sur le côté droit de l’écran.

1. Cliquez sur le bouton [!DNL Google Analytics] icône . Cela ouvre la fenêtre [!DNL Google Analytics] informations d’identification.

1. Saisissez votre [!DNL Google Analytics] informations d’identification. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].

1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter. [!DNL Commerce Intelligence]. Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier lequel, reportez-vous à la section Connexion à plusieurs [!DNL Google Analytics] profils ci-dessous.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Les modifications sont enregistrées automatiquement, donc cliquez sur **Retour aux connexions** lorsque vous avez terminé.

## Connexion de plusieurs [!DNL Google Analytics] profils

Vous pouvez avoir plusieurs sites Web connectés à un seul [!DNL Google Analytics] compte, identifié par leur propre compte [!DNL Google Analytics] identifiant de profil. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier les [!DNL Google Analytics] Identifiant du profil :

1. Se connecter [!DNL Google Analytics]
1. Accédez au [!DNL Google Analytics] tableau de bord
1. Examinez l’URL : l’identifiant du profil correspond aux huit chiffres suivants : `p` à la fin de la ligne :

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion [!DNL Google Analytics] de [!DNL Commerce Intelligence] {#disconnect}

1. Visitez votre [!DNL Google Analytics] [paramètres du compte](https://accounts.google.com/) page.
1. Sous , `Security` , puis cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL Commerce Intelligence].

## En rapport :

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connexion [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyse de l’activité du site web et des taux de conversion des clients](../../analysis/web-act-cust-conversion.md)
* [Suivi des données d’acquisition utilisateur à l’aide de [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
