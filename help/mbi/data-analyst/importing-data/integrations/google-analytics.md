---
title: Connecter Google Analytics
description: Découvrez comment connecter Google Analytics à  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Connexion [!DNL Google Analytics]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

Logo ![Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] est le service d’analyse web le plus utilisé sur Internet. L’implémentation de [!DNL Google Analytics] sur votre site web vous permet de suivre la manière dont les visiteurs et visiteuses utilisent votre site, le contenu attrayant, l’endroit où ils quittent, etc. L’analyse de ces mesures dans [!DNL Commerce Intelligence], ainsi que d’autres données, améliore l’intégrité globale et la convivialité de votre site.

Commencez par saisir vos informations d’identification [!DNL Google Analytics] dans [!DNL Commerce Intelligence] :

1. Accédez à **[!UICONTROL Manage Data** > **Integrations]**.

1. Cliquez sur **[!UICONTROL Add Integration]**, situé dans la partie droite de l’écran.

1. Cliquez sur l’icône [!DNL Google Analytics] . La page des informations d’identification de [!DNL Google Analytics] s’ouvre.

1. Saisissez vos informations d’identification [!DNL Google Analytics]. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].

1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter [!DNL Commerce Intelligence]. Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour savoir lequel, reportez-vous à la section Connexion de plusieurs profils [!DNL Google Analytics] ci-dessous.

   Page d’administration de ![Google Analytics affichant l’ID de profil dans l’URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Les modifications sont enregistrées automatiquement. Par conséquent, cliquez sur **Retour aux connexions** lorsque vous avez terminé.

## Connexion de plusieurs profils [!DNL Google Analytics]

Plusieurs sites web peuvent être connectés à un seul compte [!DNL Google Analytics], identifié par son propre identifiant de profil [!DNL Google Analytics]. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier l’identifiant de profil [!DNL Google Analytics] d’un site web particulier :

1. Connexion à [!DNL Google Analytics]
1. Accéder au tableau de bord de [!DNL Google Analytics] du site web spécifique
1. Examinez l’URL : l’identifiant de profil correspond aux huit numéros `p` à la fin de la ligne :

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion de [!DNL Google Analytics] de [!DNL Commerce Intelligence] {#disconnect}

1. Consultez votre page [!DNL Google Analytics] [paramètres du compte](https://accounts.google.com/).
1. Dans la section `Security` , cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL Commerce Intelligence].

## Connexe :

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connexion  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyse de l’activité du site web et des taux de conversion des clients](../../analysis/web-act-cust-conversion.md)
* [Suivi des données d’acquisition des utilisateurs à l’aide  [!DNL Google Analytics]  cookies](../../analysis/google-track-user-acq.md)
