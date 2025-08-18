---
title: Rapports du Help Desk pour Zendesk
description: Découvrez vos canaux de recommandation les plus précieux.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Rapports du Help Desk pour [!DNL Zendesk]

>[!NOTE]
>
>Cette option n’est disponible que pour les clients qui sont inclus dans le plan `Pro` et qui utilisent la nouvelle architecture. Vous passez à la nouvelle architecture si la section `Data Warehouse Views` est disponible après avoir sélectionné `Manage Data` dans la barre d’outils principale.

La consolidation de vos données [!DNL Zendesk] avec votre base de données transactionnelle est un excellent moyen de mieux comprendre comment vos clients interagissent avec vos équipes de vente ou de succès client. Cela vous permet également de savoir quel type de clients utilisent votre plateforme d’assistance. Cette rubrique explique comment configurer un tableau de bord pour obtenir des rapports granulaires sur les performances de vos [!DNL Zendesk] et lier vos clients transactionnels.

Avant de commencer, vous devez connecter votre [[!DNL Zendesk]](../integrations/zendesk.md). Cette analyse contient [colonnes calculées avancées](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Prise en main

### Colonnes à suivre

* `audits` table
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` table
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` table
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` table
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Jeux de filtres à créer

* `[!DNL Zendesk] Tickets` table
   * `status != deleted`

* `Filter set name` : `Tickets we count`
* `Filter set logic` :

## Colonnes calculées

### Colonnes à créer

* **`[!DNL Zendesk] user's`** table
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A !=`end-user` puis `Yes` quand `B` n&#39;est pas `null` et `B` comme `%@magento.com` puis `Yes` sinon `No` fin

      * Remplacer `@magento.com` par votre domaine

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** table
   * Sélectionnez une définition : `Joined Column`
   * [!UICONTROL Create Path] :
   * [!UICONTROL Many] : `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One] : `[!DNL Zendesk] users.id`

   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] users`
   * Sélectionner un [!UICONTROL column] : `User is agent? (Yes/No)`
   * [!UICONTROL Path] : `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** table
   * Sélectionnez une définition : `Exists`
   * [!UICONTROL Create Path] :
   * [!UICONTROL Many] : `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One] : `[!DNL Zendesk] audits._id`

   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path] : `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter] :
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Sélectionnez une définition : `Exists`
   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path] : `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter] : `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** table
   * Sélectionnez une définition : `Joined Column`
   * [!UICONTROL Create Path] :
   * [!UICONTROL Many] : `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One] : `[!DNL Zendesk] users.id`

   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] users`
   * Sélectionner un [!UICONTROL column] : `email`
   * [!UICONTROL Path] : `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Sélectionnez une définition : `Joined Column`
   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] users`
   * Sélectionner un [!UICONTROL column] : `role`
   * [!UICONTROL Path] : `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Sélectionnez une définition : `Max`
   * [!UICONTROL Create Path] :
   * [!UICONTROL Many] : `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One] : `[!DNL Zendesk] tickets.id`

   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] audits`
   * Sélectionner un [!UICONTROL column] : `created_at`
   * [!UICONTROL Path] : `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter] :
   * `status` remplacé par `solved = 1`

   * Sélectionnez une définition : `Min`
   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] audits`
   * Sélectionner un [!UICONTROL column] : `created_at`
   * [!UICONTROL Path] : `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter] :
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` moins `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` moins `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - « Même tableau > Calcul »

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - Entier

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - « Même tableau > Calcul »

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`** table
   * Sélectionnez une définition : `Count`
   * [!UICONTROL Create Path] :
   * [!UICONTROL Many] : `[!DNL Zendesk] tickets.email`
   * 
     [!UICONTROL One]: `customer_entity.email`

   * Sélectionner un [!UICONTROL table] : `[!DNL Zendesk] tickets`
   * [!UICONTROL Path] : `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter] :
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - « Même tableau > Calcul »

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`** table
   * Sélectionnez une définition : `Joined Column`
   * Sélectionner un [!UICONTROL table] : `customer_entity`
   * Sélectionner un [!UICONTROL column] : `User's lifetime number of support tickets requested`
   * [!UICONTROL Path] : `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Mesures

* **[!DNL Zendesk]Nouveaux billets**
   * `Tickets we count`

* Dans le tableau **`[!DNL Zendesk] tickets`**
* Cette mesure effectue un **Nombre**
* Dans la colonne **`id`**
* Classé par l’horodatage **`created_at`**
* [!UICONTROL Filter] :

* **[!DNL Zendesk]tickets résolus**
   * `Tickets we count`
   * Statut IN `closed, solved`

* Dans le tableau **`[!DNL Zendesk] tickets`**
* Cette mesure effectue un **Nombre**
* Dans la colonne **`id`**
* Classé par l’horodatage **`created_at`**
* [!UICONTROL Filter] :

* **[!DNL Zendesk]des utilisateurs distincts déposant des tickets**
   * `Tickets we count`

* Dans le tableau **`[!DNL Zendesk] tickets`**
* Cette mesure effectue un **Comptage distinct**
* Dans la colonne **`requester_id`**
* Classé par l’horodatage **`created_at`**
* [!UICONTROL Filter] :

* **[!DNL Zendesk]temps moyen/médian de résolution du ticket**
   * `Tickets we count`
   * Statut IN `closed, solved`

* Dans le tableau **`[!DNL Zendesk] tickets`**
* Cette mesure effectue une **Moyenne (ou Médiane)**
* Dans la colonne **`Seconds to resolution`**
* Classé par l’horodatage **`created_at`**
* [!UICONTROL Filter] :

* **[!DNL Zendesk]Temps moyen/médian jusqu’à la première réponse**
   * Billets comptabilisés
   * Statut EN clôturé, résolu

* Dans le tableau **`[!DNL Zendesk] tickets`**
* Cette mesure effectue une **Moyenne (ou Médiane)**
* Dans la colonne **`Seconds to first response`**
* Classé par l’horodatage **`created_at`**
* [!UICONTROL Filter] :

>[!NOTE]
>
>Veillez à [ajouter toutes les nouvelles colonnes en tant que dimensions aux mesures](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) avant de créer de nouveaux rapports.

### Rapports

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric] : `New Tickets`
   * [!UICONTROL Filter] :
   * Statut IN `new, open, pending`

* `A` de mesure : `New tickets`
* `Time period` : `All time`
* `Interval` : `None`
* `Chart Type` : `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric] : `New Tickets`
   * [!UICONTROL Filter] :
   * Statut IN `solved, closed`

