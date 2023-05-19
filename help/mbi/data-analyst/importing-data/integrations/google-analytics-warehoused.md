---
title: Connexion à Google Analytics Warehouse
description: Découvrez comment les visiteurs utilisent votre site, quel contenu est attrayant, où les visiteurs quittent, etc.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Connexion [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Nécessite [Autorisations d’administrateur](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] est le service d’analyse web le plus utilisé sur Internet. Implémentation [!DNL Google Analytics] sur votre site web vous permet de suivre la manière dont les visiteurs utilisent votre site, quel contenu est attrayant, où les visiteurs quittent, etc. [!DNL Google Analytics Warehoused] est une intégration distincte de votre [!DNL Google Analytics] intégration. Cela permet une meilleure analyse en raison de la fonction [!DNL Google Analytics] données de votre Data Warehouse, qui est différent du flux en direct de la [!DNL Google Analytics] intégration. Analyser ces mesures dans [!DNL Commerce Intelligence], ainsi que d’autres données, améliorent l’intégrité globale et la convivialité de votre site.

## Différence entre l’intégration de GA Warehouse et l’intégration en direct

Le principal différenciateur est qu’une intégration est stockée ([!DNL Google Analytics Warehoused]), et l’autre n’est pas ([!DNL Google Analytics Live]). Dans le cas de [!DNL Google Analytics Warehoused], cela permet de manipuler votre [!DNL Google Analytics] et vous donne la possibilité de combiner des [!DNL Google Analytics] et d’autres sources de données pour créer des rapports pertinents.

Regarder [!DNL Google Analytics] campagnes publicitaires pour un exemple de ce qui peut être fait du point de vue de la manipulation. Supposons que vous ayez plusieurs campagnes publicitaires portant des noms différents pour le quatrième trimestre. Les campagnes sont le résultat d’une initiative marketing spécifique. Avec les données stockées, vous pouvez créer une colonne qui recherche les noms de campagne en question et renvoie le nom de l’initiative du quatrième trimestre `Operation Dumbo`.

L’aspect de combinaison permet [!DNL Google Analytics] données à associer à d&#39;autres données afin de mener des analyses. Par exemple, prenez `Total Time On Site By Ad Campaign` des données provenant de [!DNL Google Analytics] et rejoignez-le contre `Total Spent Per Campaign` des données provenant de [!DNL Facebook Ads] pour obtenir une vue d’ensemble de l’engagement qui vous coûte.

Avec le [!DNL Google Analytics Live] d’autre part, chaque [!DNL Google Analytics] Le graphique est comme un petit silo qui n’est pas stocké dans votre Data Warehouse.

## Connexion [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] est un `Premium` Intégration. [Contacter le support technique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) si vous souhaitez ajouter cette intégration à votre abonnement.

1. Accédez au `Connections` page sous **[!UICONTROL Admin** > **Integrations]**.
1. Cliquez sur **[!UICONTROL Add an Integration]**, situé sur le côté droit.
1. Cliquez sur le bouton [!DNL Google Analytics Warehoused] icône . Cela ouvre la fenêtre [!DNL Google Analytics] informations d’identification.
1. Saisissez votre [!DNL Google Analytics] informations d’identification. Une fois le processus d’autorisation terminé, vous êtes redirigé vers [!DNL Commerce Intelligence].
1. Une liste des identifiants de profil s’affiche. Vérifiez les profils auxquels vous souhaitez vous connecter. [!DNL Commerce Intelligence]. Si vous disposez de plusieurs profils et que vous avez besoin d’aide pour identifier lequel, reportez-vous à la section Connexion à plusieurs [!DNL Google Analytics] profils ci-dessous.

## Connexion de plusieurs [!DNL Google Analytics] profils

Vous pouvez avoir plusieurs sites Web connectés à un seul [!DNL Google Analytics] compte, identifié par leur propre compte [!DNL Google Analytics] identifiant de profil. Dans ce cas, vous avez la possibilité d’inclure tous vos identifiants de profil dans [!DNL Commerce Intelligence]. Vérifiez les identifiants de profil que vous souhaitez inclure lors de l’étape de sélection du profil.

Pour identifier les [!DNL Google Analytics] Identifiant du profil :

1. Se connecter [!DNL Google Analytics]
1. Accédez au [!DNL Google Analytics] tableau de bord
1. Examinez l’URL : l’identifiant du profil correspond aux huit chiffres suivants : `p` à la fin de la ligne

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Déconnexion [!DNL Google Analytics Warehoused] de [!DNL Commerce Intelligence] {#disconnect}

1. Visitez votre [!DNL Google Analytics] [paramètres du compte](https://myaccount.google.com/intro) page.
1. Sous , `Security` , puis cliquez sur **[!UICONTROL edit]** en regard de `Authorizing` applications et sites.
1. Cliquez sur **[!UICONTROL revoke access]** en regard de [!DNL Commerce Intelligence].

## Documentation connexe

* [Réauthentification des intégrations](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Connexion [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analyse de l’activité du site web et des taux de conversion des clients](../../analysis/web-act-cust-conversion.md)
* [Suivi des données d’acquisition utilisateur à l’aide de [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
