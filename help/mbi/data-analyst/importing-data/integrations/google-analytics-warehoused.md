---
title: Connexion à l’entrepôt de Google Analytics
description: Découvrez comment les visiteurs utilisent votre site, quel contenu est attrayant, où les visiteurs quittent, etc.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Connexion [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] est le service d’analyse web le plus utilisé sur Internet. La mise en oeuvre de [!DNL Google Analytics] sur votre site web vous permet de suivre la manière dont les visiteurs utilisent votre site, quel contenu est attrayant, où les visiteurs quittent, etc. [!DNL Google Analytics Warehoused] est une intégration distincte de votre intégration [!DNL Google Analytics] existante. Il permet une meilleure analyse en raison de la présence des données [!DNL Google Analytics] dans votre Data Warehouse, qui diffère du flux en direct de l’intégration [!DNL Google Analytics] existante. L’analyse de ces mesures dans [!DNL Commerce Intelligence], ainsi que d’autres données, améliore l’intégrité globale et la convivialité de votre site.

## Différence entre l’intégration de GA Warehouse et l’intégration en direct

Le principal différenciateur est qu’une intégration est stockée ([!DNL Google Analytics Warehoused]) et l’autre non ([!DNL Google Analytics Live]). Dans le cas de [!DNL Google Analytics Warehoused], cela permet la manipulation de vos données [!DNL Google Analytics] et vous permet de combiner [!DNL Google Analytics] avec d’autres sources de données pour créer des rapports pertinents.

Examinez [!DNL Google Analytics] campagnes publicitaires pour obtenir un exemple de ce qui peut être fait du point de vue de la manipulation. Supposons que vous ayez plusieurs campagnes publicitaires portant des noms différents pour le quatrième trimestre. Les campagnes sont le résultat d’une initiative marketing spécifique. Avec les données stockées, vous pouvez créer une colonne qui recherche les noms de campagne en question et renvoie le nom de l’initiative du quatrième trimestre `Operation Dumbo`.

L’aspect de combinaison permet de joindre [!DNL Google Analytics] données à d’autres données afin d’effectuer des analyses. Par exemple, prenez les données `Total Time On Site By Ad Campaign` de [!DNL Google Analytics] et rejoignez-les par rapport aux données `Total Spent Per Campaign` de [!DNL Facebook Ads] pour obtenir une vue d&#39;ensemble de l&#39;engagement qui vous coûte.

Avec l&#39;intégration [!DNL Google Analytics Live] en revanche, chaque graphique [!DNL Google Analytics] est comme un petit silo qui n&#39;est pas stocké dans votre Data Warehouse.

## Connexion à [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] est une intégration `Premium`. [Contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr) si vous souhaitez ajouter cette intégration à votre abonnement.

1. Accédez à la page `Connections` sous **[!UICONTROL Admin** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add an Integration]**, situé sur le côté droit.
1. Cliquez sur l’icône [!DNL Google Analytics Warehoused] . Cela ouvre la page des informations d’identification [!DNL Google Analytics].
1. Saisissez vos informations d’identification [!DNL Google Analytics]. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter [!DNL Commerce Intelligence]. Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier celui qui est, reportez-vous à la section Connexion de plusieurs profils [!DNL Google Analytics] ci-dessous.

## Connexion de plusieurs profils [!DNL Google Analytics]

Plusieurs sites web peuvent être connectés à un seul compte [!DNL Google Analytics], identifié par leur propre identifiant de profil [!DNL Google Analytics]. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier l’identifiant de profil [!DNL Google Analytics] d’un site web spécifique :

1. Connectez-vous à [!DNL Google Analytics]
1. Accédez au tableau de bord [!DNL Google Analytics] de ce site Web spécifique.
1. Examinez l’URL : l’identifiant du profil correspond aux huit nombres qui suivent `p` à la fin de la ligne.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion de [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visitez la page [!DNL Google Analytics] [paramètres du compte](https://myaccount.google.com/intro) .
1. Sous la section `Security`, cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL Commerce Intelligence].

## Documentation connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=fr)
* [Connexion [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyse de l’activité du site web et des taux de conversion des clients](../../analysis/web-act-cust-conversion.md)
* [Suivi des données d’acquisition des utilisateurs à l’aide des cookies  [!DNL Google Analytics] ](../../analysis/google-track-user-acq.md)