* `A` de mesure : `New tickets`
* `Time period` : `All time`
* `Interval` : `None`
* `Chart Type` : `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric] : `Average time to first response`

* `A` de mesure : `Average time to first response`
* `Time period` : `All time`
* `Interval` : `None`
* `Chart Type` : `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric] : `Average time to resolution`
   * [!UICONTROL Filter] :
   * Statut IN `solved, closed`

* `A` de mesure : `Average time to resolution`
* `Time period` : `All time`
* `Interval` : `None`
* `Chart Type` : `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric] : `New Tickets`

* `A` de mesure : `New tickets`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Group by` : `status`
* `Chart Type` : `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric] : `New Tickets`

   * [!UICONTROL Metric] : `New Tickets`

* `A` de mesure : `New tickets`
* `B` de mesure : `Solved tickets`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Chart Type` : `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric] : `Average time to first response`

* `A` de mesure : `Average time to first response`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Chart Type` : `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric] : `Average time to resolution`
   * [!UICONTROL Filter] :
   * Statut IN `solved, closed`

* `A` de mesure : `Average time to resolution`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Chart Type` : `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric] : `Distinct users filing tickets`

* `A` de mesure : `Distinct users filing tickets`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Chart Type` : `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric] : `New Tickets`

* `A` de mesure : `New tickets`
* `Time period` : `All time`
* `Interval` : `None`
* `Group by` : `Ticket created_at (day of week)`
* `Chart Type` : `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom` : `Top 100% sorted by created_at (hour of the day)`

* `A` de mesure : `New tickets`
* `Time period` : `All time`
* `Interval` : `None`
* `Group by` : `Ticket created_at (hour of the day)`
* `Chart Type` : `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric] : `Average lifetime revenue`

* `A` de mesure : `Average lifetime revenue`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Group by` : `User has filed a support ticket?`
* `Chart Type` : `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 
     [!UICONTROL Metric]: Users

* `A` de mesure : `New users`
* `Time period` : `All time`
* `Interval` : `Monthly`
* `Group by` : `User has filed a support ticket?`
* `Chart Type` : `Column`
