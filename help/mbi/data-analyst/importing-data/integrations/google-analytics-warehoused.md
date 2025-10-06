---
title: Connecter Google Analytics Warehouse
description: Découvrez comment les visiteurs et visiteuses utilisent votre site, quel contenu est attrayant, où les visiteurs et visiteuses quittent, etc.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Connexion [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Nécessite des [autorisations d’administrateur](../../../administrator/user-management/user-management.md).

Logo ![Google Analytics](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] est le service d’analyse web le plus utilisé sur Internet. L’implémentation de [!DNL Google Analytics] sur votre site web vous permet de suivre la manière dont les visiteurs et visiteuses utilisent votre site, le contenu attrayant, l’endroit où ils quittent, etc. [!DNL Google Analytics Warehoused] est une intégration distincte de votre intégration [!DNL Google Analytics] existante. Cela permet une meilleure analyse grâce aux données [!DNL Google Analytics] dans votre Data Warehouse, qui est différente du flux en direct de l’intégration [!DNL Google Analytics] existante. L’analyse de ces mesures dans [!DNL Commerce Intelligence], ainsi que d’autres données, améliore l’intégrité globale et la convivialité de votre site.

## Différence entre GA Warehouse et Live Integration

Le principal différenciateur est qu’une intégration est stockée ([!DNL Google Analytics Warehoused]) et que l’autre ne l’est pas ([!DNL Google Analytics Live]). Dans le cas de [!DNL Google Analytics Warehoused], cela permet de manipuler vos données [!DNL Google Analytics] et vous donne la possibilité de combiner des [!DNL Google Analytics] et d’autres sources de données pour créer des rapports pertinents.

Regardez [!DNL Google Analytics] campagnes publicitaires pour un exemple de ce qui peut être fait du point de vue de la manipulation. Supposons que vous ayez plusieurs campagnes publicitaires pour le quatrième trimestre avec des noms différents. Les campagnes sont le résultat d’une initiative marketing spécifique. Avec les données entreposées, vous pouvez créer une colonne qui recherche les noms de campagne en question et renvoie le nom d’initiative du quatrième trimestre de `Operation Dumbo`.

L&#39;aspect de combinaison permet de joindre des données [!DNL Google Analytics] à d&#39;autres données afin de réaliser des analyses. Par exemple, prenez `Total Time On Site By Ad Campaign` données de [!DNL Google Analytics] et associez-les aux données `Total Spent Per Campaign` de [!DNL Facebook Ads] pour obtenir une vue d’ensemble du coût de l’engagement.

Avec l’intégration [!DNL Google Analytics Live], en revanche, chaque graphique [!DNL Google Analytics] ressemble à un petit silo qui n’est pas stocké dans votre Data Warehouse.

## Connexion des [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] est une intégration `Premium`. [Contactez l’assistance ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si vous souhaitez ajouter cette intégration à votre abonnement.

1. Accédez à la page `Connections` sous **[!UICONTROL Admin** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add an Integration]**, situé sur le côté droit.
1. Cliquez sur l’icône [!DNL Google Analytics Warehoused] . La page des informations d’identification de [!DNL Google Analytics] s’ouvre.
1. Saisissez vos informations d’identification [!DNL Google Analytics]. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter [!DNL Commerce Intelligence]. Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour savoir lequel, reportez-vous à la section Connexion de plusieurs profils [!DNL Google Analytics] ci-dessous.

## Connexion de plusieurs profils [!DNL Google Analytics]

Plusieurs sites web peuvent être connectés à un seul compte [!DNL Google Analytics], identifié par son propre identifiant de profil [!DNL Google Analytics]. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier l’identifiant de profil [!DNL Google Analytics] d’un site web particulier :

1. Connexion à [!DNL Google Analytics]
1. Accéder au tableau de bord de [!DNL Google Analytics] du site web spécifique
1. Examinez l’URL : l’identifiant de profil correspond aux huit chiffres suivant `p` à la fin de la ligne

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion de [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Consultez votre page [!DNL Google Analytics] [paramètres du compte](https://myaccount.google.com/intro).
1. Dans la section `Security` , cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL Commerce Intelligence].

## Documentation connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connexion  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyse de l’activité du site web et des taux de conversion des clients](../../analysis/web-act-cust-conversion.md)
* [Suivi des données d’acquisition des utilisateurs à l’aide  [!DNL Google Analytics]  cookies](../../analysis/google-track-user-acq.md)
