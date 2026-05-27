---
title: Informations sur les données et les mises à jour
description: Découvrez comment vérifier le statut de votre cycle de mise à jour.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/qT3lojSuve8jHgNVKoJCUW82cN2QK497wFX8NVbptWI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 529
ht-degree: 0%

---

# Informations sur les données et les mises à jour

* [Pourquoi mes données ont-elles changé ?](#datachange)
* [Quelle est la différence entre une mise à jour régulière et forcée ?](#regularforcedupdates)
* [Pourquoi le cycle de mise à jour est-il long ?](#updatecycletime)
* [Puis-je être averti à la fin d’un cycle de mise à jour ?](#notifyupdate)
* [Pourquoi les données sont [!DNL Google ECommerce] elles différentes de ma base de données ?](#ecommdatabase)
* [Comment résoudre un problème lié à une incohérence des données ?](#datadiscrepancy)

## Pourquoi mes données ont-elles changé ? {#datachange}

Les valeurs du graphique peuvent changer tout au long de la journée en raison de la synchronisation de nouvelles données avec votre Data Warehouse. En outre, les valeurs des colonnes de données existantes peuvent changer en raison de [nouvelles vérifications](../data-warehouse-mgr/cfg-data-rechecks.md). Une revérification est un processus qui recherche les valeurs modifiées dans les colonnes de données, comme un statut de commande passant de `open` à `shipped`.

Il existe plusieurs façons différentes [pour vérifier le statut de votre cycle de mise à jour](../../best-practices/check-update-cycle.md), en fonction des paramètres d’autorisations de l’utilisateur ou de l’utilisatrice :

* **[!UICONTROL Read-Only]et [!UICONTROL Standard] des utilisateurs** - Vous pouvez pointer sur l’icône en haut à droite de la page pour voir quand le dernier point de données a été extrait.
* **[!UICONTROL Admin]des utilisateurs** - Peut afficher la dernière icône de point de données et de statut d’intégration de compte. Pour plus d’informations, accédez à **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** pour afficher le statut actuel de la mise à jour et l’heure de la dernière mise à jour terminée.
* **Méthode API** - Peut récupérer le cycle de mise à jour terminé le plus récent à l’aide de l’API Update Cycle Status.

Pour plus d&#39;informations sur la vérification de l&#39;état du cycle de mise à jour, voir [Vérification de l&#39;état du cycle de mise à jour](../../best-practices/check-update-cycle.md).

## Quelle est la différence entre une mise à jour régulière et forcée ? {#regularforcedupdates}

Les mises à jour régulières sont des processus **planifiés** tandis que les mises à jour forcées sont **des processus manuels que vous lancez**. Si vous avez des heures d&#39;interruption (ou une période pendant laquelle [!DNL Commerce Intelligence] ne devez pas mettre à jour vos données), forcer une mise à jour lance un cycle qui ne respecte pas les limites de la période d&#39;interruption.

## Pourquoi le cycle de mise à jour est-il long ? {#updatecycletime}

De nombreux facteurs peuvent s’ajouter à une durée de mise à jour déjà longue. Certaines [méthodes de réplication](../data-warehouse-mgr/cfg-replication-methods.md), [fréquence de vérification plus élevée](../data-warehouse-mgr/cfg-data-rechecks.md) et le nombre de tableaux de bord et de graphiques ne sont que quelques-unes des contributions. Adobe recommande de [reconfigurer certains de vos paramètres](../../best-practices/reduce-update-cycle-time.md) et [optimiser votre base de données pour analyse](../../best-practices/opt-db-analysis.md) afin de réduire le temps de mise à jour.

## Puis-je être averti à la fin d’un cycle de mise à jour ? {#notifyupdate}

Si une mise à jour est en cours, vous pouvez utiliser un lien sur la page **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** pour demander une notification par e-mail une fois le cycle terminé. Si aucune mise à jour n’est en cours, un lien s’affiche pour forcer le démarrage d’une mise à jour.

## Pourquoi les données sont[!DNL Google ECommerce]elles différentes de ma base de données ? {#ecommdatabase}

Des incohérences entre [!DNL Google Analytics] et votre base de données peuvent survenir pour diverses raisons. Le suivi n’étant pas correctement activé, les utilisateurs qui visitent en navigation privée et les événements de clics ne fonctionnent pas correctement ne sont que quelques exemples. Si votre chiffre d’affaires et vos commandes ne vous semblent pas corrects, [consultez cette rubrique](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=fr) pour diagnostiquer un problème.

## Comment résoudre un problème lié à une incohérence des données ? {#datadiscrepancy}

Adobe sait que voir des données incohérentes peut être une expérience frustrante. Essayez d’utiliser la [Liste de contrôle des incohérences de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=fr) ou le tutoriel [Exportations de données](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=fr) pour diagnostiquer le problème. Si vous êtes toujours bloqué, [contactez l’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=fr).
